---
marp: true
---

# Everyday Linked Data

Alex Michael Berry
github.com/almibe
twitter.com/alexmiberry

---

# Goals

* Explain how RDF and Linked Data are more general purpose than a lot of people give them credit for
* Suggest adopting RDF for more common day to day data tasks rather than only large projects
* Propose some ideas for moving forward with this and go over some issues I've ran into

---

# Non-Goals

* Teach RDF in 20 minutes
* Make specific recomendations for software
* Be 100% correct about everything I say :P

---

# But First

* Breifly explain what RDF and Linked Data are
* Explain their role in libraries and archives

---

# RDF (Resource Description Framework) in Two Slides

* RDF was developed in the late 90's to help describe web sites, but its use has expanded since then (see https://bioportal.bioontology.org/)
* RDF builds on a very simple `subject predicate object` model that is also very flexible

---

# RDF in Two Slides

* RDF is very modular, and a number of specs have sprung up around it to support:
    * Access/Modification/Query (SPARQL + HTTP specs)
    * Serialization (too many to mention)
    * Schema/Validation/Constraint (RDFS & SHACL)
    * Ontology Support/Inferencing (OWL)

---

# Linked Data in Two Slides

from https://www.w3.org/2011/gld/wiki/5_Star_Linked_Data

Tim Berners-Lee, the inventor of the Web and initiator of the Linked Data project, suggested a 5 star deployment scheme for Linked Data. The 5 Star Linked Data system is cumulative. Each additional star presumes the data meets the criteria of the previous step(s).

---

# Linked Data in Two Slides

☆ Data is available on the Web, in whatever format.	
☆☆ Available as machine-readable structured data, (i.e., not a scanned image).
☆☆☆ Available in a non-proprietary format, (i.e, CSV, not Microsoft Excel).	
☆☆☆☆ Published using open standards from the W3C (RDF and SPARQL).	
☆☆☆☆☆ All of the above and links to other Linked Open Data.

---

# RDF in Libraries and Archives

* Usage of RDF is increasing in the libraries and archives world
* Standards such as MODS/MADS have mappings to RDF
* BIBFRAME is the elephant in the room
* The Fedora repository and others implement the Linked Data Platform spec

---

# RDF in Libraries and Archives

* So there is a professional development aspect to learning about Linked Data and RDF
<br/>
* That isn't what this talk is about

---

# What is this talk about?

* Using Linked Data/RDF for day to day tasks
* Namely working with data that won't leave your computer/private server
    * Can still take advantage of existing Linked Data
* Is this antithetical to linked (open) data?
    * I'd argue that it isn't since it will increase the usage of Linked Data

---

# Examples

* Work Stuff
    * Personal note taking
    * TODO tracking
    * Internal modeling
    * Analytics

---

# Examples

* Non-Work Stuff
    * Personal budgeting
    * Recipe management
    * Personal/Pet medical records
    * TTRPG Note taking

---

# Examples

* So kind of anything 
    * Probably not best for working directly with large amounts of text or binary data though

---

# Aspects of RDF Adoption

* Education/Documentation
* Tooling
* Certain concepts can be overly challenging or esoteric

---

# Education/Documentation

* Well written specs
* But there's a lot of outdated information
    * It feels like 1/2 of all links are broken when researching
* Books are often outdated or very focused on a single aspect of Linked Data/RDF
* Vendor specific/directly from the vendor (aka marketing)
* Much is extremely ∀cadƎmic

---

# Tooling

* All popular (and most niche) languages have some support for RDF
    * I first learned about RDF via Prolog
* Many stores/servers exist
* It can be very hard to determine what exactly is supported by any given library/tool
* A lot is propritary or inactive

---

# Challenging/Esoteric Concepts

* What are the best practices for crafting IRIs when you aren't talking about webpages?
* Blank Nodes
* Reification
* Schemas vs Ontologies

---

# Comparing RDF

* RDF has strengths and weaknesses compared to the common gotos
* RDF can be file based or server based
* RDF has a common query language
* RDF is graph based so cardinality, nested data, and sparse data are well supported
* Linking different data sources is baked in

---

# Comparing RDF

* Has a simple enough data model that ORMs aren't needed
    * I think it's important when working with RDF programatically that you deal with the actual RDF data model and don't abstract it
* Allows for a gradual adoption of a schema
    * Allows you to just start storing data and evolve a schema as you go if needed
    * But schema/validation/constraint support in tooling is currently lacking IMHO, I think tools need to become more opinionated in this regard

---

# Advice for Adopting Linked Data

* Have a specific project and goals in mind before looking into adopting Linked Data
    * Is validation important?
    * Do you need transaction support?
    * Do you need full text search?
    * What persistence do you need (Distributed DB/local files/memory)
    * Single or multi process/user access

---

# Advice for Adopting Linked Data

* Data modeling like software development is iterative, so be ready to experiment and make changes as you go
    * This includes both data modeling decisions as well as software choices
    * Look to existing standards and implementations for ideas, but realize your use case may require something different
* Have fun

---

# Thanks

Alex Michael Berry
github.com/almibe
twitter.com/alexmiberry
