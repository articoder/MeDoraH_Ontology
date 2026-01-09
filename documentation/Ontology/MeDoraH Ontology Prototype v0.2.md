# MeDoraH Ontology Prototype v0.2

MeDoraH Ontology for Narratives of Digital Humanities
**Version:** 0.2 (Prototype for Claim Layer & Reference Layer)
**Status:** Research Prototype

------

## 1. Introduction and Scope

The MeDoraH project investigates how semantic web technologies and digital methods can support the analysis of oral history interviews about the formation, disruption, and change of Digital Humanities (DH). Interviews (and related sources) are used to study:

- Individual and collective agency
- Knowledge creation, mobility, and loss
- Spatial, institutional, and disciplinary dynamics
- Changing recollections and accounts over time, across different sources and perspectives

This ontology prototype provides a conceptual schema for:

- Modelling entities mentioned in oral history sources (e.g., people, organisations, groups, projects, conferences, methods, technologies, works, places, times)
- Expressing relations between them (e.g., socio-institutional relations, creation, use, influence, part–whole structure, spatial/temporal anchoring)
- Supporting network analysis of “networks that emerge from oral history accounts” rather than assuming pre-defined external social networks

The ontology is designed to:

- Serve as the **core schema for a Knowledge Graph (KG)** storing structured data extracted from interviews and related sources
- Support mixed-methods analysis combining qualitative interpretation with network and text analysis
- Remain lightweight and interpretable for domain experts while remaining compatible with semantic-web practice (RDF/OWL, SPARQL, alignment-ready design)

### 1.1 Purpose of v0.2

This document describes the **second iteration of the entity-centric “Fabula / Reference layer”**: the layer modelling “what interviewees talk about” (entities, events, artefacts, concepts) rather than “how it is told” (narrative/discourse structure, stance, epistemic modality).

Compared to v0.1 , v0.2:

- Refines the **class hierarchy** into a clearer separation between:
  - **Artefacts** (things made/used, e.g. software, datasets, publications)
  - **Conceptual Items** (ideas for knowledge-making, e.g. theories, methods, disciplines)
- Refines the **Event taxonomy** to better represent DH-relevant activity types (projects, courses/programmes, conferences, event series, activities)
- Consolidates relations into a small set of **top-level relation patterns** (Actor–Actor, Actor–Artefact, Actor–ConceptualItem, Actor–Event, etc.) that can be specialised, but remain parsimonious and extraction-friendly

------

## 2. Design Principles and Modelling Approach

### 2.1 Conceptual Focus: Networks of Recollection

The KG is intended to store and analyse **connections as they are recalled and articulated in sources**, rather than asserting objective historical truth by default. In practice:

- Relations are interpreted as **claims grounded in sources** (interview segments, other texts), with provenance and confidence handled at the pipeline/KG layer (e.g., RDF-star reification or statement nodes).
- Conflicting accounts can coexist without forcing resolution; “truth maintenance” is a research activity, not an ontology requirement.

> v0.2 therefore focuses on **stable reference anchors** (entities/events/artefacts/concepts) and **reusable relation patterns**.

### 2.2 Top-Level Categories

The ontology adopts a small set of top-level categories that are meaningful for both humanists and technologists:

| Top-level class  | Informal meaning                                      | Typical examples                             |
| ---------------- | ----------------------------------------------------- | -------------------------------------------- |
| `Actor`          | Agents capable of intentional action or participation | persons, organisations, groups               |
| `Event`          | Things that happen over time                          | projects, conferences, courses               |
| `Artefact`       | Created and used outputs/resources/technologies       | software, datasets, publications             |
| `ConceptualItem` | Knowledge-making ideas and intellectual constructs    | methods, theories, disciplines               |
| `SpatialEntity`  | Places                                                | cities, countries, institutions-as-locations |
| `TemporalEntity` | Times/intervals                                       | year, decade, period                         |
| `Property`       | Analytic classification or credential                 | role/position, qualification                 |

### 2.3 Relation Patterns

The ontology is structured around a small number of **top-level relation patterns**, each with specialisations.

| Pattern                        | Informal description                               |
| ------------------------------ | -------------------------------------------------- |
| `Actor → Actor`                | socio-institutional and interpersonal relations    |
| `Actor → Artefact`             | creating and using artefacts/works/technologies    |
| `Actor → ConceptualItem`       | engagement with disciplines/methods/definitions    |
| `Actor → Event`                | participation, organisation, presentation, funding |
| `Event → Spatial/Organisation` | where events take place                            |
| `Event → Temporal`             | time extent of events                              |
| `Entity → Entity`              | dependency/part–whole/influence/run-on relations   |
| `Artefact → ConceptualItem`    | aboutness / implementation relations               |
| `Actor → Property`             | roles/positions/qualifications                     |
| `Actor → SpatialEntity`        | residence, work location, organisation location    |

