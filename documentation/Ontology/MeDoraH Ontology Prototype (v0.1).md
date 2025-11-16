# MeDoraH Ontology Prototype (v0.1)

MeDoraH Ontology for Narratives of Digital Humanities 
**Version:** 0.1 (Prototype) 
**Status:** Research prototype (not yet finalised) 

---

## 1. Introduction and Scope

The MeDoraH project investigates how semantic web technologies and digital methods can support the analysis of oral history interviews about the formation, disruption, and change of Digital Humanities (DH). The interviews (and related sources) are used to study:

- Individual and collective agency  
- Knowledge creation, mobility, and loss  
- Spatial, institutional, and disciplinary dynamics  
- Changing narratives over time across different sources and perspectives  

This ontology prototype provides a conceptual schema for:

- Modelling entities mentioned in oral history sources (e.g. people, organisations, projects, methods, technologies, places, times)  
- Expressing relations between them (e.g. collaboration, creation, use, influence, spatial and temporal context)  
- Supporting network analysis of “networks that emerge from oral history accounts” rather than pre-defined social networks  

The ontology is designed to:

- Serve as the core schema for a Knowledge Graph (KG) storing structured data extracted from interviews and related sources  
- Support mixed-methods analysis that combines qualitative interpretation with network and text analysis  
- Remain lightweight and interpretable for domain experts (oral historians, DH scholars) while being compatible with standard semantic-web practices  

This is a **prototype**, not a closed upper ontology. It is expected to evolve in response to:

- Empirical findings from interviews  
- Methodological and theoretical discussions in the project  
- Alignment needs with standards such as CIDOC-CRM and domain ontologies used in heritage and DH  

### 1.1 Strategic Purpose of v0.1

This document describes the **first-pass, entity-centric core** of the MeDoraH Ontology.

- **Primary goal:** model the factual entities (people, places, projects, concepts) and relations recalled in the oral histories.  
- **Focus:** “what is mentioned” (entities and relations) rather than “how it is told” (narrative structure and subjectivity).  

This foundational layer is a prerequisite for the project’s deeper hermeneutic goals. It provides a stable, queryable **“what layer”** that will underpin the future **v0.2 Narrative Layer**, which will focus on modelling:

- Subjectivity and stance  
- Recollection and reinterpretation  
- Intersubjectivity and interviewer–interviewee dynamics  



---

## 2. Design Principles and Modelling Approach

### 2.1 Conceptual Focus: Narratives of Recollection

The long-term aim of the MeDoraH ontology is to model **acts of recollection** in oral history interviews.  

- **v0.1** does **not** yet model narrative structures themselves.  
- Instead, it provides a **robust, queryable model of recalled entities** (people, institutions, projects, concepts, events and their relationships.)

In practice:

- Relations are interpreted as **claims grounded in sources** (interviews, related documents).  
- The KG will record **provenance** and **confidence scores** via the data pipeline, so different or conflicting accounts can coexist.  
- v0.1 is deliberately conservative: it models what is being talked about and how things connect, but not yet the detailed rhetorical structure of the storytelling.



### 2.2 Top-Level Categories

The ontology adopts a small, legible set of top-level categories that are meaningful for both humanists and technologists.

| Top-level class  | Informal meaning                                   | Typical examples                         |
| ---------------- | -------------------------------------------------- | ---------------------------------------- |
| `Actor`          | Agents capable of intentional action               | People, organisations, collectives       |
| `Event`          | Things that happen over time                       | Projects, activities, processes          |
| `Item`           | Things that are created, used, or depended on      | Publications, datasets, methods, devices |
| `SpatialEntity`  | Places                                             | Cities, regions, institution locations   |
| `TemporalEntity` | Times                                              | Years, decades, historical periods       |
| `Property`       | Classifications and characteristics assigned by us | Roles, genres, qualifications            |

These categories are:

- Familiar enough for non-technical contributors.  

- Expressive enough to support semantic modelling and network analysis.

  

### 2.3 Relation Patterns

The ontology centres on a small number of high-level relation patterns, which can be specialised as needed:

