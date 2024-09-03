# MeDoraH Ontology and Schema Repository
Welcome to the MeDoraH (Mixed-methods Digital Oral History) Ontology and Schema Repository. This repository houses the evolving ontology and schema definitions for the MeDoraH project, which aims to integrate semantic web technologies with historical-interpretative analysis in oral history research.

Our ontology provides a comprehensive framework for representing oral history interviews, their metadata, and associated analytical data. It is designed to support advanced content analysis, facilitate interdisciplinary research in digital humanities, and adhere to FAIR (Findable, Accessible, Interoperable, Reusable) data principles.
## Goals
**File Management**: Develop file schemas that creates a digital library/repository with a goal of information dissemination this include effectively capture technical metadata, provenance information, and 
relationships between different file types (e.g., audio recordings, transcripts).

**Content Modelling**: Create detailed content models that accurately represent the structure, semantics, and relationships within oral history narratives, enabling sophisticated network analysis and interpretation.

**FAIR Compliance**: Implement features in the schemas that support the FAIR data principles, enhancing the findability, accessibility, interoperability, and reusability of oral history data.

**Semantic Enrichment**: Enable the representation of complex relationships between different elements of oral history data, supporting advanced querying and knowledge discovery.


## Repository Structure
- `/ontology`: Contains the core ontology files in various formats (e.g., .ttl, .owl)
- `/documentation`: Holds detailed documentation, literature review, usage guides, and examples
- `/extensions`: Houses useful resources for ontology mapping and alignment
- `/tools`: Contains scripts and tools for working with the ontology and schemas


## Practice of incorporating FAIR standards:
Findable:
- Persistent identifiers (PIDs) are used for all main entities (Interview, Interviewer, Interviewee, Project, Collection).
- Implement rich metadata descriptions using properties from established vocabularies (e.g., Dublin Core, FOAF).

Accessible:
- Include clear access rights information for each interview and collection.
- [ ] Provide API access to the metadata and data where possible.

Interoperable:
- Use established ontologies and vocabularies where possible (e.g., FOAF for person descriptions, Dublin Core for general metadata).
- Align our custom classes and properties with existing standards where applicable.

Reusable:
- Provide clear provenance information for each interview and associated files.
- Include detailed metadata about the interview process, participants, and content.