### 2.4 Practical Modelling Notes

**A. Parsimony over proliferation**
Specialise a relation only if it changes domain/range or has clearly different semantics.

**B. Avoid “union domain/range” pitfalls in RDFS**
Your design includes patterns like `Actor|Project → uses → Artefact` and `Event → takesPlaceAt → Spatial|Organisation`. In strict RDFS, multiple `rdfs:domain` or `rdfs:range` statements imply intersection (not union). In this prototype document, we treat these as **intended constraints** and recommend one of these implementation strategies:

1. Use **OWL unionOf** for domain/range, or
2. Set domain/range to a broader class (e.g. `Entity`) and constrain in SHACL, or
3. Introduce a helper superclass (e.g. `Location`) if you want purely RDFS constraints.

v0.2 documents the intended constraints and flags where implementers should decide.

------

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

### 3.2 Informal Class Hierarchy (v0.2)

**Top level**

- `Entity`
  - `Actor`
    - `Person`
    - `Organisation`
    - `Group` (loose groups, committees, informal networks)
  - `Event`
    - `Project`
    - `CourseAndProgramme`
    - `Conference`
    - `EventSeries`
    - `Activity`
  - `Artefact`
    - `Technology`
      - `Software`
      - `Hardware`
      - `Standard`
      - `Infrastructure`
    - `Work`
      - `InformationResource`
      - `Publication`
      - `Corpus`
      - `Database`
      - `Dataset`
      - `Website`
  - `ConceptualItem`
    - `ConceptualFramework`
      - `Theory`
      - `Paradigm`
      - `SchoolOfThought`
      - `Definition`
    - `Methodology`
      - `Method`
      - `Practice`
      - `Technique`
    - `Discipline`
      - `AcademicDiscipline`
      - `FieldOfStudy`
      - `ResearchArea`
  - `SpatialEntity` (Place)
  - `TemporalEntity` (Time)
  - `Property`
    - `RoleOrPosition`
    - `Qualification`

------

## 4. Class Reference

This section defines each class with label, definition, and examples. Only key subclasses are expanded; further subclasses can follow the same pattern.

### 4.1 Core Superclass

#### 4.1.1 `Entity`

- **Label:** Entity
- **IRI:** `medorah:Entity`
- **Definition:**
  A thing that can be referred to in the narratives modelled in MeDoraH, including persons, organisations, groups, events, artefacts, concepts, places, times, and analytic properties.
- **Notes:**
  - Root of the main hierarchy.
  - Used as the domain or range of generic properties such as `medorah:isPartOf`.

------

### 4.2 Actor Module

| Class          | Subclass of | Short definition                                      |
| -------------- | ----------- | ----------------------------------------------------- |
| `Actor`        | `Entity`    | Entity capable of intentional action or participation |
| `Person`       | `Actor`     | Individual human agent/narrator/subject               |
| `Organisation` | `Actor`     | Formal institution or organisational entity           |
| `Group`        | `Actor`     | Informal or loosely bounded collective                |

#### 4.2.1 `Actor`

- **Definition:**
  An entity capable of intentional action or participation in events, as recalled in oral history and related sources.
- **Notes:**
  - Central to modelling agency and responsibility.
  - Includes both individuals and collective actors.

#### 4.2.2 `Person`

- **Definition:**
  An individual human being who appears as an agent, narrator, or subject in the sources.
- **Examples:**
  - An interviewee describing their role in founding a DH centre.
  - A collaborator mentioned as developing a tool or shaping a method.

#### 4.2.3 `Organisation`

- **Definition:**
  A formally recognised institution or organisational entity involved in DH-relevant activity (universities, departments, centres, archives, companies, etc.).
- **Examples:**
  - A university department hosting DH courses.
  - A research centre providing infrastructure or training.

#### 4.2.4 `Group`

- **Definition:**
  A loosely defined group, committee, informal network, or community that may not be fully institutionalised but is described as acting collectively.
- **Examples:**
  - An early “working group” or “committee” described in interviews.
  - A mailing list community described as an actor.

------

### 4.3 Event Module

