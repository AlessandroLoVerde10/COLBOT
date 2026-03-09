# COLBOT
Collateral framework RAG chatbot developed during my time at the ECB (only publicly available info shared).
It delivers legally grounded responses with article references through an intuitive graphic interface. The app has been improved benefiting of experts' feedback and review of the responses.

![unnamed](https://github.com/user-attachments/assets/bfeaf538-abfd-4d65-8c24-31ecf363c939)

## Background
My journey with RAG (Retrieval-Augmented Generation) systems at the ECB started during a training (Data Academy) where the final project (DevGPT) was a chatbot to explore internal code repositories in GITLAB.

## App today
After a year of development, we - ECB's Market operations Innovation Lab and Market Operations Framework - launched COLBOT (Collateral Framework Chatbot), a RAG-based chatbot for exploring the European collateral legal framework. 


The app is now available for internal use across the entire European System of Central Banks (ECB + 27 National Central Banks) on a AWS secure platform. It has been presented to wide audiences and conferences in the ESCB: like Market Operations committee, DG-M Townhall, Markets AI Network, Collateral management Network, ...

 
COLBOT uses the following publicly available sources on the EURLEX website:
- [General Documentation EU 2015/510 (ECB/2014/60)](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02014O0060-20250616)
- Haircuts Guideline EU 2016/65
- Temporary Framework ECB/2014/31


## Architecture

1) Data ingestion and pre-processing
EURLEX (HTML) guidelines are parsed collecting metadata, corpus and cross-references, then chunked via recursive splitter and stored in a vector DB using an embedding model.

2) Pre-retrieval: Query Transformation
The user query is expanded and improved by an LLM based on specific definitions and then semantically labelled according to predefined macro-categories.

3) Retrieval of the relevant legal context
Relevant legal paragraphs are retrieved via similarity search (Titan 2) between the query and chunked legal text, either on the full embedding space (basic) or on a filtered semantic cluster (advanced).

4) Post-retrieval: Augmentation & Generation
Retrieved chunks (with metadata and tables) are concatenated into the final prompt, ranked by similarity score. An LLM judge pre-filters sources for relevance. Claude 3.5 then generates the response, maintaining chat history across follow-up questions.

Final prompt: ”You are ColBot, a RAG chatbot useful to answer queries about asset eligibility … {LEGAL CONTEXT} {user query}”

<img width="4543" height="1405" alt="unnamed" src="https://github.com/user-attachments/assets/6ced8a6a-66d5-4ffc-9dd3-93e60c64452b" />

## Dependencies


### Disclaimer
This post reflects a collective achievement to which I contributed and does not represent an official ECB communication. COLBOT is an AI tool that will improve over time leveraging on new technology, user feedback and developer effort. It is useful for searching extensive documentation and extracting synthetic insights, but relies on standardized prompts, can be inaccurate and of course cannot replace human legal interpretation or the official Guidelines.



In the images below:
- COLBOT architecture
- an example of interaction with the app