| Pattern                    | Informal description                               |
| -------------------------- | -------------------------------------------------- |
| `Actor → Actor`            | Interpersonal and organisational relationships     |
| `Actor → Item`             | Creation, use, and conceptual application of items |
| `Actor → Event`            | Participation in events and projects               |
| `Event → Spatial/Temporal` | Where and when events occur                        |
| `Actor → Spatial`          | Residence and movement                             |
| `Item → Item`              | Compositional and technical dependencies           |
| `Entity → Property`        | Roles, skills, genres, classifications             |
| `Entity → Entity`          | Conceptual or personal influence                   |

#### High-Level Relation Summary (Informally)

* **Actors** engage in **Events**, create and use **Items**, relate to other **Actors**, and are located in or move between **Places**.
* **Events** occur at **Places** and during **Times**.
* **Items** may depend on or be part of other **Items**.
* All **Entities** can be associated with **Properties** (roles, skills, genres, classifications).
* **Entities** can influence each other conceptually or personally.



These patterns are derived from the project’s research questions around:

- Agency (individual and collective)  
- Knowledge mobility and loss  
- Spatial and institutional layering  
- Networks that **emerge from recollections**, not just from external records



### 2.4 Relationship to Extraction and KG Population

The ontology is designed to be:

- **Amenable to NLP-based extraction** of entities and relations from transcripts (e.g. Person, Organisation, Project, Method, Technology, Place, Time).  
- **Usable as a schema** for an RDF-based KG queried via SPARQL and other interfaces. 

Definitions and scope notes indicate, where relevant:

- Which relations are intended to be primarily populated by **automated pipelines**.  
- Which require **human annotation, interpretation, or correction** (e.g. influence, stance, beliefs).



---

## 3. Ontology Overview

### 3.1 Namespace and Naming

- **Prefix:** `medorah:`  
- **Core superclass:** `medorah:Entity`  

Unless otherwise stated, classes and properties mentioned in this document are assumed to be in the `medorah:` namespace.

Example (Turtle):

```turtle
@prefix medorah: <http://example.org/medorah/> .
@prefix rdfs:    <http://www.w3.org/2000/01/rdf-schema#> .

medorah:Person a rdfs:Class ;
    rdfs:subClassOf medorah:Actor ;
    rdfs:label "Person"@en .
```


### 3.2 Informal Class Hierarchy

**Top level:**

* `Entity`
  * `Actor`
    * `Person`
    * `Organisation`
    * `Collective`
  * `Event`

    * `Activity`
    * `Project`
    * `Process`
  * `Item`

    * `InformationItem`

      * `AudioVisualItem`
      * `ComputationalItem`

        * `Software`
        * `Dataset`
      * `Publication`

        * `LiteraryOrScholarlyWork`
        * `Catalogue`
    * `ConceptualItem`

      * `Theory`
      * `Method`
      * `Language`
      * `Technology`
      * `Discipline`

        * `FieldOfStudy`
        * `AcademicDiscipline`
      * `SkillAndKnowledge`
    * `PhysicalItem`

      * `Product`
      * `Device`
  * `SpatialEntity` (Place)
  * `TemporalEntity` (Time)

**Separate branch:**

* `Property`
  * `Role`
  * `GenreStyle`
  * `Qualification`



---

## 4. Class Reference

This section defines each class with label, definition, and examples. Only key subclasses are expanded; further subclasses can follow the same pattern.

### 4.1 Core Superclass

#### 4.1.1 `Entity`

* **Label:** Entity

* **IRI:** `medorah:Entity`

* **Definition:**
  A thing that can be referred to in the narratives modelled in MeDoraH, including persons, organisations, events, items, places, times, and properties.

* **Notes:**

  * Root of the main hierarchy.
  * Used as the domain or range of generic properties such as `hasProperty`, `hasAttribute`, and `influences`.

  

---

### 4.2 Actor Module

| Class          | Subclass of | Short definition                                      |
| -------------- | ----------- | ----------------------------------------------------- |
| `Actor`        | `Entity`    | Entity capable of intentional action or participation |
| `Person`       | `Actor`     | Individual human agent/narrator/subject               |
| `Organisation` | `Actor`     | Formal institution or organisational entity           |
| `Collective`   | `Actor`     | Informal or loosely bounded group acting collectively |

#### 4.2.1 `Actor`