| Class                | Subclass of | Short definition                                       |
| -------------------- | ----------- | ------------------------------------------------------ |
| `Event`              | `Entity`    | Temporal occurrence in which actors can participate    |
| `Project`            | `Event`     | Structured activity with goals and outputs             |
| `CourseAndProgramme` | `Event`     | Formal education/training activity (course, programme) |
| `Conference`         | `Event`     | Organised scholarly meeting/event                      |
| `EventSeries`        | `Event`     | A recurring series (conference series, seminar series) |
| `Activity`           | `Event`     | Bounded activity (meeting, workshop, training session) |

#### 4.3.1 `Event`

- **Definition:**
  A temporal occurrence or happening in which actors can participate, and which can be located in time and space.
- **Notes:**
  - Represents events as **recalled/mentioned**.
  - Fine-grained narrative modelling (how events are narrated, sequenced, evaluated) is handled in other layers, not in this Fabula layer.

#### 4.3.2 `Project`

- **Definition:**
  A planned, structured activity (often funded) with defined goals and outputs (e.g., corpora, tools, publications).
- **Examples:**
  - A grant-funded digitisation project.
  - A long-term infrastructure initiative.

#### 4.3.3 `CourseAndProgramme`

- **Definition:**
  A formal course, training programme, or educational curriculum relevant to DH.
- **Examples:**
  - A DH MA programme.
  - A short training course on TEI or text analysis.

#### 4.3.4 `Conference`

- **Definition:**
  A scholarly meeting or event where research is presented and community relations are formed.
- **Examples:**
  - An annual DH conference.
  - A workshop-style conference meeting.

#### 4.3.5 `EventSeries`

- **Definition:**
  A recurring, named series of events (conference series, lecture series, seminar series).
- **Examples:**
  - A recurring annual conference series.
  - A seminar series run by a centre.
- **Modelling note:**
  - Individual instances (specific year) can be `Conference` or `Activity` and linked via `medorah:isPartOf` to the `EventSeries`.

#### 4.3.6 `Activity`

- **Definition:**
  A bounded event characterised by actors performing actions, typically shorter and more localised than a project.
- **Examples:**
  - A workshop.
  - A meeting, training session, or code sprint.

------

### 4.4 Artefact Module

> v0.2 distinguishes between **Artefacts** (things made/used) and **Conceptual Items** (ideas). This is the most important structural change from v0.1 .

| Class        | Subclass of | Short definition                                             |
| ------------ | ----------- | ------------------------------------------------------------ |
| `Artefact`   | `Entity`    | Created/used artefact (technology, work, resource)           |
| `Technology` | `Artefact`  | Technical artefact enabling practice                         |
| `Work`       | `Artefact`  | Information work/resource (publication, dataset, corpus, etc.) |

#### 4.4.1 `Artefact`

- **Definition:**
  Anything that can be created, used, or depended on in DH practice, including technologies and works/resources.

------

#### 4.4.2 `Technology`

- **Definition:**
  A technical artefact used to enable or perform DH practice, including software, hardware, standards, and infrastructure.
- **Key subclasses:**

| Class            | Short definition                        | Examples                                                     |
| ---------------- | --------------------------------------- | ------------------------------------------------------------ |
| `Software`       | Executable programs, scripts, platforms | a DH tool, TEI editor                                        |
| `Hardware`       | Physical computing equipment            | servers, scanners                                            |
| `Standard`       | Formal standards/specifications         | TEI Guidelines as a standard (if treated as such), XML standard |
| `Infrastructure` | Socio-technical infrastructure          | repository platform, compute infrastructure                  |

> Modelling note: Some things (e.g. TEI) can be treated as **Standard** (artefact) and also discussed as a **ConceptualItem** (conceptual framework/definition). In the Fabula layer, choose the representation that matches the usage in a claim (or link the two via `medorah:implementsConcept` or `medorah:about`).

------

#### 4.4.3 `Work`

- **Definition:**
  An informational resource or output that can be authored, published, curated, used, cited, or integrated.
- **Key subclasses:**

| Class                 | Short definition                                  | Examples                       |
| --------------------- | ------------------------------------------------- | ------------------------------ |
| `InformationResource` | Generic information resource                      | documentation, reports         |
| `Publication`         | Formally disseminated scholarly/professional work | article, book, report          |
| `Corpus`              | Curated collection of texts/records               | email corpus, interview corpus |
| `Database`            | Structured data store / curated DB                | institutional DB               |
| `Dataset`             | Structured data package                           | annotations dataset            |
| `Website`             | Web-based resource/presence                       | project website                |

------

### 4.5 Conceptual Item Module

