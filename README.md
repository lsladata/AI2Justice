## RAG-Based Chatbot
A customizable Retrieval-Augmented Generation (RAG) chatbot that allows you to build intelligent conversational AI systems with your own data sources.

🌟 Overview
This project provides a foundation for creating chatbots that can answer questions based on your specific documents and knowledge base. Using RAG technology, the chatbot retrieves relevant information from your data and generates accurate, contextual responses.

✨ Features
Hybrid Search: Combines semantic search (embeddings) with keyword search (BM25) for optimal retrieval
Document Processing: Support for multiple document formats (PDF, TXT, DOCX, Markdown)
Vector Embeddings: Create and store document embeddings with metadata for semantic search
BM25 Integration: Traditional keyword-based search for precise matching
Streamlit UI: Interactive and user-friendly chat interface
Customizable: Easy to adapt to your specific use case
Scalable: Handles large document collections
🏗️ Architecture
User Query → Hybrid Retrieval → Context Ranking → LLM Generation → Response
              ├─ Vector Embeddings (Semantic - Metadata Enhanced)
              └─ BM25 (Keyword)
The system:

Converts your documents into embeddings and builds BM25 index
Stores embeddings in a vector database
For each query, performs both semantic search (embeddings) and keyword search (BM25)
Combines and ranks results from both methods
Generates responses using an LLM with the retrieved context
📋 Prerequisites
Python 3.8+
OpenAI API key (or other LLM provider)
Virtual environment (recommended)
🚀 Quick Start
1. Clone the Repository
Copygit clone https://github.com/yourusername/rag-chatbot.git
cd rag-chatbot
2. Install Dependencies
Copypip install -r requirements.txt
3. Configure Environment
Create a .env file in the project root:

OPENAI_API_KEY=your_api_key_here
VECTOR_DB_PATH=./data/vectordb
DOCUMENTS_PATH=./data/documents
4. Add Your Documents
Place your documents in the data/documents directory:

Copymkdir -p data/documents
# Add your PDF, TXT, or DOCX files here
5. Build the Embeddings and Indexes
Copypython build_embeddings.py
This script will:

Process all documents in the data/documents directory
Generate vector embeddings for semantic search
Build BM25 index for keyword search
Save both indexes for fast retrieval
6. Run the Streamlit App
Copystreamlit run app.py
The app will open in your browser at http://localhost:8501

📁 Project Structure
rag-chatbot/
├── app.py                  # Streamlit chat application
├── build_embeddings.py     # Script to build embeddings and BM25 index
├── requirements.txt        # Python dependencies
├── .env.example           # Environment variables template
├── data/
│   ├── documents/         # Your source documents
│   ├── embeddings/        # Stored vector embeddings
│   └── bm25_index/        # BM25 index storage
├── src/
│   ├── document_loader.py # Document processing
│   ├── embeddings.py      # Embedding generation
│   ├── bm25_retriever.py  # BM25 search implementation
│   ├── hybrid_search.py   # Combines vector + BM25 search
│   └── chatbot.py         # RAG logic
└── tests/                 # Unit tests
🔧 Configuration
Choosing Your LLM
Edit config.py to select your preferred language model:

CopyLLM_PROVIDER = "openai"  # Options: openai, anthropic, huggingface
MODEL_NAME = "gpt-4"
TEMPERATURE = 0.7
Hybrid Search Configuration
Adjust the balance between semantic and keyword search in config.py:

Copy# Retrieval settings
VECTOR_WEIGHT = 0.6  # Weight for embedding-based search
BM25_WEIGHT = 0.4    # Weight for BM25 keyword search
TOP_K = 5            # Number of documents to retrieve
Vector Database Options
The project supports multiple vector stores:

ChromaDB (default): Easy to use, persistent storage
FAISS: Fast similarity search
Pinecone: Cloud-based, scalable solution
Customizing the Prompt
Modify the system prompt in src/chatbot.py to adjust the chatbot's behavior:

