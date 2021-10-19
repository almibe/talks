---
marp: true
---

# Storing Ligature's Data Model in Key-Value Database

Alex Michael Berry
github.com/almibe

---

# Overview

 * Briefly explain Ligature
 * Cover how Hexastore and Key-Value Databases fit well with Ligature's Data Model

---

# Background

 * Ligature is a hobby project of mine
 * I've always been interested in using graphs to model information
 * So I wanted something that would allow me to use graphs as casually (and potentially universally) as other data formats
 * Something along the lines of spread sheets for knowledge graphs
   * Not a 1:1 comparison though since although both are quite visual I think graphs need more programmatic access, especially when they are densely linked

---

# Example - Visual

![](output.svg)

---

# Example - Dot

```
digraph G {
 backend  -> mysql1           [ label="dependsOn" ];
 backend  -> solr1            [ label="dependsOn"];
 mysql1   -> "127.0.0.1:3306" [ label="addr" ];
 mysql1   -> "8.0"            [ label="version" ];
 solr1    -> "127.0.0.1:8983" [ label = "addr" ];
 solr1    -> "8.10.0"         [ label="version" ];
 backend  -> "127.0.0.1:8888" [ label = "addr" ];
 frontend -> backend          [ label="dependsOn"];
 frontend -> "127.0.0.1:9999" [ label = "addr" ];
}
```

---

# Example - Serialized Ligature

```
<backend>  <dependsOn> <mysql1>         <1>
<backend>  <dependsOn> <solr1>          <2>
<mysql1>   <addr>      "127.0.0.1:3306" <3>
<mysql1>   <version>   "8.0"            <4>
<solr1>    <addr>      "127.0.0.1:8983" <5>
<solr1>    <version>   "8.10.0"         <6>
<backend>  <addr>      "127.0.0.1:8888" <7>
<frontend> <dependsOn> <backend>        <8>
<frontend> <addr>      "127.0.0.1:9999" <9>
```

---

# Ligature

 * Started as an RDF implementation
 * Original intention was to learn more about RDF through practice
 * Realized there were some changes I could make to RDF to make it fit my personal use cases better

---

# Identifiers

 * RDF uses IRIs for Identifiers
 * IRIs are defined by https://datatracker.ietf.org/doc/html/rfc3987
 * They are very complicated, and even established libraries like JENA only partially support them
   * https://jena.apache.org/documentation/notes/iri.html
 * Since RDF is focused on the Semantic Web simple identifiers don't make sense
 * Since I want to support local only datasets I'm fine with allowing much simpler identifiers

---

# Identifiers

 * I've decided to support Identifiers as a string that contains only valid URL characters
 * So all valid URLs are Identifiers, but an Identifier doesn't have to be a valid URL
 * Use a URI if you want, use a regular "variable" name if you want, use a (namespaced) atomic id counter if you want, use a (namespaced) nanoid if you want, use a (namespaced) UUID if you want
 * This make Identifiers align with my use case and a lot easier work with in general
 * Also because of the focus on supporting things like nanoid and UUID blank nodes aren't needed

---

# Ligature's Data Model

 * A Ligature instance contains a set of named Datasets
 * Datasets contain a set of Statements
 * Statements are represented as following

| Entity     | Attribute  | Value      | Context    |
| ---------- | ---------- | ---------- | ---------- |
| Identifier | Identifier | Identifier | Identifier |
|            |            | Literal    |            |

---

# Literals

 * Literals in Ligature are currently pretty minimal
   * Identifier - a Ligature Identifier
   * String - a utf-8 string
   * Integer - a 64-bit integer (Java's longs, Rust's i64, etc)
   * Bytes - a byte array
 * I wanted to start with a minimal set, more might be added

---

# Contexts

 * A big difference from RDF
 * The final position in a quad in Ligature is called the Context
 * Every Statement in a Dataset needs an unique Context
 * This allows for making Statements about Statements
   * Time stamping statements
   * crediting the source of Statements
   * noting if a Statement is still valid
   * pointing to Statements that supersede this one, etc.

---

# Hexastore

![](hexastore-paper.png)

* A 2008 paper comparing different storage methods for RDF triples, arguing for a method that can be adapted to work with Key-Value Databases

---

# Key-Value Databases

 * Many type of Key-Value Database exist
 * For this to work best the following requirements should be met
   * Transactional
   * Sorted
   * Scannable

---

# Key-Value Databases

 * Many Key-Value Databases fit these requirements
   * Native/Embedded - RocksDB (FaceBook), LMDB (OpenLDAP)
   * JVM/Embedded - Xodus (JetBrains), MVStore (H2), MapDB
   * Browser - IndexedDB
   * Distributed - FoundationDB (Apple)

---

# Hexastore + Key-Value Databases

  * A simple view of this approach is for every triple {s,p,o} you store six entries in a Key-Value Database, one for each permutation in the key position

  | Key | Value | Note              |
  | --- | ----- | ----------------- |
  | spo |       |                   |
  | sop |       |                   |
  | pso |       | Not always needed |
  | pos |       |                   |
  | osp |       |                   |
  | ops |       | Not always needed |

---

# Hexastore + Key-Value Databases

 * To get this to work correctly all of the values of {s,p,o} should be fixed length ids instead of the actual value the ids could also include type infomation
 * This requires several lookup tables to covert Subjects to Ids and Ids to Subjects
 * Also each entry should be prefixed with a code saying which type of entry it is (SPO = 1, SOP = 2, PSO = 3, POS = 4, etc.)
 * But since all the values are known fixed size and sorted scanning the database allows for quick lookups

---

# Lookup Example

 * Consider you want to find all triples with a given predicate and object value
 * Just find the ids for the predicate and object and then do a scan for all entires with the given prefix

`ENTRY_TYPE + PREDICATE_ID + OBJECT_ID`

 * You can then decode the matching entries to get all the subjects that make up the matching triples

---

# Applying Hexastore to Ligature

 * The basics still apply
 * The Context is the main difference between the two since the models are almost the same with some cosmetic name changes
 * Luckily since the Context is always unique for a given Dataset only one additional row is needs `CEAV`
 * A lookup with a Context involved is essentially an exists check

---

# Ligature

  | Key  | Value | Note               |
  | ---- | ----- | ------------------ |
  | eavc |       |                    |
  | evac |       |                    |
  | aevc |       | Not always needed  |
  | avec |       |                    |
  | veac |       |                    |
  | vaec |       | Not always needed  |
  | ceav |       | Unique to Ligature |

---

# Conclusion

 * Ligature tries to be portable thanks to its simple model
 * Key-Value Databases are probably the best fit but Document, Column, and Relational Databases can also be used

---

# Thanks

Alex Michael Berry
github.com/almibe
twitter.com/alexmiberry