| Class                 | Subclass of      | Short definition                                        |
| --------------------- | ---------------- | ------------------------------------------------------- |
| `ConceptualItem`      | `Entity`         | Immaterial construct used to create/structure knowledge |
| `ConceptualFramework` | `ConceptualItem` | Theories, paradigms, schools, definitions               |
| `Methodology`         | `ConceptualItem` | Methods/practices/techniques                            |
| `Discipline`          | `ConceptualItem` | Disciplines, fields of study, research areas            |

#### 4.5.1 `ConceptualItem`

- **Definition:**
  An immaterial construct used to organise, interpret, or generate knowledge, such as theories, methods, and disciplines.
- **Examples:**
  - “Digital Humanities” as a field/research area.
  - “Text encoding” as a method/technique.
  - A definition coined by a scholar.

------

#### 4.5.2 `ConceptualFramework`

- **Definition:**
  A conceptual apparatus (theory, paradigm, school of thought, definition) used to interpret or frame knowledge and practice.
- **Subclasses:**
  - `Theory`
  - `Paradigm`
  - `SchoolOfThought`
  - `Definition`

**`Definition` note:**
A `Definition` is treated as a conceptual object that can be coined or stabilised by actors (e.g. defining “Digital Humanities” or a technical term).

------

#### 4.5.3 `Methodology`

- **Definition:**
  A structured approach to knowledge-making.
- **Subclasses:**
  - `Method` (a method, procedure, or named approach)
  - `Practice` (a practice that may be more situated/institutional)
  - `Technique` (a specific technique, often more operational)

------

#### 4.5.4 `Discipline`

- **Definition:**
  A disciplinary area or field of knowledge.
- **Subclasses:**
  - `AcademicDiscipline` (more institutionalised discipline)
  - `FieldOfStudy` (often used for educational contexts)
  - `ResearchArea` (often used for research contexts, potentially emerging)

------

### 4.6 Spatial and Temporal Module

#### 4.6.1 `SpatialEntity` (Place)

- **Definition:**
  A geographic or spatial location relevant to the narratives, including cities, regions, countries, or other places used to situate actors and events.
- **Examples:**
  - A city where a DH centre is located.
  - A country relevant to cross-national comparison.

> If you require a more granular administrative model later, introduce subclasses such as `AdministrativeArea` (needed by `grewUpIn` in Section 5.11).

#### 4.6.2 `TemporalEntity` (Time)

- **Definition:**
  A temporal expression or interval associated with events or other entities (year, decade, period, date range).
- **Examples:**
  - “1998”
  - “the 1990s”
  - “post-war period”

------

### 4.7 Property Module

| Class            | Subclass of | Short definition                                        |
| ---------------- | ----------- | ------------------------------------------------------- |
| `Property`       | `Entity`    | Analytic classification / credential attached to actors |
| `RoleOrPosition` | `Property`  | Role, job title, institutional position                 |
| `Qualification`  | `Property`  | Degree, certification, prerequisite credential          |

#### 4.7.1 `Property`

- **Definition:**
  An analytic classification or credential used to classify actors (and, if needed later, other entities).
- **Modelling rationale:**
  - This class captures *our structured representation of roles/qualifications* which often appear in interview accounts (e.g., “I was a lecturer”, “she was trained as a linguist”, “he had a PhD in…”).

#### 4.7.2 `RoleOrPosition`

- **Definition:**
  A property describing social/professional roles and institutional positions.
- **Examples:**
  - Professor, Researcher, Archivist, Developer, Director.

#### 4.7.3 `Qualification`

- **Definition:**
  A property describing degrees, certifications, or other qualifications.
- **Examples:**
  - PhD, MA, certification programme.

------

## 5. Object Property Reference

This section describes top-level object properties and their sub-properties. Example triples use Turtle syntax.

### 5.1 `Actor → Actor`: `hasSocioInstitutionalRelationWith`

#### 5.1.1 `hasSocioInstitutionalRelationWith`

- **Label:** has socio-institutional relation with
- **IRI:** `medorah:hasSocioInstitutionalRelationWith`
- **Domain:** `medorah:Actor`
- **Range:** `medorah:Actor`
- **Definition:**
  A general socio-institutional relationship between two actors, to be specialised by sub-properties such as employment, study, collaboration, provision, representation, etc.

**Sub-properties (as specified in your v0.2 design):**