* **Definition:**
  An entity capable of intentional action or participation in events, as recalled in the oral history narratives.
* **Notes:**

  * Includes individuals and group-level actors (formal and informal).
  * Central to research questions about agency and responsibility.

#### 4.2.2 `Person`

* **Definition:**
  An individual human being who appears as an agent, narrator, or subject in the sources.
* **Examples:**

  * An interviewee describing their role in founding a centre.
  * A collaborator mentioned as having developed a tool or method.
* **Typical sources:**

  * Interview transcripts (names, pronouns, self-descriptions).
  * External authority files (e.g. VIAF, ORCID) for reconciliation.

#### 4.2.3 `Organisation`

* **Definition:**
  A formally recognised institution or organisational entity involved in DH-relevant activities, such as universities, departments, centres, archives, companies, or projects with institutional identity.
* **Examples:**
  * A university department hosting DH courses.
  * A research centre or archive supporting a DH project.

#### 4.2.4 `Collective`

* **Definition:**
  A loosely defined group, committee, informal network, or community that may not be fully institutionalised but is described as acting collectively in the sources.
* **Examples:**

  * An early informal DH working group.
  * A mailing list community or conference “crowd” spoken of as a group.

---

### 4.3 Event Module

| Class      | Subclass of | Short definition                                     |
| ---------- | ----------- | ---------------------------------------------------- |
| `Event`    | `Entity`    | Temporal occurrence in which actors can participate  |
| `Activity` | `Event`     | Bounded, action-centred event                        |
| `Project`  | `Activity`  | Structured, often funded activity with goals/outputs |
| `Process`  | `Event`     | Series of steps or transformations                   |

#### 4.3.1 `Event`

* **Definition:**
  A temporal occurrence or happening in which actors can participate, and which can be located in time and space.
* **Notes:**

  * Represents events **as recalled in the narrative**.
  * v0.1 focuses on the event as an entity; the act of recalling the event will be modelled explicitly in the v0.2 Narrative Layer.

#### 4.3.2 `Activity`

* **Definition:**
  An event characterised by actors performing specific actions, typically bounded in time, such as workshops, meetings, or concrete project tasks.
* **Examples:**

  * A DH workshop.
  * A code sprint or collaborative annotation session.

#### 4.3.3 `Project`

* **Definition:**
  A planned, structured activity or set of activities, often with defined goals, funding, and outputs, mentioned in relation to the development of DH.
* **Examples:**

  * A long-term DH project to digitise and analyse a corpus.
  * A grant-funded pilot project to build a tool.

#### 4.3.4 `Process`

* **Definition:**
  A series of steps or transformations with inputs and outputs, often used to model workflows or technical/historical processes (e.g. digitisation, adoption of technology).

* **Examples:**

  * A digitisation workflow.
  * The process of adopting a new computational method or platform.

  

---

### 4.4 Item Module

#### 4.4.1 `Item`

* **Definition:**
  Anything that can be created, used, or depended on in DH practice, including information objects, conceptual constructs, and physical artefacts.

---

#### 4.4.1.1 `InformationItem`

* **Definition:**
  A symbolic object whose primary function is to convey information or meaning (textual or non-textual), such as publications, datasets, or software code.
* **Examples:**

  * An interview transcript.
  * A dataset of encoded texts.
  * The source code of a DH tool.

**Key subclasses:**

| Class                     | Short definition                                             |
| ------------------------- | ------------------------------------------------------------ |
| `AudioVisualItem`         | Non-textual media items (audio/video interviews, recordings) |
| `ComputationalItem`       | Information items executed or processed by machines          |
| `Software`                | Executable programs or scripts used in DH                    |
| `Dataset`                 | Structured collections of data (e.g. corpus, annotations)    |
| `Publication`             | Formally disseminated information items                      |
| `LiteraryOrScholarlyWork` | Scholarly articles, monographs, essays                       |
| `Catalogue`               | Catalogues, finding aids, or inventories                     |

---

#### 4.4.1.2 `ConceptualItem`

* **Definition:**
  An immaterial construct used to organise, interpret, or generate knowledge, such as theories, methods, technologies, disciplines, and skills.
