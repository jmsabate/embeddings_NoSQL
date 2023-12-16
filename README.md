# embeddings_NoSQL
Representació dels embeddings dels continguts NoSQL, continguts i preguntes sintètiques
El format del registre de les dades 'metadata' emmagatzemades com a payload a la vector store és:
de cada contingut són:

Each data point (data_point) is a dictionary with keys:

"doc_name": name of the segment document

"chunk_title": Chunk title (parapragh name aprox.) of the segment. (There are some nuances in this field, see the previous program)

"source": Values:

  "source" meaning the embedding point is the content itself;
  
  "synthetic_question" meaning the embedding point is a synthetic question its answer is in the content;
  
  "summary" meaning the embedding point is a summary of the content

"chunk": Always the original segment (chunk) no matter if it is the original content, synthetic question or summary.

"source_content": While the key "chunk" always stores the original content, this key contains:

 	if key["source"] == "source": "source_content" = {chunk} content
	
 	if key["source"] == "synthetic_question": "source_content" = {syntethic question}
	
 	if key["source"] == "summary": "source_content" = {summary}

"data_point": is built according to the requirements of the embedding model, plus adding the doc_name and chunk_title. Currently the result of concatenate: 

 	string "passage: " (according to the embedding model recommendation) + 
 	
  	value of the key "doc_name" of the data_point above + 
	
 	value of the key "chunk_title" of the data_point above + 
 	
  	value of the key "source_content" of the data_point above.


For each data point there are three relevant elements

1 DATA POINT KEY

An integer starting from 0 when creating the data base

2 EMBEDDING VECTOR

The string stored in the field data_point["data_point"] defined above

3 METADATA (PAYLOAD)

The dictionary data_point defined above.