| Property              | Domain         | Range          | Informal meaning                           |
| --------------------- | -------------- | -------------- | ------------------------------------------ |
| `hasEmploymentAt`     | `Person`       | `Organisation` | Person employed by organisation            |
| `studiedAt`           | `Person`       | `Organisation` | Person studied at organisation             |
| `founded`             | `Person`       | `Organisation` | Person founded/established organisation    |
| `collaboratedWith`    | `Person`       | `Person`       | Persons collaborated/worked together       |
| `mentorsOrSupervises` | `Person`       | `Person`       | Mentoring or supervision relation          |
| `providesResource`    | `Actor`        | `Actor`        | Provision of resources/services/support    |
| `influences`          | `Person`       | `Person`       | Person influences another person           |
| `hasEducationIn`      | `Person`       | `Organisation` | Education context (broader than studiedAt) |
| `chairOf`             | `Person`       | `Organisation` | Person chairs organisation/committee       |
| `represents`          | `Person`       | `Organisation` | Person represents organisation             |
| `affiliatedWith`      | `Person`       | `Organisation` | Person affiliated with organisation        |
| `mergedWith`          | `Organisation` | `Organisation` | Organisations merged                       |

**Modelling notes:**

- `collaboratedWith` can be declared symmetric in OWL.
- `mergedWith` is typically symmetric, but you may later introduce `acquiredBy` if you need directionality.
- `studiedAt` vs `hasEducationIn`: if both are kept, define a crisp distinction (e.g., “formal enrolment” vs “training/education context”), otherwise consider making one a subproperty of the other.

**Example:**

```turtle
:alice a medorah:Person ;
  medorah:hasEmploymentAt :ucl ;
  medorah:collaboratedWith :bob ;
  medorah:affiliatedWith :cdh_ucl .

:ucl a medorah:Organisation .
:cdh_ucl a medorah:Organisation .
```

------

### 5.2 `Actor → Artefact`: `createsItem` (inverse `createdBy`)

#### 5.2.1 `createsItem`

- **Label:** creates item
- **IRI:** `medorah:createsItem`
- **Domain:** `medorah:Actor`
- **Range:** `medorah:Artefact`
- **Inverse:** `medorah:createdBy`
- **Definition:**
  The actor is responsible for creating or bringing into existence an artefact (technology or work).

**Sub-properties:**

| Property          | Domain  | Range        | Informal meaning            |
| ----------------- | ------- | ------------ | --------------------------- |
| `authorsWork`     | `Actor` | `Work`       | Actor authors a work        |
| `publishesWork`   | `Actor` | `Work`       | Actor publishes a work      |
| `createsArtefact` | `Actor` | `Artefact`   | Generic artefact creation   |
| `developsTech`    | `Actor` | `Technology` | Actor develops a technology |

**Example:**

```turtle
:alice medorah:authorsWork :paper_X .
:lab_Y medorah:developsTech :tool_Z .

:paper_X a medorah:Publication .
:tool_Z a medorah:Software .
```

------

### 5.3 `Actor|Project → Artefact`: `uses` (inverse `usedBy`)

#### 5.3.1 `uses`

- **Label:** uses
- **IRI:** `medorah:uses`
- **Intended domain:** `medorah:Actor` or `medorah:Project`
- **Range:** `medorah:Artefact`
- **Inverse:** `medorah:usedBy`
- **Definition:**
  The actor (or project) uses or employs an artefact in practice.

**Implementation note (domain constraint):**
To avoid RDFS intersection semantics, a common approach is:

- set **domain = `Entity`** (or omit domain),
- constrain with **SHACL** or OWL unionOf,
- and keep intended usage in documentation.

**Sub-properties:**

| Property               | Domain               | Range        | Informal meaning            |
| ---------------------- | -------------------- | ------------ | --------------------------- |
| `usesTechnology`       | `Actor` or `Project` | `Technology` | Uses a technology           |
| `usesCorpusOrResource` | `Person`             | `Work`       | Uses a corpus/resource/work |

**Example:**

```turtle
:project_A a medorah:Project ;
  medorah:usesTechnology :tei_publisher .

:bob a medorah:Person ;
  medorah:usesCorpusOrResource :humanist_corpus .

:tei_publisher a medorah:Software .
:humanist_corpus a medorah:Corpus .
```

------

### 5.4 `Actor → ConceptualItem`: `engagesWithConcept`

#### 5.4.1 `engagesWithConcept`

- **Label:** engages with concept
- **IRI:** `medorah:engagesWithConcept`
- **Domain:** `medorah:Actor`
- **Range:** `medorah:ConceptualItem`
- **Definition:**
  Actor engages with conceptual items (disciplines, methods, conceptual frameworks) through working, studying, supporting, developing, or defining.