* **Examples:**

  * “Text encoding” as a method.
  * “Digital humanities” as a field of study.
  * “Indexing” as a conceptual technique.

**Key subclasses:**

| Class               | Short definition                                             |
| ------------------- | ------------------------------------------------------------ |
| `Theory`            | Explanatory frameworks or theoretical positions              |
| `Method`            | Ways of doing things (e.g. “close reading”, “topic modelling”) |
| `Language`          | Natural or programming languages                             |
| `Technology`        | Named technologies or platforms (e.g. “XML”, “TeX”)          |
| `Discipline`        | Disciplines or fields (with `FieldOfStudy` and `AcademicDiscipline`) |
| `SkillAndKnowledge` | Capabilities or expertise (e.g. “programming”, “cataloguing”) |

---

#### 4.4.1.3 `PhysicalItem`

* **Definition:**
  Tangible artefacts or devices involved in DH practice, such as hardware, physical media, or equipment.

**Key subclasses:**

| Class     | Short definition                                        |
| --------- | ------------------------------------------------------- |
| `Product` | Commercial items (e.g. hardware products) used in DH    |
| `Device`  | Functional items or components (e.g. servers, scanners) |

---

### 4.5 Spatial and Temporal Module

#### 4.5.1 `SpatialEntity` (Place)

* **Definition:**
  A geographic or spatial location relevant to the narratives, including institution locations, cities, regions, or countries.
* **Examples:**

  * A city where a DH centre is located.
  * A country relevant to cross-national comparison.

#### 4.5.2 `TemporalEntity` (Time)

* **Definition:**
  A temporal expression or interval associated with events or other entities, such as dates, periods, or durations.

* **Examples:**

  * A specific year (e.g. “1998”).
  * A period like “the 1990s”.

  

---

### 4.6 Property Module

| Class           | Subclass of | Short definition                                             |
| --------------- | ----------- | ------------------------------------------------------------ |
| `Property`      | `Entity`    | Abstract classification or characteristic assigned to other entities |
| `Role`          | `Property`  | Social or professional role of a person                      |
| `GenreStyle`    | `Property`  | Genre or style classification of an item                     |
| `Qualification` | `Property`  | Degrees, certifications, or prerequisites                    |

#### 4.6.1 `Property`

* **Definition:**
  An abstract characteristic or classification that can be associated with other entities (e.g. roles, genres, qualifications).
* **Modelling rationale:**

  * `Property` (and its children like `Role`, `GenreStyle`) is intentionally kept **separate** from `ConceptualItem`.
  * `Property` is used for classifications that we, as researchers, apply to entities (e.g. giving a person the role “Professor”, or classifying an interview as “Oral History Interview”).
  * `ConceptualItem` is used for ideas that are themselves **objects of discourse** in the interview (e.g. the method “Text Encoding” being discussed).
  * This allows us to query our **analytic classifications** separately from what interviewees talk about.

#### 4.6.2 `Role`

* **Definition:**
  A property that describes social or professional roles played by persons (e.g. “professor”, “archivist”, “software developer”).
* **Usage:**
  Typically associated with `Person` via `hasRole`.

#### 4.6.3 `GenreStyle`

* **Definition:**
  A property that classifies objects by type, genre, or style (e.g. “oral history interview”, “technical report”, “manifesto”).
* **Usage:**
  Often associated with `InformationItem` via `isCategorisedAs` (see Section 5.6).

#### 4.6.4 `Qualification`

* **Definition:**
  A property describing conditions, credentials, or requirements such as degrees, certifications, or prerequisites.

* **Usage:**

  * Linked to a `Person` to record degrees or professional qualifications.
  * Linked to an `Activity`/`Event` to capture entry requirements.

  

---

## 5. Object Property Reference

This section describes top-level object properties and their sub-properties. Example triples use Turtle syntax.

### 5.1 `Actor → Actor`: `relatesTo`

#### 5.1.1 `relatesTo`

* **Label:** relates to
* **IRI:** `medorah:relatesTo`
* **Domain:** `Actor`
* **Range:** `Actor`
* **Definition:**
  A general relationship between two actors, to be specialised by sub-properties such as employment or collaboration.

**Sub-properties (indicative, not exhaustive):**

