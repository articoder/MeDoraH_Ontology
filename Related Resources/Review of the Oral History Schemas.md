
## PBCore (Public Broadcasting Core)
* **Descriptive Metadata**: Captures information about the content, such as title, creator, and subject.
* **Administrative Metadata**: Includes details about the creation, management, and rights of the content.
* **Technical Metadata**: Describes the technical aspects of the audiovisual files, such as format and duration.
* **Structural Metadata**: Provides information about the structure of the content, including relationships between different segments or versions.
Use Cases:
* Archiving and cataloging audiovisual content.
* Facilitating data sharing between organisations.
* Enhancing search and retrieval of audiovisual records.

## EAD (Encoded Archival Description)
* **Hierarchical Structure**: EAD allows for a multi-level description of collections, from the collection level down to individual items.
* **XML-Based**: XML for encoding, making it machine-readable and interoperable with other systems.
* **Compatibility**: Can be mapped to other standards such as DACS (Describing Archives: A Content Standard) and ISAD(G) (General International Standard Archival Description).
Use Cases:
* Creating digital finding aids for archival collections.
* Facilitating access to and discovery of archival materials.
* Enhancing interoperability and data exchange between archival repositories.

## OAI (Open Archives Initiative)
* **Metadata Harvesting**: Enables the collection of metadata from various repositories into a centralized database.
* **Interoperability**: Promotes standards that ensure different systems can work together seamlessly.
* **ResourceSync**: A specification for synchronizing web resources, standardized as ANSI/NISO Z39.99-2017.
Use Cases:
* Aggregating metadata from multiple digital libraries.
* Enhancing the discoverability of digital resources.
* Supporting open access and institutional repositories.


## METS (Metadata Encoding and Transmission Standard)
* **Descriptive Metadata**: Information about the content, such as title and author.
* **Administrative Metadata**: Details about the creation, management, and rights of the digital objects.
* **Structural Metadata**: Information about the structure and relationships of the digital objects.
* **XML-Based**: Uses XML for encoding, ensuring interoperability and machine-readability.
⠀Use Cases:
* Packaging digital objects and their metadata for transmission.
* Archiving digital objects for long-term preservation.
* Facilitating the exchange of digital objects between repositories.

## TEI (Text Encoding Initiative)
* **Semantic Encoding**: Focuses on the semantic representation of texts rather than their presentation.
* **Customisation**: Allows for project-specific customisations using the ODD (One Document Does it all) mechanism.
* **Wide Adoption**: Used by libraries, museums, publishers, and scholars for online research, teaching, and preservation.
⠀Use Cases:
* Encoding literary and historical texts for digital humanities projects.
* Creating digital editions of manuscripts and archival materials.
* Facilitating text analysis and research in the humanities.

## EBUcore:
Provides useful classes like Rating, Publication history, Part (for segmentation), and Textline (for synchronising segments with transcription)
It also supports representation of events

Properties of Event:
* ebucore:eventName: The name of the event
* ebucore:eventDescription: A description of the event
* ebucore:eventStartDate and ebucore:eventEndDate: Temporal information
* ebucore:hasLocation: Links to a Location object
* ebucore:hasAgent: Links to Agent objects (persons or organizations involved)

⠀Event Relationships:
* ebucore:hasRelatedEvent: This property allows linking related events, but it doesn't specify the nature of the relationship (e.g., sequence, causality).

Others:
1. Editorial Object:
   * The core concept in EBUcore, representing any type of content.
   * Can be used to describe entire programs, parts of programs, or collections.
2. MediaResource:
   * Represents the actual media asset (audio, video, or multimedia).
   * Contains technical metadata about the resource.
3. Agent:
   * Describes people or organizations involved in the content creation or distribution.
   * Subtypes include Person, Organisation, and Group.
4. Location:
   * Describes places relevant to the content or its creation.
5. Concept:
   * Used for subject classification and thematic description of content.
6. Part:
   * Allows for the description of segments or parts of a media resource.
   * Crucial for describing specific sections of oral history interviews.
7. PublicationEvent:
   * Describes when and how the content was or will be published.
8. Rating:
   * Used for content classification, e.g., parental guidance ratings.
9. Rights:
   * Describes the rights associated with the content, including copyright and usage rights.
10. Format:
    * Describes the technical format of the media resource.



## OHMS
Key Features
* **Time-Coding Transcripts**: The application allows users to embed timecodes into transcripts, linking specific points in the text to corresponding moments in the audio or video recording.
* **Indexing Interviews**: Users can create an index of the interview, annotating key segments with metadata such as keywords, summaries, and subjects.
* **Workflow Management**: The Interview Manager module provides an overview of the progress of each interview, allowing multiple users to collaborate on different stages of the process. It includes status indicators like “in progress,” “ready for QC,” “active QC,” and “complete.”
* **XML Export**: Once the metadata creation and indexing are complete, the interview record can be exported as an XML file. This file interfaces with the OHMS Viewer and can be integrated into various content management systems (CMS).



## Metadata Object Description Schema (MODS)





https://www.loc.gov/standards/mods/userguide/generalapp.html