**Sub-properties:**

| Property             | Domain   | Range        | Informal meaning                               |
| -------------------- | -------- | ------------ | ---------------------------------------------- |
| `workInField`        | `Actor`  | `Discipline` | Worked in / taught in / supported a discipline |
| `studiesField`       | `Actor`  | `Discipline` | Studied in a discipline                        |
| `coinsOrDefinesTerm` | `Person` | `Definition` | Person coins or defines a term/definition      |

**Example:**

```turtle
:alice medorah:workInField :digital_humanities .
:alice medorah:coinsOrDefinesTerm :definition_DH_1999 .

:digital_humanities a medorah:ResearchArea .
:definition_DH_1999 a medorah:Definition .
```

------

### 5.5 `Actor → Event`: `engagesIn` (inverse `isEngagedInBy`)

#### 5.5.1 `engagesIn`

- **Label:** engages in
- **IRI:** `medorah:engagesIn`
- **Domain:** `medorah:Actor`
- **Range:** `medorah:Event`
- **Inverse:** `medorah:isEngagedInBy`
- **Definition:**
  Actor is involved in an event (participation, organisation, presenting, or funding).

**Sub-properties:**

| Property         | Domain  | Range   | Informal meaning                       |
| ---------------- | ------- | ------- | -------------------------------------- |
| `participatesIn` | `Actor` | `Event` | Attends/participates/receives training |
| `organises`      | `Actor` | `Event` | Organises or provides an event         |
| `presentedAt`    | `Actor` | `Event` | Presents talk/work at event            |
| `funds`          | `Actor` | `Event` | Funds an event                         |

**Example:**

```turtle
:ucl medorah:organises :course_DH_101 .
:bob medorah:participatesIn :course_DH_101 .
:alice medorah:presentedAt :conf_DH_2005 .
:funding_body medorah:funds :project_A .
```

------

### 5.6 `Actor → Property`: `hasProperty`

#### 5.6.1 `hasProperty`

- **Label:** has property
- **IRI:** `medorah:hasProperty`
- **Domain:** `medorah:Actor`
- **Range:** `medorah:Property`
- **Inverse:** `medorah:isPropertyOf`
- **Definition:**
  Associates an actor with analytic properties such as roles/positions and qualifications.

**Sub-properties:**

| Property            | Domain  | Range            | Informal meaning            |
| ------------------- | ------- | ---------------- | --------------------------- |
| `hasRoleOrPosition` | `Actor` | `RoleOrPosition` | Actor holds a role/position |

> Recommended addition (consistent with your class design):
> `hasQualification` (Actor → Qualification). If you prefer to keep only one explicit subproperty for now, you can still link qualifications via the generic `hasProperty`.

**Example:**

```turtle
:alice medorah:hasRoleOrPosition :role_professor .
:bob medorah:hasProperty :qualification_phd .

:role_professor a medorah:RoleOrPosition .
:qualification_phd a medorah:Qualification .
```

------

### 5.7 `Event → Spatial|Organisation`: `takesPlaceAt`

#### 5.7.1 `takesPlaceAt`

- **Label:** takes place at
- **IRI:** `medorah:takesPlaceAt`
- **Domain:** `medorah:Event`
- **Intended range:** `medorah:SpatialEntity` or `medorah:Organisation`
- **Definition:**
  Links an event to its location, expressed either as a place or as an organisation-as-venue.

**Implementation note:**
If you want strict typing without union-range complexity, you can:

- define `takesPlaceAt` range `SpatialEntity` only, and
- represent organisation venues via `Organisation locatedIn Place`, and/or a specialised `takesPlaceAtOrganisation` property.

**Example:**

```turtle
:conf_DH_2005 medorah:takesPlaceAt :paris .
:workshop_X medorah:takesPlaceAt :ucl .

:paris a medorah:SpatialEntity .
:ucl a medorah:Organisation .
```

------

### 5.8 `Event → Temporal`: `hasTimeExtent`

#### 5.8.1 `hasTimeExtent`

- **Label:** has time extent
- **IRI:** `medorah:hasTimeExtent`
- **Domain:** `medorah:Event`
- **Range:** `medorah:TemporalEntity`
- **Definition:**
  Links an event to the time interval/date/period during which it occurs.

**Example:**

```turtle
:project_A medorah:hasTimeExtent :time_1999_2002 .
:time_1999_2002 a medorah:TemporalEntity .
```

------

### 5.9 `Entity → Entity`: `dependency`

#### 5.9.1 `dependency`

