# RAG-Based Chatbot

A customizable Retrieval-Augmented Generation (RAG) chatbot that allows you to build intelligent conversational AI systems with your own data sources.

## 🌟 Overview

This project provides a foundation for creating chatbots that can answer questions based on your specific documents and knowledge base. Using RAG technology, the chatbot retrieves relevant information from your data and generates accurate, contextual responses.

## ✨ Features

- **Document Processing**: Support for multiple document formats (PDF, TXT, DOCX, Markdown)
- **Vector Database**: Efficient similarity search using embeddings
- **Customizable**: Easy to adapt to your specific use case
- **Scalable**: Handles large document collections
- **API Integration**: Ready-to-use API endpoints
- **Modern UI**: Clean chat interface (optional)

## 🏗️ Architecture

```
User Query → Embedding → Vector Search → Context Retrieval → LLM Generation → Response
```

The system:
1. Converts your documents into embeddings
2. Stores them in a vector database
3. Retrieves relevant context for user queries
4. Generates responses using an LLM with the retrieved context

## 📋 Prerequisites

- Python 3.8+
- OpenAI API key (or other LLM provider)
- Virtual environment (recommended)

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/rag-chatbot.git
cd rag-chatbot
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_api_key_here
VECTOR_DB_PATH=./data/vectordb
DOCUMENTS_PATH=./data/documents
```

### 4. Add Your Documents

Place your documents in the `data/documents` directory:

```bash
mkdir -p data/documents
# Add your PDF, TXT, or DOCX files here
```

### 5. Build the Knowledge Base

```bash
python build_index.py
```

### 6. Run the Chatbot

```bash
python app.py
```

Visit `http://localhost:5000` to interact with your chatbot!

## 📁 Project Structure

```
rag-chatbot/
├── app.py                  # Main application
├── build_index.py          # Document indexing script
├── requirements.txt        # Python dependencies
├── .env.example           # Environment variables template
├── data/
│   ├── documents/         # Your source documents
│   └── vectordb/          # Vector database storage
├── src/
│   ├── document_loader.py # Document processing
│   ├── embeddings.py      # Embedding generation
│   ├── vectorstore.py     # Vector database operations
│   └── chatbot.py         # RAG logic
├── templates/             # Web UI templates (if applicable)
└── tests/                 # Unit tests
```

## 🔧 Configuration

### Choosing Your LLM

Edit `config.py` to select your preferred language model:

```python
LLM_PROVIDER = "openai"  # Options: openai, anthropic, huggingface
MODEL_NAME = "gpt-4"
TEMPERATURE = 0.7
```

### Vector Database Options

The project supports multiple vector stores:
- **ChromaDB** (default): Easy to use, persistent storage
- **FAISS**: Fast similarity search
- **Pinecone**: Cloud-based, scalable solution

### Customizing the Prompt

Modify the system prompt in `src/chatbot.py` to adjust the chatbot's behavior:

```python
SYSTEM_PROMPT = """
You are a helpful assistant that answers questions based on the provided context.
Always cite sources when possible and admit when you don't know something.
"""
```

## 📚 Usage Examples

### Basic Query

```python
from src.chatbot import RAGChatbot

chatbot = RAGChatbot()
response = chatbot.query("What is the main topic of the documents?")
print(response)
```

### API Endpoint

```bash
curl -X POST http://localhost:5000/chat \
  -H "Content-Type: application/json" \
  -d '{"query": "Your question here"}'
```

## 🛠️ Advanced Features

### Adding Custom Document Loaders

Extend `DocumentLoader` class to support new file formats:

```python
from src.document_loader import DocumentLoader

class CustomLoader(DocumentLoader):
    def load_custom_format(self, file_path):
        # Your custom loading logic
        pass
```

### Implementing Conversation Memory

Enable multi-turn conversations by storing chat history.

### Fine-tuning Retrieval

Adjust retrieval parameters for better results:

```python
retriever = vectorstore.as_retriever(
    search_type="similarity",
    search_kwargs={"k": 5}  # Number of documents to retrieve
)
```

## 🧪 Testing

Run the test suite:

```bash
pytest tests/
```

## 📝 Best Practices

1. **Document Preparation**: Clean and structure your documents before indexing
2. **Chunk Size**: Experiment with different chunk sizes (default: 1000 tokens)
3. **Overlap**: Use overlap between chunks to maintain context (default: 200 tokens)
4. **Regular Updates**: Rebuild the index when documents change
5. **Monitoring**: Track query performance and relevance

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [LangChain](https://langchain.com/) - Framework for LLM applications
- [ChromaDB](https://www.trychroma.com/) - Vector database
- [OpenAI](https://openai.com/) - Language models

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/rag-chatbot/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/rag-chatbot/discussions)
- **Email**: your.email@example.com

## 🗺️ Roadmap

- [ ] Multi-language support
- [ ] Advanced filtering options
- [ ] Conversation history
- [ ] User authentication
- [ ] Docker deployment
- [ ] Cloud deployment guides
- [ ] Streaming responses
- [ ] Multiple data source support

---

**Note**: This is a template project. Please customize it according to your specific requirements and use case.

Made with ❤️ by [Your Name]
