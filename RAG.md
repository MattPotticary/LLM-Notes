# RAG

[Home](outline.md)

- [RAG](#rag)
  - [RAG Terminology](#rag-terminology)
  - [Architecture](#architecture)
  - [Data Ingestion](#data-ingestion)
  - [Data Sources](#data-sources)
    - [Preprocessing](#preprocessing)
    - [Storage and Optimization](#storage-and-optimization)
    - [Chunking](#chunking)
    - [Embeddings / Alternatives](#embeddings--alternatives)
      - [Embedding Techniques](#embedding-techniques)
      - [Alternatives to Embeddings](#alternatives-to-embeddings)
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

- Traditional Vector search
- Memory RAG
- Hybrid RAG (Knowledge graphs)
- Hypothetical Document Embeddings
- Corrective RAG
- Self-RAG
- Agentic RAG

## Data Ingestion

- Static: One-time batch ingestion of a fixed corpus.
- Dynamic: Continuous updating of the corpus with new information.
- Batch: Periodic ingestion of data in batches.
- Streaming: Immediate ingestion of data as it becomes available.

## Data Sources

- Binary formats (images, audio, video, PDFs) - requires specialized processing (OCR, speech-to-text)
- Text data (HTML, Markdown, TXT) - requires parsing and cleaning
- Stuctured data (spreadsheets)

### Preprocessing

- Text extraction and cleaning
- Normalization (lowercasing, removing punctuation)
- Deduplication
- Language detection and filtering
- OCR for images/documents

### Storage and Optimization

- Compression techniques
- Caching strategies
- Scalability considerations (distributed systems)
- Cost optimization (e.g., embedding model selection)

### Chunking

- Sentance
- Document
- Page
- Paragraph
- Semantic
- LLM based
- Recursive Character Splitting
- Fized chunk size
- Parent / Child ?? Late Chunking??

### Embeddings / Alternatives

#### Embedding Techniques

- Dense Embeddings
- Sparse Embeddings
- Multi-modal Embeddings
- Fine-tuned Embeddings

#### Alternatives to Embeddings

- TF-IDF: term frequency-inverse document frequency for keyword-based relevance scoring.
- BM25: an improved version of TF-IDF that considers term saturation and document length normalization.
- Keyword-based Search: using inverted indices to quickly find documents containing specific keywords.
- Hybrid Approaches / combining embeddings with keyword search: using embeddings for semantic similarity while also leveraging keyword matches for precision.

### Metadata

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