- **Label:** dependency
- **IRI:** `medorah:dependency`
- **Domain:** `medorah:Entity`
- **Range:** `medorah:Entity`
- **Definition:**
  A generic dependency relationship between entities, including part–whole, conceptual influence, and software–hardware relations.

**Sub-properties:**

| Property                 | Domain           | Range            | Informal meaning                  |
| ------------------------ | ---------------- | ---------------- | --------------------------------- |
| `isPartOf`               | `Entity`         | `Entity`         | Entity is part of a larger entity |
| `conceptuallyInfluences` | `ConceptualItem` | `ConceptualItem` | One concept influences another    |
| `runsOn`                 | `Software`       | `Hardware`       | Software runs on hardware         |

**Example:**

```turtle
:conf_DH_2005 medorah:isPartOf :conf_series_DH .
:topic_modelling medorah:conceptuallyInfluences :distant_reading .
:tool_Z medorah:runsOn :server_A .
```

------

### 5.10 `Artefact → ConceptualItem`: `about`

#### 5.10.1 `about`

- **Label:** about
- **IRI:** `medorah:about`
- **Domain:** `medorah:Artefact`
- **Range:** `medorah:ConceptualItem`
- **Definition:**
  Connects artefacts (works/technologies) to conceptual items they are about, implement, or operationalise.

**Sub-properties:**

| Property            | Domain     | Range            | Informal meaning                               |
| ------------------- | ---------- | ---------------- | ---------------------------------------------- |
| `hasTopic`          | `Work`     | `Discipline`     | Work is about a discipline/field/topic         |
| `implementsConcept` | `Artefact` | `ConceptualItem` | Artefact implements a concept/method/framework |

**Example:**

```turtle
:paper_X medorah:hasTopic :digital_humanities .
:tool_Z medorah:implementsConcept :topic_modelling .
```

------

### 5.11 `Actor → SpatialEntity`: `hasResidence`

#### 5.11.1 `hasResidence`

- **Label:** has residence
- **IRI:** `medorah:hasResidence`
- **Domain:** `medorah:Actor`
- **Range:** `medorah:SpatialEntity`
- **Definition:**
  Associates an actor with locations of residence, upbringing, work, or organisational location.

**Sub-properties:**

| Property    | Domain         | Range                                        | Informal meaning              |
| ----------- | -------------- | -------------------------------------------- | ----------------------------- |
| `residesIn` | `Person`       | `SpatialEntity`                              | Person resides in place       |
| `grewUpIn`  | `Person`       | `SpatialEntity` (often `AdministrativeArea`) | Person grew up in area        |
| `workedIn`  | `Person`       | `SpatialEntity`                              | Person worked in place        |
| `locatedIn` | `Organisation` | `SpatialEntity`                              | Organisation located in place |

**Example:**

```turtle
:alice medorah:residesIn :london .
:alice medorah:workedIn :paris .
:ucl medorah:locatedIn :london .
```

------

## 6. Datatype Properties

v0.2 remains conservative about datatype properties and relies on standard RDF vocabularies where possible:

- `rdfs:label` for preferred labels
- `rdfs:comment` for definitions/notes
- `skos:prefLabel` / `skos:altLabel` for label management (optional)
- External identifiers (ORCID, VIAF, ROR, DOI, etc.) can be stored using `dcterms:identifier`, `schema:identifier`, or a project-specific `medorah:hasIdentifier`.

### 6.1 `hasAttribute` (optional catch-all)

- **Label:** has attribute
- **IRI:** `medorah:hasAttribute`
- **Domain:** `medorah:Entity`
- **Range:** `rdfs:Literal`
- **Definition:**
  Captures literal attributes (notes, codes, minimal descriptions) that do not warrant separate entities.

------

## 7. Alignment and Interoperability

The ontology is intended to be alignment-ready with common semantic web standards. No formal alignment is committed in v0.2, but plausible correspondences include:

- `Person` ↔ `foaf:Person`, `schema:Person`, `cidoc:E21 Person`
- `Organisation` ↔ `foaf:Organization`, `schema:Organization`, `cidoc:E74 Group`
- `Event` ↔ `cidoc:E5 Event`
- `SpatialEntity` ↔ `cidoc:E53 Place`
- `TemporalEntity` ↔ `cidoc:E52 Time-Span`
- `Publication` / `Work` ↔ `schema:CreativeWork`, `dcterms:BibliographicResource`, FRBRoo/IFLA-LRM inspired patterns (if adopted later)

Alignment decisions should be driven by:

