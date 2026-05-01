![chainlit1](https://github.com/antima2001/Llama3/assets/118009457/ec5c54c2-c5fd-4a8a-8176-d9a6b4c3acd9)

### PDF Q&A Chatbot using Chainlit + LangChain + Ollama

This project is a conversational PDF question-answering chatbot built using Chainlit, LangChain, Ollama, and ChromaDB.

#### It allows users to:

1. Upload a PDF file
2. Automatically process and embed its content
3. Ask natural language questions
4. Get context-aware answers with source references

#### Feature
1. 📂 Upload PDF via UI
2. 🧠 Retrieval-Augmented Generation (RAG)
3. 💬 Conversational memory (chat history aware)
4. 🔍 Source document tracing
5. ⚡ Local LLM inference using Ollama
6. 🧩 Chunking + semantic search using ChromaDB

| Component   | Tool Used        |
| ----------- | ---------------- |
| UI          | Chainlit         |
| LLM         | Ollama (LLaMA3)  |
| Embeddings  | nomic-embed-text |
| Vector DB   | Chroma           |
| Framework   | LangChain        |
| PDF Parsing | PyPDF2           |

#### ⚙️ How It Works (Architecture)
**1. File Upload**
1. User uploads a PDF through Chainlit UI.
2. File is stored temporarily.

**2. Text Extraction**
1. PyPDF2 reads the PDF.
2. Extracts raw text from all pages.

**3. Text Chunking**
1. RecursiveCharacterTextSplitter splits text into chunks:
2. Chunk size: 1200
3. Overlap: 50

**👉 This improves retrieval accuracy.**

**4. Embeddings Generation**
Each chunk is converted into vector embeddings using:
```bash
nomic-embed-text (Ollama)
```

**5. Vector Storage**
Embeddings are stored in:
```bash
Chroma Vector Database
```

**6. Conversational Retrieval Chain**

#### Uses:

1. ChatOllama (llama3)
2. Retriever from Chroma
3. Conversation memory

**👉 Enables context-aware Q&A**

**7. Query Processing**
User asks a question
System:
1. Retrieves relevant chunks
2. Sends them to LLM
3. Generates answer

#### 📦 Installation
**1. Clone the Repository**
```bash
git clone https://github.com/your-username/pdf-chatbot.git
cd pdf-chatbot
```

**2. Install Dependencies**
```bash
pip install -r requirements.txt
```

**3. Install & Run Ollama**

Make sure Ollama is installed and running:
```bash
ollama pull llama3
ollama pull nomic-embed-text
ollama run llama3
```

**4. Run the App**
```bash
chainlit run app.py
```

#### 🔑 Key Components Explained

**Conversational Memory**
```text
ConversationBufferMemory
```
1. Stores chat history
2. Allows follow-up questions

**Vector Store**
```
Chroma.from_texts()
```
1. Stores embeddings
2. Enables semantic search

**Retrieval Chain**
```text
ConversationalRetrievalChain
```

**Combines:**
1. LLM
2. Retriever
3. Memory

**Async Execution**
```bash
await chain.ainvoke()
```
1. Enables non-blocking UI
2. Better user experience

#### 📌 Example Use Cases

1. 📚 Research paper Q&A
2. 📄 Resume analysis
3. 🏢 Company documents chatbot
4. 📑 Legal / policy document assistant

#### ⚠️ Limitations
1. Works best with text-based PDFs
2. Scanned PDFs may fail (no OCR)
3. Entire PDF loaded in memory (not optimized for huge files yet)

#### 🔮 Future Improvements
1. Add OCR support (Tesseract)
2. Persistent vector DB (disk-based Chroma)
3. Multi-file support
4. Streaming responses
5. Better UI/UX (chat history panel, tabs)