| Property                      | Domain   | Range          | Informal meaning                          |
| ----------------------------- | -------- | -------------- | ----------------------------------------- |
| `hasEmploymentAt`             | `Person` | `Organisation` | Person is employed by an organisation     |
| `founds`                      | `Person` | `Organisation` | Person founds/establishes an organisation |
| `collaboratesWith`            | `Person` | `Person`       | Two persons collaborate                   |
| `communicatesWith`            | `Person` | `Person`       | Persons are in communicative contact      |
| `isColleagueOf`               | `Person` | `Person`       | Persons share a professional context      |
| `hasPersonalRelationshipWith` | `Person` | `Person`       | Non-purely professional relation          |

* **Modelling notes:**

  * Some sub-properties can be declared **symmetric** (e.g. `collaboratesWith`, `isColleagueOf`, `hasPersonalRelationshipWith`).
  * Others are directional (e.g. `hasEmploymentAt`, `founds`).

  

---

### 5.2 `Actor → Item`: `creates` (inverse `createdBy`)

#### 5.2.1 `creates`

* **Label:** creates
* **IRI:** `medorah:creates`
* **Domain:** `Actor`
* **Range:** `Item`
* **Definition:**
  The actor is responsible for creating or bringing into existence an item (information, conceptual, or physical).

**Sub-properties:**

| Property                  | Domain         | Range                     | Informal meaning                               |
| ------------------------- | -------------- | ------------------------- | ---------------------------------------------- |
| `publishesIn`             | `Person`       | `Publication`             | Person publishes in a given publication        |
| `authorsIn`               | `Person`       | `LiteraryOrScholarlyWork` | Person authors a scholarly work                |
| `developsInformationItem` | `Actor`        | `InformationItem`         | Actor develops or produces an information item |
| `craft`                   | `Person`       | `PhysicalItem`            | Person crafts a physical item                  |
| `manufacture`             | `Organisation` | `PhysicalItem`            | Organisation manufactures a physical product   |

**Example:**

```turtle
:person_A medorah:creates :dataset_X .
:person_A medorah:authorsIn :article_Y .
```

---

### 5.3 `Actor → Item`: `uses` (inverse `usedBy`)

#### 5.3.1 `uses`

* **Label:** uses
* **IRI:** `medorah:uses`
* **Domain:** `Actor`
* **Range:** `Item`
* **Definition:**
  The actor uses or employs an item in practice.

**Sub-properties:**

| Property                 | Domain   | Range             | Informal meaning                              |
| ------------------------ | -------- | ----------------- | --------------------------------------------- |
| `employsInformationItem` | `Actor`  | `InformationItem` | Actor uses a dataset, publication, or similar |
| `appliesConceptualItem`  | `Person` | `ConceptualItem`  | Person applies a method, theory, or concept   |
| `employsTool`            | `Person` | `PhysicalItem`    | Person uses a device or physical tool         |

**Example:**

```turtle
:person_B medorah:appliesConceptualItem :method_TextEncoding .
:person_B medorah:uses :software_ToolX .
```



---

### 5.4 `Actor → Event`: `engagesIn` (inverse `isEngagedInBy`)

#### 5.4.1 `engagesIn`

* **Label:** engages in
* **IRI:** `medorah:engagesIn`
* **Domain:** `Actor`
* **Range:** `Event`
* **Definition:**
  The actor is involved in or participates in an event.

**Sub-properties:**

| Property           | Domain         | Range      | Informal meaning                    |
| ------------------ | -------------- | ---------- | ----------------------------------- |
| `participatesIn`   | `Person`       | `Event`    | Person participates in an event     |
| `worksOn`          | `Person`       | `Project`  | Person works on a specific project  |
| `hosts`            | `Organisation` | `Event`    | Organisation hosts an event         |
| `performsActivity` | `Person`       | `Activity` | Person performs a specific activity |

---

### 5.5 `Actor → Entity`: `hasViewAbout` (inverse `isViewedAs`)

> Note: Although earlier drafts used “Actor → Item”, the sub-properties clearly support `Entity` as the range; this documentation adopts the more general pattern `Actor → Entity`.

#### 5.5.1 `hasViewAbout`