- FAIR portal interoperability requirements
- Integration with external authority files and catalogues
- Practical querying and user interface needs

------

## 8. Competency Questions (v0.2)

v0.2 is designed to support foundational queries for agency, institutionalisation, mobility, and knowledge-making in recalled narratives.

### Actors, Institutions, and Groups

- Which **Persons** are mentioned as key actors in the formation of DH?
- Which **Groups** are mentioned (committees, informal networks), and which persons/organisations are connected to them?
- Which **Organisations** employ, affiliate, or are chaired by which persons (`hasEmploymentAt`, `affiliatedWith`, `chairOf`)?
- Which organisations are said to have **merged** (`mergedWith`)?

### Projects, Conferences, and Training

- Which **Projects** are funded by which actors (`funds`)?
- Which **Conferences** are part of which **EventSeries** (`isPartOf`)?
- Which **CoursesAndProgrammes** are organised by which organisations (`organises`) and attended by which persons (`participatesIn`)?

### Technologies and Works

- Which persons or organisations **developed technologies** (`developsTech`)?
- Which projects or actors **use** particular technologies (`usesTechnology`)?
- Which persons **use** corpora/resources (`usesCorpusOrResource`)?

### Concepts, Methods, and Disciplines

- Which actors **work in** which disciplines (`workInField`)?
- Which persons are said to have **defined or coined** important definitions (`coinsOrDefinesTerm`)?
- Which technologies or works **implement** or are **about** specific methods/frameworks (`implementsConcept`, `about`)?

### Spatial and Temporal Anchoring

- Where did key events take place (`takesPlaceAt`), and when (`hasTimeExtent`)?
- Which actors’ biographies involve cross-place mobility (`workedIn`, `residesIn`, `grewUpIn`)?

------

## 9. Implementation Notes

### 9.1 KG Population and Provenance

Although v0.2 defines entity and relation types, MeDoraH’s oral-history epistemology requires that extracted assertions retain provenance and uncertainty:

- Each extracted relation should be associated with:
  - source (interview, transcript, segment ID)
  - evidence span (quote or offset)
  - extractor metadata (method/model/prompt version)
  - confidence/validation status (automatic + human review)

This can be implemented via:

- RDF-star (statement annotations)
- or reified statement nodes (Claim layer), leaving v0.2 as the anchor schema

### 9.2 Extraction-Friendliness

The v0.2 relation set is designed so that extraction can:

- detect entities with lightweight typing (Person/Organisation/Project/Technology/etc.)
- map raw predicates to a controlled inventory of sub-properties under the 11 top-level patterns
- progressively specialise predicates as evidence accumulates (e.g., start with `hasSocioInstitutionalRelationWith`, later refine to `studiedAt`)

------

## 10. Versioning, Maintenance, and Roadmap

### 10.1 Versioning

**Current version:** 0.2 (prototype, internal to MeDoraH)
Future versions are expected to:

- refine definitions and constraints based on corpus evidence
- formalise SHACL constraints (domain/range, cardinalities where appropriate)
- incorporate richer modelling for narrative, stance, and intersubjectivity in adjacent layers (not in this Fabula layer)

### 10.2 Change Log (v0.1 → v0.2)

Relative to v0.1 , the most important changes are:

1. **Class refactor**

- `Item` has been replaced by a clearer distinction between:
  - `Artefact` (Technology + Work)
  - `ConceptualItem` (Framework + Methodology + Discipline)

1. **Event taxonomy refined**

- Introduced explicit subclasses: `Project`, `CourseAndProgramme`, `Conference`, `EventSeries`, `Activity`

1. **Actor taxonomy refined**

- `Collective` becomes `Group` (explicitly scoped to loose groups, committees, informal networks)

1. **Relation inventory reorganised**

- Consolidated into 11 top-level relation patterns with explicit sub-properties (including newly emphasised ones such as `providesResource`, `funds`, and `mergedWith`)

### 10.3 Open Modelling Questions (recommended to track)

To keep the prototype robust and publication-grade, the following are worth tracking explicitly:

- **StudiedAt vs HasEducationIn:** do you need both? If yes, define a strict distinction.
- **Event location as Organisation:** decide whether this is a convenience shortcut or a first-class modelling choice.
- **Influence relations:** `Person influences Person` and `ConceptualItem conceptuallyInfluences ConceptualItem` are distinct; ensure extraction prompts don’t conflate them.
- **Definition modelling:** if `Definition` instances are important (e.g. multiple competing definitions over time), consider adding optional date/provenance or linking definitions to works where they are published.

