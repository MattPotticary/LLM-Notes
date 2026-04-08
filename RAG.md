# RAG

This document provides an overview of Retrieval-Augmented Generation (RAG) systems, serving as a reference for key concepts and considerations for: architecture, data ingestion strategies, retrieval techniques, context relevance filtering, generation methods, evaluation measures, security concerns, and tools/frameworks in the RAG ecosystem.

- [RAG](#rag)
  - [RAG Terminology](#rag-terminology)
  - [Architecture](#architecture)
  - [Data Ingestion](#data-ingestion)
    - [Preprocessing](#preprocessing)
    - [Engineering considerations](#engineering-considerations)
    - [Chunking](#chunking)
    - [Embeddings](#embeddings)
    - [Metadata](#metadata)
  - [Retrieval](#retrieval)
  - [Context Relevance Filtering](#context-relevance-filtering)
  - [Generation](#generation)
  - [Evaluation Measures](#evaluation-measures)
  - [Security Concerns](#security-concerns)
  - [RAG Tools and Frameworks](#rag-tools-and-frameworks)

## RAG Terminology

- Grounding / Faithfulness: ensuring model responses are supported by retrieved evidence rather than invented.
- Retriever: the component that finds relevant documents or passages from the indexed corpus.
- Generator: the LLM that uses retrieved context to compose the final answer.
- Retriever-Generator gap: mismatch between what is retrieved and what the generator needs.
- Corpus: the collection of documents, passages, or knowledge sources used for retrieval.
- Vector store: embedding database used for semantic similarity search.
- Semantic search: retrieval based on meaning rather than exact keyword matching.
- Hallucination: generation of unsupported or incorrect information by the model.
- Source attribution: linking model output to specific retrieved documents or passages.
- Relevance scoring: ranking retrieved items by how well they match the query.
- Context window: the token limit for the model to process prompt plus retrieved content.
- Multi-hop retrieval: using sequential retrieval steps to answer complex questions.
- Prompt injection: malicious or irrelevant information introduced through retrieved context.
- Query rewriting: transforming the original query to improve retrieval effectiveness.
- Retrieval latency: time taken to fetch and return relevant context for the model.
- Evidence aggregation: combining multiple retrieved passages into a coherent response.
- Validation / consistency check: verifying that generated answers are supported by retrieved evidence.
- Feedback loop: using generated output or user corrections to improve future retrieval and ranking.

## Architecture

A RAG system is generally made up of 3 main components: the first being a query recieved from the user, the second being a retriever which searches a corpus of documents for relevant information, and the third being a generator (LLM) which takes the retrieved information and produces a final answer.

Vector search: Embeddings are used to represent documents and queries in a high-dimensional space, allowing for semantic similarity search.

![Vector search architecture](assets/vector_retrieval.svg)

Memory RAG: Similar to vector search but with a focus on maintaining a dynamic memory of past interactions and retrieved information.

![Memory RAG architecture](assets/memory_rag.svg)

Hybrid RAG (Knowledge graphs): Combines vector search with structured knowledge graphs to enhance retrieval and reasoning capabilities.

![Hybrid RAG architecture](assets/hybrid_rag.svg)

Hypothetical Document Embeddings: Instead of embedding the original documents, this approach generates hypothetical documents based on the query and embeds those for retrieval.

![Hypothetical Document Embeddings architecture](assets/hypo_rag.svg)

Corrective RAG: Uses feedback from the generator to iteratively refine the retrieval process, improving relevance over time.

![Corrective RAG architecture](assets/cor_rag.svg)

Self-RAG: The model retrieves information from its own generated content or internal knowledge, rather than an external corpus.

![Self-RAG architecture](assets/self_rag.svg)

Agentic RAG: Integrates RAG into an agent architecture, allowing for multi-step reasoning and interaction with external tools or APIs during the retrieval and generation process.

![Agentic RAG architecture](assets/agentic_rag.svg)

## Data Ingestion

Data ingestion strategies for RAG systems can vary based on the use case and requirements. Some common approaches include:

- Static: One-time batch ingestion of a fixed corpus.
- Dynamic: Continuous updating of the corpus with new information.
- Batch: Periodic ingestion of data in batches.
- Streaming: Immediate ingestion of data as it becomes available.

Data comes in many forms and from many sources, and the ingestion strategy and preprocessing will depend on the specific use case. Some common data sources include:

- Binary formats (images, audio, video, PDFs) - requires specialized processing (OCR, speech-to-text)
- Text data (HTML, Markdown, TXT) - requires parsing and cleaning
- Structured data (spreadsheets)

### Preprocessing

- Text extraction, cleaning, and normalization
- Document deduplication
- OCR for images/documents

### Engineering considerations

- Compression techniques
- Caching strategies
- Scalability considerations
- Cost optimization (e.g., embedding model selection)

### Chunking

For textual documents, different chunking strategies can be employed to break down documents into manageable pieces for retrieval and generation. Ideally we want to minimize the amount of irrelevant information included in each chunk while maximizing the amount of relevant information.

The simplest chunking strategy is to use a fixed chunk size, where the document is split into equal-sized chunks based on a predetermined number of tokens or characters, this technique is easy to implement and was the traditional approach used in early RAG systems due to limitation of model context sizes. However, this approach may not always align well with natural language boundaries and can lead to fragmented information.

To get around this, another set of strategies include breaking the document down into structural units such as:

- Document
- Page
- Paragraph
- Sentence

This approach can help preserve the semantic integrity of the information and improve retrieval relevance, but it may require more complex parsing and may result in variable chunk sizes that need to be managed effectively.

Where as other strategies may focus on token counts or semantic boundaries:

- Semantic
- LLM based

Other strategies may involve more complex approaches such as:

- Recursive Character Splitting
- Parent / Child ?? Late Chunking??

### Embeddings

- Dense Embeddings: models like BERT, RoBERTa, or Sentence Transformers to create dense vector representations of documents and queries.
- Contextual Embeddings: models that generate embeddings based on the context of the query and document (e.g., using cross-encoders).
- Multi-modal Embeddings: combining embeddings from different modalities (e.g., text and images).
- Domain specific fine-tuned Embeddings: embeddings that have been fine-tuned for a specific task or domain.
- Sparse Embeddings: techniques like TF-IDF, BM25 to create sparse vector representations.
  - TF-IDF: term frequency-inverse document frequency for keyword-based relevance scoring.
  - BM25 is an improved version of TF-IDF that considers term saturation and document length normalization.
- Keyword-based Search: using inverted indices to quickly find documents containing specific keywords.
- Hybrid Approaches / combining embeddings with keyword search: using embeddings for semantic similarity while also leveraging keyword matches for precision.
- Knowledge Graph Embeddings: representing entities and relationships in a knowledge graph as vectors for retrieval.

### Metadata

Typically as the dataset is ingested and split up into chunks, various metadata is stored along with the chunk to provide additional context and information for retrieval and generation. Common metadata fields include:

- Document ID
- Creation / Modified Datetime
- Version
- Source / Proviencne
- Access controls
- Author
- Document type
- Tags
- Embedding / Chunking strategy

## Retrieval

- Sentence-Window Retrieval
- Auto-Merging
- Query Rewriting
- Multi-Hop Retrieval
- Re-ranking

## Context Relevance Filtering

- Relevance Scoring
- Thresholding
- Top-K Selection
- Dynamic Context Sizing
- Redundancy Removal
- Diversity Promotion
- Context Summarization
- User Feedback Integration

## Generation

- Source Attribution
- Answer Generation
- Answer Validation
- Multi-hop Reasoning
- Explanation Generation
- Counterfactual Generation
- Self-Consistency / Self-Verification

## Evaluation Measures

- Context Relevance
- Groundedness
- Answer Relevance (the "RAG Triad")
- NDCG
- MRR
- F1 scores
- Human evaluation (accuracy, helpfulness, faithfulness)
- Hallucination rate

## Security Concerns

- Prompt injection via retrieved context
- Data privacy and access controls for sensitive documents
- Adversarial attacks on retriever or generator components
- Mitigation strategies (e.g., input sanitization, access controls)

## RAG Tools and Frameworks

- Haystack
- LangChain
- LlamaIndex
- OpenAI Retrieval API
- Hugging Face RAG implementations
- AWS Bedrock Retrieval
- Azure Cognitive Search with RAG
- Pinecone + LLM integration
