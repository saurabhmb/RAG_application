# RAG Application - Chat with Your Documents

A simple Retrieval Augmented Generation (RAG) application that lets you upload documents and chat with them using AI.

## What is RAG?

RAG (Retrieval Augmented Generation) combines document retrieval with AI generation to answer questions based on your specific documents. Instead of relying on the AI's training data, it searches through your uploaded content to provide accurate, source-based answers.

## Features

- Upload PDF, CSV, and TXT files
- Add text content directly
- Scrape websites for content
- Chat with your documents using AI
- Local vector database storage (Qdrant)
- Modern web interface

## Quick Start

### Prerequisites
- Node.js 18+
- Docker (for vector database)
- OpenAI API key

### Installation

1. **Clone and install**
```bash
git clone repo
cd RAGApplication
npm install
```

2. **Start the vector database**
```bash
docker-compose up -d
```

3. **Create environment file**
Create `.env.local` in the root directory:
```env
QDRANT_URL=http://localhost:6333
OPENAI_API_KEY=your_openai_api_key_here
```

4. **Run the application**
```bash
npm run dev
```

5. **Open in browser**
Visit `http://localhost:3000`

## How to Use

1. **Enter your OpenAI API key** in the application interface
2. **Add your content:**
   - Upload files (PDF, CSV, TXT - max 10MB)
   - Paste text directly
   - Enter website URLs to scrape
3. **Start chatting** with your documents
4. Ask questions about your uploaded content

## How It Works

1. **Document Processing**: Your files are split into small chunks
2. **Vector Creation**: Each chunk is converted into numerical vectors using OpenAI embeddings
3. **Storage**: Vectors are stored in Qdrant database for fast retrieval
4. **Query Processing**: When you ask a question, the system finds the most relevant chunks
5. **AI Response**: GPT-4 uses the relevant chunks to generate accurate answers

## Technology Stack

- **Frontend**: Next.js, React, TypeScript
- **Vector Database**: Qdrant
- **AI**: OpenAI GPT-4 and embeddings
- **Document Processing**: LangChain

## Troubleshooting

**Common Issues:**

- **"Failed to index file"**: Check your OpenAI API key and ensure Qdrant is running
- **"No documents found"**: Make sure to upload documents before chatting
- **Connection errors**: Verify Docker is running and Qdrant is accessible at `localhost:6333`

**Check if Qdrant is running:**
```bash
curl http://localhost:6333/collections
```

**Restart the application:**
```bash
docker-compose down
docker-compose up -d
npm run dev
```

## Environment Variables

Required variables for `.env.local`:

```env
# Qdrant Vector Database
QDRANT_URL=http://localhost:6333          # Local Docker setup
# QDRANT_API_KEY=your_key                 # Only needed for Qdrant Cloud

# OpenAI API
OPENAI_API_KEY=sk-your_openai_key_here    # Required for embeddings and chat
```

## API Endpoints

- `POST /api/index-text` - Add text content
- `POST /api/index-file` - Upload and process files  
- `POST /api/index-website` - Scrape website content
- `POST /api/chat` - Chat with your documents
- `GET /api/rag-store` - Get document statistics
- `DELETE /api/delete-index` - Clear all documents

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - see LICENSE file for details