* **Label:** has view about
* **IRI:** `medorah:hasViewAbout`
* **Domain:** `Actor` (typically `Person`)
* **Range:** `Entity`
* **Definition:**
  Captures an actor’s expressed view or stance regarding another entity.

**Sub-properties:**

| Property                | Domain   | Range    | Informal meaning                                     |
| ----------------------- | -------- | -------- | ---------------------------------------------------- |
| `holdsBeliefAbout`      | `Person` | `Entity` | Person expresses a belief about an entity            |
| `expressesIntention`    | `Person` | `Entity` | Person expresses a future-oriented plan or intention |
| `expressesPreference`   | `Person` | `Entity` | Person expresses preference or evaluation            |
| `expressesEmotionAbout` | `Person` | `Entity` | Person expresses an emotional stance                 |

* **Notes:**

  * In v0.1, these are the main properties for capturing **subjective and interpretive** aspects of oral history accounts.
  * They should always be **backed by textual evidence and provenance** in the KG.
  * In v0.2, these views will be anchored to specific `NarrativeSegment`s, not just to the `Actor` globally.

  

---

### 5.6 `Entity → Property`: `hasProperty` (inverse `isPropertyOf`)

#### 5.6.1 `hasProperty`

* **Label:** has property
* **IRI:** `medorah:hasProperty`
* **Domain:** `Entity`
* **Range:** `Property`
* **Definition:**
  Associates an entity with a property such as role, genre, qualification, or skill.

**Sub-properties:**

| Property          | Domain   | Range                          | Informal meaning                                             |
| ----------------- | -------- | ------------------------------ | ------------------------------------------------------------ |
| `hasSkill`        | `Person` | `SkillAndKnowledge`            | Person possesses a particular skill or knowledge             |
| `hasRole`         | `Person` | `Role`                         | Person holds a certain social/professional role              |
| `hasAttribute`    | `Entity` | `rdfs:Literal`                 | Literal attribute (e.g. code, note) that does not justify a separate entity |
| `isCategorisedAs` | `Entity` | `Property` (e.g. `GenreStyle`) | Classification of an entity by genre or similar property     |

> Note: For clarity and consistency with the `Property` module, `isCategorisedAs` is documented here with range `Property` (typically `GenreStyle`). If you wish to treat some category labels as `ConceptualItem`s, they can be modelled separately and linked via additional properties.

---

### 5.7 `Event → Spatial`: `occursAt`

#### 5.7.1 `occursAt`

* **Label:** occurs at
* **IRI:** `medorah:occursAt`
* **Domain:** `Event`
* **Range:** `SpatialEntity`
* **Definition:**
  The event takes place at a particular location.



---

### 5.8 `Event → Temporal`: `occursDuring`

#### 5.8.1 `occursDuring`

* **Label:** occurs during
* **IRI:** `medorah:occursDuring`
* **Domain:** `Event`
* **Range:** `TemporalEntity`
* **Definition:**
  The event takes place within a temporal interval.



---

### 5.9 `Actor → Spatial`: `hasResidence`

#### 5.9.1 `hasResidence`

* **Label:** has residence
* **IRI:** `medorah:hasResidence`
* **Domain:** `Actor` (typically `Person`)
* **Range:** `SpatialEntity`
* **Definition:**
  A location associated with an actor’s residence or long-term presence.



---

### 5.10 `Item → Item`: `dependency`

#### 5.10.1 `dependency`

* **Label:** dependency
* **IRI:** `medorah:dependency`
* **Domain:** `Item`
* **Range:** `Item`
* **Definition:**
  A generic dependency relationship between items.

**Sub-properties:**

| Property   | Domain     | Range    | Informal meaning                            |
| ---------- | ---------- | -------- | ------------------------------------------- |
| `isPartOf` | `Item`     | `Item`   | Item is a constituent part of a larger item |
| `runsOn`   | `Software` | `Device` | Software runs on a given device or platform |



---

### 5.11 `Entity → Entity`: `influences`

#### 5.11.1 `influences`

* **Label:** influences
* **IRI:** `medorah:influences`
* **Domain:** `Entity`
* **Range:** `Entity`
* **Definition:**
  One entity is described as influencing another in the narrative sources.

**Sub-properties:**

