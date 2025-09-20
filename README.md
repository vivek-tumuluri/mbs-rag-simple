# 🎬 Manchester-by-the-Sea RAG System

A simple yet powerful **Retrieval-Augmented Generation (RAG)** system that allows you to ask questions about the Manchester-by-the-Sea movie script using AI. The system converts the PDF script into searchable vectors and uses semantic similarity to find relevant content for answering questions.

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4-green.svg)](https://openai.com/)
[![ChromaDB](https://img.shields.io/badge/ChromaDB-Vector%20DB-orange.svg)](https://www.trychroma.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🚀 Features

- **📄 PDF Document Processing**: Automatically extracts and processes PDF files
- **🔍 Semantic Search**: Uses vector embeddings for intelligent content retrieval
- **🤖 AI-Powered Q&A**: Generates accurate, conversational answers based on document content
- **📍 Source Attribution**: Shows which parts of the document were used
- **✅ Quality Filtering**: Only responds when confident in the answer
- **🧠 Intelligent Analysis**: Connects information from different parts of the document
- **📝 Partial Information Handling**: Works with available context even when incomplete

## 📁 Project Structure

```
mbs-rag-simple/
├── data/                    # Source documents (PDFs)
│   └── Manchester-by-the-Sea.pdf
├── chroma/                  # Vector database storage (auto-generated)
├── create_database.py       # Document processing pipeline
├── query_data.py           # Question answering system
├── requirements.txt        # Python dependencies
├── .env                    # Environment variables (create this)
└── README.md              # This file
```

## 🛠️ Installation

### Prerequisites
- Python 3.8 or higher
- OpenAI API key

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/vivek-tumuluri/mbs-rag-simple.git
   cd mbs-rag-simple
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   Create a `.env` file in the project root:
   ```bash
   OPENAI_API_KEY=your_openai_api_key_here
   ```

## 📚 Dependencies

| Package | Purpose |
|---------|---------|
| `langchain-community` | Document loaders and vector stores |
| `langchain-openai` | OpenAI integration for embeddings and chat |
| `python-dotenv` | Environment variable management |
| `chromadb` | Vector database for similarity search |
| `pypdf` | PDF text extraction |

## 🚀 Usage

### Step 1: Process Documents

First, add your PDF files to the `data/` folder, then run:

```bash
python create_database.py
```

This will:
- Load all PDF files from the `data/` folder
- Split them into 1000-character chunks with 200-character overlap
- Convert chunks to vector embeddings using OpenAI
- Store everything in a ChromaDB vector database

### Step 2: Ask Questions

Query the system with questions about your documents:

```bash
python query_data.py "What is the movie about?"
python query_data.py "Who is Lee Chandler?"
python query_data.py "What happens to Lee and Patrick?"
python query_data.py "What is Lee's job?"
python query_data.py "How do Lee and Patrick relate to each other?"
```

## 🔧 How It Works

### Document Processing Pipeline

1. **📂 Load Documents**: Scans `data/` folder for PDF files
2. **✂️ Split Text**: Breaks documents into manageable chunks (1000 chars)
3. **🧮 Generate Embeddings**: Converts text chunks to vector representations
4. **💾 Store in Database**: Saves embeddings in ChromaDB for fast retrieval

### Question Answering Process

1. **🔄 Convert Query**: Transforms your question into a vector embedding
2. **🔍 Similarity Search**: Finds the 3 most similar document chunks
3. **✅ Quality Check**: Only proceeds if similarity > 50%
4. **🧠 Intelligent Analysis**: AI analyzes and connects information from retrieved chunks
5. **💬 Generate Answer**: Uses ChatGPT with improved prompt template for conversational responses
6. **📋 Return Response**: Provides detailed answer with source citations

### Vector Similarity

The system uses **cosine similarity** to find relevant content:
- Converts both questions and documents to high-dimensional vectors
- Measures the angle between vectors (not distance)
- Closer angles = more semantically similar content
- Works with synonyms and related concepts (e.g., "car" matches "automobile")

## ⚙️ Configuration

### Chunking Parameters

In `create_database.py`, you can adjust:
- **chunk_size**: Length of text chunks (default: 1000)
- **chunk_overlap**: Overlap between chunks (default: 200)

### Retrieval Parameters

In `query_data.py`, you can modify:
- **k**: Number of chunks to retrieve (default: 3)
- **similarity threshold**: Minimum similarity score (default: 0.5)

### Prompt Template

The system uses an intelligent prompt template that:
- **Analyzes context thoroughly**: Uses available information even when incomplete
- **Connects information**: Synthesizes data from multiple chunks
- **Provides conversational responses**: Natural, helpful answers
- **Handles partial information**: Works with what's available rather than rejecting queries

## 📊 Performance

- **Database size**: ~205 chunks from 1 PDF
- **Response time**: 2-3 seconds per query
- **Accuracy**: High for both specific and general questions
- **Analysis quality**: Intelligent synthesis of information from multiple chunks
- **Memory usage**: ~50MB for typical documents

## 🎯 Example Queries

Here are some example queries that work well with the Manchester-by-the-Sea script:

### Character Questions
```bash
python query_data.py "Who is Lee Chandler?"
python query_data.py "What is Patrick's relationship with Lee?"
```

### Plot Questions
```bash
python query_data.py "What happens to Lee and Patrick?"
python query_data.py "Why does Lee leave Manchester?"
```

### General Story Questions
```bash
python query_data.py "What is the main plot of the movie?"
python query_data.py "What happens in the story?"
```

### Scene Questions
```bash
python query_data.py "What happens in the fishing boat scene?"
python query_data.py "What does Lee do for work?"
```

### Relationship Questions
```bash
python query_data.py "How do Lee and Patrick relate to each other?"
python query_data.py "What is the family dynamic in the story?"
```

## 🔍 Troubleshooting

### Common Issues

1. **"Unable to find matching results"**
   - Try more specific questions
   - Lower the similarity threshold in `query_data.py`
   - Ensure the database was created successfully

2. **Generic responses**
   - Check if your question is too broad
   - Ensure documents contain relevant content
   - Try rephrasing your question

3. **API errors**
   - Verify your OpenAI API key in `.env`
   - Check your API usage limits
   - Ensure you have internet connectivity

4. **Database not found**
   - Run `python create_database.py` first
   - Check that the `chroma/` directory exists
   - Ensure PDF files are in the `data/` directory

### Debug Mode

To see what chunks are being retrieved, the system prints the context before generating the answer.

## 🚀 Extending the System

### Add More Document Types
- Modify `create_database.py` to support other file types
- Add new loaders for Word docs, text files, etc.

### Improve Retrieval
- Experiment with different chunk sizes
- Add metadata to chunks for better filtering
- Implement hybrid search (keyword + semantic)

### Enhanced Responses
- Add conversation memory
- Implement follow-up questions
- Add confidence scoring

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Add new document types
- Improve the prompt templates
- Add new features
- Report issues or bugs
- Improve documentation

## 📄 License

This project is open source and available under the [MIT License](https://opensource.org/licenses/MIT).

## ⚠️ Important Notes

- **API Costs**: This system requires an OpenAI API key and will make API calls for both embedding generation and response generation. Monitor your usage to avoid unexpected costs.
- **Data Privacy**: The system sends document content to OpenAI's servers for processing. Ensure compliance with your data privacy requirements.
- **Rate Limits**: Be aware of OpenAI's rate limits when processing large documents or making many queries.

## 🙏 Acknowledgments

- Built with [LangChain](https://langchain.com/) for document processing and AI integration
- Uses [ChromaDB](https://www.trychroma.com/) for vector storage and retrieval
- Powered by [OpenAI](https://openai.com/) for embeddings and language generation
- Inspired by the Manchester-by-the-Sea screenplay by Kenneth Lonergan

---