# File Schema

## Prefix and base URI

medorah: http://www.medorah.org/ontology#
## Classes
### medorah:Interview
- **Label**: Interview
- **Description**: Represents an oral history interview session, including metadata about the interview, participants, and associated files.
- **Properties**:
  - hasInterviewer (→ medorah:Interviewer)
  - hasInterviewee (→ medorah:Interviewee)
  - partOfProject (→ medorah:Project)
  - inCollection (→ medorah:Collection)
  - hasAudioFile (→ medorah:AudioFile)
  - hasTranscriptFile (→ medorah:TranscriptFile)
  - hasSpeechSegment (→ medorah:SpeechSegment)
  - identifier (xsd:string)
  - title (xsd:string)
  - description (xsd:string)
  - date (xsd:date)
  - location (xsd:string)
  - duration (xsd:duration)
  - language (xsd:language)
  - subject (xsd:string)
  - accessRights (xsd:string)
  - hasPID (xsd:anyURI)
  - accessConditions (xsd:string)

### medorah:Interviewer
- **Label**: Interviewer
- **Description**: Represents a person conducting an oral history interview, including their professional details and role in the interview process.
- **Subclass of**: foaf:Person
- **Properties**:
  - affiliation (xsd:string)
  - biography (xsd:string)
  - role (xsd:string)

### medorah:Interviewee
- **Label**: Interviewee
- **Description**: Represents a person being interviewed in an oral history session, including their biographical information and demographics.
- **Subclass of**: foaf:Person
- **Properties**:
  - affiliation (xsd:string)
  - biography (xsd:string)
  - demographics (xsd:string)

### medorah:Project
- **Label**: Project
- **Description**: Represents a research project under which interviews are conducted, including project details, funding information, and associated researchers.
- **Properties**:
  - identifier (xsd:string)
  - title (xsd:string)
  - description (xsd:string)
  - startDate (xsd:date)
  - endDate (xsd:date)
  - funding (xsd:string)
  - researchers (xsd:string)

### medorah:Collection
- **Label**: Collection
- **Description**: Represents a collection of interviews or related materials, including metadata about the collection's scope, creator, and access rights.
- **Properties**:
  - identifier (xsd:string)
  - title (xsd:string)
  - description (xsd:string)
  - creator (xsd:string)
  - dateRange (xsd:string)
  - extent (xsd:string)
  - accessRights (xsd:string)

### medorah:AudioFile
- **Label**: Audio File
- **Description**: Represents the original audio recording of an interview, including technical metadata and file integrity information.
- **Properties**:
  - identifier (xsd:string)
  - fileName (xsd:string)
  - fileFormat (xsd:string)
  - duration (xsd:duration)
  - bitRate (xsd:integer)
  - samplingRate (xsd:integer)
  - fileSize (xsd:long)
  - checksum (xsd:string)
  - equipment (xsd:string)

### medorah:TranscriptFile
- **Label**: Transcript File
- **Description**: Represents the transcription of an interview, including metadata about the transcription process and file characteristics.
- **Properties**:
  - identifier (xsd:string)
  - fileName (xsd:string)
  - fileFormat (xsd:string)
  - wordCount (xsd:integer)
  - fileSize (xsd:long)
  - checksum (xsd:string)
  - speechToTextTool (xsd:string)

### medorah:SpeechSegment
- **Label**: Speech Segment
- **Description**: Represents a specific segment of speech within an interview, including timing information, speaker identification, and content analysis.
- **Properties**:
  - identifier (xsd:string)
  - startTime (xsd:time)
  - endTime (xsd:time)
  - transcriptText (xsd:string)
  - speaker (→ foaf:Person)
  - audioFileReference (→ medorah:AudioFile)
  - speechCharacteristics (xsd:string)
  - segmentIndex (xsd:integer)
  - synopsis (xsd:string)
  - keywords (xsd:string)

## Common Properties
- identifier (xsd:string)
- title (xsd:string)
- description (xsd:string)
- date (xsd:date)
- location (xsd:string)
- duration (xsd:duration)
- language (xsd:language)
- subject (xsd:string)
- accessRights (xsd:string)

## FAIR-specific Properties
- hasPID (xsd:anyURI): Associates a persistent identifier with a resource
- accessConditions (xsd:string): Specifies the conditions under which the resource can be accessed

## External Ontology Alignments
- medorah:Interview rdfs:subClassOf dcterms:BibliographicResource
- medorah:Interviewer rdfs:subClassOf foaf:Person
- medorah:Interviewee rdfs:subClassOf foaf:Person
- medorah:Interview rdfs:subClassOf prov:Entity