CopySYSTEM_PROMPT = """
You are a helpful assistant that answers questions based on the provided context.
Always cite sources when possible and admit when you don't know something.
"""
📚 Usage Examples
Using the Streamlit App
Run the app: streamlit run app.py
Upload documents or use pre-loaded documents
Type your question in the chat interface
View responses with source citations
Building Embeddings Programmatically
Copyfrom src.embeddings import EmbeddingBuilder
from src.bm25_retriever import BM25Indexer

# Build vector embeddings
embedding_builder = EmbeddingBuilder()
embedding_builder.process_documents('./data/documents')
embedding_builder.save('./data/embeddings')

# Build BM25 index
bm25_indexer = BM25Indexer()
bm25_indexer.build_index('./data/documents')
bm25_indexer.save('./data/bm25_index')
Using Hybrid Search
Copyfrom src.hybrid_search import HybridRetriever

retriever = HybridRetriever(
    embeddings_path='./data/embeddings',
    bm25_path='./data/bm25_index'
)

# Retrieve relevant documents
results = retriever.search(
    query="Your question here",
    vector_weight=0.6,
    bm25_weight=0.4,
    top_k=5
)
🛠️ Advanced Features
Understanding Hybrid Search
The hybrid search combines two complementary approaches:

Vector Embeddings (Semantic Search)

Understands meaning and context
Finds conceptually similar content
Handles synonyms and paraphrasing
Better for abstract queries
BM25 (Keyword Search)

Precise keyword matching
Fast and efficient
Better for specific terms and names
Handles rare or technical terms
Tuning Search Weights
Experiment with different weight combinations:

Copy# More semantic (better for conceptual questions)
retriever.search(query, vector_weight=0.8, bm25_weight=0.2)

# More keyword-based (better for specific terms)
retriever.search(query, vector_weight=0.3, bm25_weight=0.7)

# Balanced (default)
retriever.search(query, vector_weight=0.6, bm25_weight=0.4)
Adding Custom Document Loaders
Extend DocumentLoader class to support new file formats:

Copyfrom src.document_loader import DocumentLoader

class CustomLoader(DocumentLoader):
    def load_custom_format(self, file_path):
        # Your custom loading logic
        pass
Rebuilding Indexes
When you add or update documents:

Copy# Rebuild both embeddings and BM25 index
python build_embeddings.py --rebuild

# Or rebuild incrementally (only new documents)
python build_embeddings.py --incremental
🧪 Testing
Run the test suite:

Copypytest tests/
📝 Best Practices
Document Preparation: Clean and structure your documents before indexing
Chunk Size: Experiment with different chunk sizes (default: 512 tokens)
Overlap: Use overlap between chunks to maintain context (default: 50 tokens)
Hybrid Weights: Tune vector/BM25 weights based on your document type
Technical docs: Higher BM25 weight (0.5-0.6)
General content: Higher vector weight (0.6-0.7)
Regular Updates: Rebuild indexes when documents change
Monitoring: Track query performance and relevance
Testing: Compare results with vector-only vs hybrid search
🤝 Contributing
Contributions are welcome! Please:

Fork the repository
Create a feature branch (git checkout -b feature/AmazingFeature)
Commit your changes (git commit -m 'Add some AmazingFeature')
Push to the branch (git push origin feature/AmazingFeature)
Open a Pull Request
📄 License
This project is licensed under the MIT License - see the LICENSE file for details.

🙏 Acknowledgments
Streamlit - Web application framework
LangChain - Framework for LLM applications
Sentence Transformers - Embedding models
Rank-BM25 - BM25 implementation
OpenAI - Language models
📞 Support
Issues: GitHub Issues
Discussions: GitHub Discussions
Email: your.email@example.com
🗺️ Roadmap
 Multi-language support
 Advanced filtering options
 Conversation history in Streamlit
 User authentication
 Docker deployment
 Cloud deployment guides (AWS, GCP, Azure)
 Streaming responses
 Multiple data source support
 Reranking models integration
 Query expansion techniques
 A/B testing for search weights
Note: This is a template project. Please customize it according to your specific requirements and use case.

Made with ❤️ by [Your Name]
