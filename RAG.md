# Typical RAG Flow

![alt text](image-2.png)

# Chunking Strategies
<h2> Size Based </h2>
    <h3> Technique: Divide the text into strings of equal length </h3>
    <p> 1. Incude overlap on each side of the chunk to include some context </p>
    <p> 2. Easy to implement but break up related content int sperate chunks </p>
<h2> Structure Based </h2>
    <h3> Technique: Divide the text based upon on the structure (headers, paragraph, sections) </h3>
    <p> 1. Avoids breaking up multiple content into multiple chunks </p> 
    <p> 2. Requires us to understand the structure of document beforehand </p> 
<h2> Semantic Based </h2>
    <h3> Technique: Divide text into groups of related sentences or sections </h3>
    <p> 1. Required us to understand the meaning of invidual sentences </p> 
    <p> 2. Computationally expensive but more relevant chunks </p> 


# Text Embeddings

![alt text](image-3.png)

![alt text](image-4.png)




