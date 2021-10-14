---
marp: true
---

# Introduction to Ligature

Alex Michael Berry
github.com/almibe
twitter.com/alexmiberry

---

# Overview

 * Explain the goals I had that led to starting work on Ligature
 * How Ligature differs from related tools
 * Brief status update and next goals

---

# Overview

 * This is more of a "Hello" introduction and not a teaching introduction
 * This project is still under development so many things are likely to change

---

# Background

 * I've always been interested in using graphs to model information
 * So I wanted something that would allow me to use graphs as casually (and potentially universally) as other data formats
 * Something along the lines of spread sheets for knowledge graphs

---

# Graph Databases

 * Really cool, but not really what I'm looking for
 * Usually client/server focused
 * Rarely embeddable
 * Usually just a single implementation (in Java or C++)
 * Have complicated feature sets that focus on enterprise use cases
 * Often are document databases where a field in a document can be a link to another document

---

# RDF

 * Much closer to what I want
 * I was first introduced to RDF in class in grad school
 * "Statement" oriented rather than *Document* oriented
 * Has a clear specification with serialization formats, query language, schemas, and ontologies
 * Multiple implementations

---

# RDF

 * Still has some issues for what I want to do
 * Was created for the Semantic Web so its goals don't align with mine
 * Implementations can still be complex to embed and use
 * Each implementation can implement a different subset of the various standards

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
   * If you plan on linking Ligature datasets you should know that ahead of time and can use URIs or a different scheme if you want\*
   * If you never plan on linking your dataset then you are free to do whatever\*

\*as long as it is a legal identifier

---

# Identifiers

 * I've decided to support Identifiers as a string that contains only valid URL characters
 * So all valid URLs are Identifiers, but an Identifier doesn't have to be a valid URL
 * Use a URL if you want, use a URN if you want, use a URI if you want, use a regular "variable" name if you want, use a (namespaced) atomic id counter if you want, use a (namespaced) nanoid if you want, use a (namespaced) UUID if you want
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
   * String - a utf-8 string
   * Integer - a 64-bit integer (Java Longs, Rust i64, etc)
   * Bytes - a byte array
 * I wanted to start with a minimal set, more might be added

---

# Contexts

 * A big difference from RDF
 * The final position in a quad in Ligature is called the Context
 * Every Statement in a Dataset needs an unique Context
 * This allows for making Statements about Statements
 * Time stamping statements, crediting the source of Statements, noting if a Statement is still valid, pointing to Statements that supersede this one, etc.

---

# Status

 * Multiple implementations are being worked on
 * A specification is also be developed along side implementations
 * A scripting language called Wander is being developed as well for interacting with Ligature instances
 * Focus will shift to schema/ontology support after this based on RDFS/SHACL/OWL (aka when the real fun starts)

---

# Thanks

Alex Michael Berry
github.com/almibe
twitter.com/alexmiberry
