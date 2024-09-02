#medorah/ongoing

Here is a draft of necessary metadata that we may need in our project:
**Interview*** Integrate the indexing metadata from OHMS

⠀**Interviewer**
* Identifier (unique ID for each interview)
* Title
* Date
* Location
* Duration
* Language
* Description
* Subject (keywords, need controlled vocabularies)
* Transcript (full-text, time-stamped), where we can Integrate the indexing metadata from OHMS
* Annotations (time-stamped, keywords, notes)
* Access Rights (restrictions, permissions)
* Identifier (unique ID for each interviewer)
* Name
* Affiliation
* Biography
* Role (interviewer, facilitator, etc.)

⠀**Interviewee**
* Identifier (unique ID for each interviewee)
* Name
* Affiliation
* Biography
* Demographics (age, gender, occupation, etc.)

⠀**Project**
* Identifier (unique ID for each project) hashcode
* Title
* Description
* Start Date
* End Date
* Funding (sources, grants)
* Researchers (names, roles)
* Affiliations (institutions, organizations)

⠀**Collection**
* Identifier (unique ID for each collection)
* Title
* Description
* Creator
* Date Range
* Extent (number of interviews, size)
* Access Rights (restrictions, permissions)

⠀**Original Audio File**
* Identifier (unique ID for each audio file)
* File Name
* Format
* Duration
* Bit Rate
* Sampling Rate
* File Size
* MD5 Checksum (for data integrity)
* Equipment used

⠀**Transcript File**
- Identifier (unique ID for each transcript file) 
- File Name 
- Format 
- Word Count 
- File Size 
- Checksum (for data integrity) 
- Speech to Text tool (version, processing pipeline)


**Speech Segments**: 
* Identifier: URI 
* StartTime: time 
* EndTime: time 
* TranscriptText: string 
* Speaker: URI (link to Person) 
* AudioFileReference: URI 
* SpeechCharacteristics: (tones, rhythms, emotions) 
* SegmentIndex: integer 
* Synopsis: text 
* Keywords: String 

**SpeechSegment**:
* Identifier: URI
* StartTime: time
* EndTime: time
* TranscriptText: string
* Speaker: URI (link to Person)
* AudioFileReference: URI
* SpeechCharacteristics:
* SpeechRate: float
* PitchAnalysis:
	* MeanPitch: float
	* PitchRange: float
	* PitchVariability: float
* EmotionDetection:
	* PrimaryEmotion: string
	* EmotionIntensity: float
	* SecondaryEmotions: 
    * {Emotion: string, Intensity: float}
* VoiceQuality:
	* Breathiness: float
	* Creakiness: float
	* VocalEffort: string
* Rhythm:
	* SpeechRhythmRegularity: float
	* PauseFrequency: float
	* AveragePauseDuration: float
* Fluency:
	* FilledPauses: integer
	* Repetitions: integer
	* FalseStarts: integer
	* NonverbalVocalization:
    * {Type: string, TimeOffset: duration}
* LinguisticFeatures:
  * SentenceType: string
  * Sentiment: float
  * KeywordsDetected: 
    * {Keyword: string, Confidence: float}
* NamedEntitiesDetected:
  * {Entity: string, Type: string, Confidence: float}
* OHMSMetadata:
  * SegmentIndex: integer
  * Synopsis: text
  * Keywords: 
    * string
* Subjects:
  * {Subject: string, AuthoritySource: URI}
* GPSCoordinates: GeoCoordinates



**Digitalisation Processing** 
- Software used (environment, version, library dependencies, parameters, processing pipeline)
- The researcher who is responsible for digitalising (Same as the Individual class)




**Multilingual Support**



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

















### From the content perspective
⠀**Some Named Entities in the interview**
* Person
	* Identifier (unique ID for each person)
	* Name
	* Type (interviewer, interviewee, mentioned)
	* Place
	* Identifier (unique ID for each place)
	  * Name
	  * Type (location of interview, mentioned)

* Organization
	* Identifier (unique ID for each organization)
	* Name
	* Type (affiliation, mentioned)

* Event
	* Identifier (unique ID for each event)
	* Name
	* Date
	* Type (historical, personal)

**Some Controlled Vocabularies to be defined**
* Subject Headings
* Identifier (unique ID for each subject heading)
* Term
* Source (e.g., Library of Congress Subject Headings)
* Genres
* Identifier (unique ID for each genre)
* Term
* Source (e.g., Library of Congress Genre/Form Terms)


**Relationships**
* Interview-to-Interviewer
* Interview-to-Interviewee
* Interview-to-Project
* Interview-to-Collection
* Interview-to-Audio File
* Interview-to-Transcript File
* Interview-to-Named Entities
* Named Entities-to-Controlled Vocabularies



For OHMS, I think it is a less standardised but more flexible one. It offers the metadata for **Indexing the interview segments**
* **Segment Title:** A brief title for a specific segment of the interview.
* **Segment Synopsis:** A summary of the content covered in the segment.
* **Segment Keywords:** Keywords or phrases that describe the main topics discussed in the segment.
* **Segment Start Time:** The timestamp indicating the start of the segment.
* **Segment End Time:** The timestamp indicating the end of the segment (if applicable).



Some Mapping
1. Administrative metadata:
   * pbcoreIdentifier: Unique identifier for the interview
   * pbcoreAnnotation: Additional notes about the interview process or content
2. Descriptive metadata:
   * pbcoreTitle: The title of the oral history interview Example: "Interview with John Doe on the history of computing"
   * pbcoreSubject: The main topics covered in the interview Example: "Computer science; ENIAC; Programming languages"
   * pbcoreDescription: A summary of the interview content
   * pbcoreCreator: The interviewer(s) and interviewee(s)
   * pbcoreCoverage: The time period and geographic location discussed
3. Technical metadata:
   * instantiationDigital: The digital file format of the interview recording
   * instantiationDuration: The length of the interview
4. Rights metadata:
   * rightsSummary: Information about usage rights and restrictions