| Property                 | Domain           | Range            | Informal meaning                                       |
| ------------------------ | ---------------- | ---------------- | ------------------------------------------------------ |
| `conceptuallyInfluences` | `ConceptualItem` | `ConceptualItem` | One concept/method/theory is said to influence another |
| `personalInfluences`     | `Actor`          | `Actor`          | One actor is said to influence another                 |

* **Notes:**

  * Influence relations are interpretive and should be supported by **narrative evidence and provenance**.
  * They do not claim objective causal certainty; they capture **how influence is described** by interviewees or sources.

  

---

## Datatype Properties

### 6.1 `hasAttribute`

* **Label:** has attribute
* **IRI:** `medorah:hasAttribute`
* **Domain:** `Entity`
* **Range:** `rdfs:Literal`
* **Definition:**
  Captures literal attributes such as labels, descriptions, identifiers, codes, or notes that do not warrant modelling as separate entities.
* **Implementation notes:**

  * In practice, standard vocabularies such as `rdfs:label`, `rdfs:comment`, `skos:prefLabel`, etc., will also be used.
  * `hasAttribute` can be used as a **catch-all** in the prototype and later refined into more specific datatype properties if needed.

---



## Alignment and Interoperability

The ontology is intended to be interoperable with broader semantic web standards. While no formal alignment is yet committed, the following high-level correspondences are envisaged:

* `Person` ↔ `foaf:Person`, `schema:Person`, `cidoc:E21 Person`
* `Organisation` ↔ `foaf:Organization`, `schema:Organization`, `cidoc:E74 Group`
* `Event` ↔ `cidoc:E5 Event`
* `InformationItem` / `Publication` ↔ FRBRoo/IFLA LRM concepts and `cidoc:E89 Propositional Object`
* `SpatialEntity` ↔ `cidoc:E53 Place`
* `TemporalEntity` ↔ `cidoc:E52 Time-Span`

Alignment will be driven by:

* Requirements of the FAIR data portal

* The need to integrate with external data sources (archives, authority files, etc.)

  

---

## Competency Questions (v0.1)

v0.1 is designed to provide the foundational data for the project’s research questions.

### About the Domain of Digital Humanities

* “Which **Persons** and **Organisations** are mentioned as key actors in the formation of DH?”
* “Show the network of all **Persons** connected by `collaboratesWith` or `isColleagueOf`.”
* “Which **Persons** are associated with which **Organisations** (via `founds` or `hasEmploymentAt`)?”
* “Which **ConceptualItems** (Methods, Technologies) are `appliesConceptualItem` by which **Persons**?”
* “How are **Projects** and **Organisations** layered over **SpatialEntities** (places) and **TemporalEntities** (times)?”

### Network & Semantic Analysis

* “What is the complete inventory of **Persons**, **Organisations**, and **Projects** from the interview?”
* “Generate a graph of all **Actors** and **Events** to analyse network structure.”
* “Which **Persons** express any `hasViewAbout` (e.g. `holdsBeliefAbout`, `expressesEmotionAbout`) an **Entity**?”



---

## Implementation Notes

The ontology will be used to:

* Guide information extraction from interview transcripts and related sources using LLM-based and traditional NLP pipelines.
* Populate an RDF Knowledge Graph stored in a triple store, supporting SPARQL and potentially natural language querying.
* Support network analysis by providing a clear set of node and edge types consistent with the ontology.

**Pipeline-level design considerations (beyond the ontology itself):**

* Segment transcripts into narrative units.
* Extract entities and relations consistent with the class and property definitions.
* Attach provenance (source interview, segment, quote) and confidence scores.
* Enable both automated and human-curated corrections and enrichments.



---

## Versioning, Maintenance, and Roadmap

### Versioning

**Current version:** 0.1 (prototype, internal to MeDoraH)

Future versions will:

* Refine class and property definitions.
* Incorporate feedback from domain experts and evidence from data-driven discovery.
* Introduce the v0.2 Narrative Layer and additional alignment with external standards.

### Maintenance

The ontology is curated by the MeDoraH team.

Changes are expected to be:

* Recorded in a change log.
* Discussed in project meetings.
* Aligned with data modelling and extraction needs.
