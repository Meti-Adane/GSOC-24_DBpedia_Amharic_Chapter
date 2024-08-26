# GSOC-24

# Project Summary 
This project endeavors to create an Amharic DBpedia Chapter, aiming to be the first sub-Saharan African language to join the internationalization efforts of DBpedia. Our goal is to extend the existing extractor framework for Amharic to allow knowledge graph extraction from Amharic Wikipedia. We will make the extracted knowledge graph queryable and available to end users via a web page .

# Key Achivemnts and deliverables 
  - Extended the DBpedia framework to support Amharic.
      - [View Change list](https://github.com/dbpedia/extraction-framework/pull/766) 
  - Added wiki template to DBepdia ontology class and properties mapping, achieving a 35% overall mapping completion, up from the initial 0%.
      - [View Amharic mappings](https://mappings.dbpedia.org/index.php/Mapping_am) 
  - Added data parsers to handle linguistic nuances specific to Amharic.
      - [Ethiopian calendar date handler](https://github.com/dbpedia/extraction-framework/pull/763) 
      - [Duration + Datatypes for Amharic](https://github.com/dbpedia/extraction-framework/pull/764)
  - Extracted triples from Wikipedia dumps using configured extractors, resulting in a total of 8.2 million triples and 300k distinct triples. These triples were uploaded to triple stores and are now accessible for querying by end users via Virtuoso and QLever endpoints.
  -    - [Virtuoso sparql endpoint](https://virtuoso.am.dbpedia.nliwod.org/sparql)
       - [Qlever endpoint](https://qlever-ui.dbpedia.nliwod.org)
  
  - Created and deployed a website for Amharic DBpedia, making the extracted triples accessible to users.
      - [View Website](https://am.dbpedia.nliwod.org)


# Project Description
DBpedia is a collaborative initiative focused on extracting structured information from Wikipedia and presenting it as Linked Open Data. While semantic web resourceful languages like English and German have dedicated DBpedia chapters, there is a need for more representation of low-resourced languages like Amharic.
Amharic is the official language of Ethiopia and the second most widely spoken Semitic language globally, following Arabic, with approximately 22 Million speakers at the time of writing. However, it is one such language that lacks its own DBpedia chapter. 

The primary goal of this project is to contribute to DBpedia internationalization efforts and create an Amharic DBpedia Chapter to allow knowledge graph extraction from Amharic Wikipedia. Our goal is to extend the existing extractor framework for Amharic.

## Extending extractors 
We added data parser and extractor configurations to enable the extraction of knowledge graphs from Amharic Wikipedia. As a result, we extended the following extractors:

**GeoCoordinate Parser:** Extracts geographical coordinates from Wikipedia articles, enabling the inclusion of location-based data in the knowledge graph.
**Date time parser:** Parses dates and times to standardize and include temporal information in the knowledge graph.
**DateInterval Mapping:** Handles intervals between dates, capturing ranges of time for events or periods mentioned in articles.
**Disambiguation Extractor:** Identifies and processes disambiguation pages to correctly associate terms with their intended meanings.
**Gender Extractor:** Extracts gender information from articles to enrich the dataset with gender-specific data.
**Homepage Extractor:** Extracts official homepage URLs from Wikipedia articles, linking entities to their corresponding websites.
**ImageExtractor:** Retrieves images associated with Wikipedia articles, adding visual context to the knowledge graph.
**InfoboxExtractor:** Extracts structured data from infoboxes in Wikipedia articles, a key source of information for building knowledge graphs.
**TopicalConcepts Extractor:** Extends the knowledge graph by identifying and extracting key concepts related to the topics covered in Wikipedia articles.

## Handling Nuances for Amharic 
Extending the above extractors enabled us to effectively extract a knowledge graph from Amharic Wikipedia. However, upon inspecting the triples, we discovered that dates written in the Ethiopian calendar were being incorrectly mapped due to our initial one-to-one mapping configuration. We realized we needed to implement a handler to convert Ethiopian dates to Gregorian ones. Additionally, we had to address dates written in Geez numerals.

Our approach involved converting the Ethiopian date to a Julian date, followed by converting the Julian date back to the Gregorian calendar. For converting Geez numerals to Arabic numerals, we employed a graph-based approach. This method assigns the highest multiplier to the root node, derived from the rightmost value. We then take the value from the left subtree, multiply it by the node value, and add the value from the right subtree to the product. The order of operations is crucial in ensuring accurate conversions.

## Extracted Data 
Once we had the extractors and nuance handlers configured for Amharic, the next step was to add more mappings to th [mappings server](https://mappings.dbpedia.org/index.php/Mapping_am) for mapping-based extractors. We then ran both generic and mapping-based extractors. Finally, we made these triples available via: 
- [Databus collection](https://databus.dbpedia.org/purplebee/collections/am_chapter/)
- [Virtuoso sparql endpoint](https://virtuoso.am.dbpedia.nliwod.org/sparql)
- [Qlever endpoint](https://qlever-ui.dbpedia.nliwod.org)



# What's next 
This project serves as a foundational step toward developing a comprehensive Amharic chapter. Future contributors can advance the project by:
- Adding more mappings
- Adding more infboxes in [am.wikipedia](https://am.wikipedia.org/wiki/ዋናው_ገጽ)
- Add new Extractors or Extend more extractors for amharic 

