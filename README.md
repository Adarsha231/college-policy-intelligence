🎓 College Policy Intelligence

AI-Powered College Policy Management and Student Assistance System

College Policy Intelligence is an AI-powered application designed to simplify college policy management and improve access to institutional information. It provides a centralized platform where administrators can upload and manage policy documents, compare revised policies, and help students retrieve relevant information through an AI-powered chatbot.

The system uses Retrieval-Augmented Generation (RAG) to provide context-based answers from uploaded college policy documents.

---

📌 Problem Statement

College policies and institutional guidelines are generally distributed across multiple PDF documents, circulars, and notices.

Students often face difficulties finding specific information from lengthy documents, while administrators spend considerable time managing policy revisions and identifying changes between different versions.

The absence of a centralized intelligent platform can also lead to students accessing outdated information.

💡 Proposed Solution

College Policy Intelligence provides a centralized AI-powered platform that:

- Allows administrators to upload and manage college policy PDF documents.
- Automatically extracts and processes information from uploaded PDFs.
- Compares previous and revised policy versions.
- Identifies added, removed, and modified policy information.
- Allows students to ask questions using natural language.
- Retrieves relevant information from active policy documents using RAG.
- Provides policy-related answers based on retrieved document content.

---

✨ Key Features

👨‍💼 Administrator Module

- Secure administrator authentication.
- Upload college policy PDF documents.
- Manage policy documents.
- Maintain policy version history.
- Automatically compare previous and updated policy documents.
- Generate policy comparison reports.
- Store policy update notification records.

🎓 Student Module

- Secure student authentication.
- Student dashboard.
- AI-powered policy chatbot.
- Ask questions about college rules and regulations.
- Retrieve information from active policy documents.
- Access policy documents through the application.

🤖 AI-Powered Features

- PDF text extraction.
- Intelligent document chunking.
- Text embedding generation.
- Semantic similarity search.
- Retrieval-Augmented Generation (RAG).
- Automatic policy version comparison.
- Active policy version filtering.

---

🛠️ Technology Stack

Technology| Purpose
Flutter & Dart| Frontend development
Node.js| Backend runtime
Express.js| REST API development
Python| AI and document processing
FastAPI| AI service APIs
MongoDB Atlas| Application database
ChromaDB| Vector database
Sentence Transformers| Text embeddings
all-MiniLM-L6-v2| Embedding model
Groq| LLM inference
JWT| Authentication
Firebase| Push notifications

---

🏗️ System Architecture

The application follows a three-layer architecture.

1. Frontend – Flutter: Provides the user interface for students and administrators.
2. Backend – Node.js and Express: Handles authentication, authorization, API requests, database operations, and communication with the AI service.
3. AI Service – Python and FastAPI: Handles PDF processing, embeddings, vector retrieval, answer generation, and policy comparison.

Architecture Workflow

             STUDENT / ADMIN
                    |
                    v
             FLUTTER FRONTEND
                    |
                    v
           NODE.JS + EXPRESS
                    |
          +---------+---------+
          |                   |
          v                   v
      MONGODB              FASTAPI
    APPLICATION              AI
      DATABASE             SERVICE
                              |
                 +------------+------------+
                 |            |            |
                 v            v            v
              PDF          CHROMADB      GROQ
           PROCESSING      VECTOR DB      LLM
                 |            |            |
                 +------------+------------+
                              |
                              v
                       AI RESPONSE
                              |
                              v
                       FLUTTER UI

---

🔄 Working Methodology

1. Policy Document Upload

- Administrator logs into the application.
- Selects a policy PDF document.
- Provides the corresponding policy name.
- Flutter sends the document to the Express backend.
- Express forwards the document to the FastAPI AI service.

2. PDF Processing and Ingestion

The AI service performs the following operations:

1. Receives the uploaded PDF.
2. Validates the document.
3. Extracts text from the PDF.
4. Divides the extracted text into smaller chunks.
5. Generates embeddings using Sentence Transformers.
6. Stores the chunks and embeddings in ChromaDB.

Chunking Configuration:

- Chunk Size: 500
- Chunk Overlap: 100
- Embedding Model: all-MiniLM-L6-v2

3. Automatic Policy Comparison

When an administrator uploads a revised version of an existing policy:

- The backend identifies the previous document using its policy name.
- The old and new document IDs are forwarded to the AI comparison service.
- The system compares the policy contents.
- A comparison report is generated and stored in MongoDB.

The comparison report contains:

- Summary
- Added content
- Removed content
- Modified content
- Potential conflicts

4. Student AI Chatbot

When a student asks a question:

1. The question is submitted through the Flutter interface.
2. Express forwards the request to FastAPI.
3. The question is converted into an embedding.
4. ChromaDB searches for semantically relevant policy chunks.
5. Only active policy versions are considered during normal student retrieval.
6. Retrieved information is supplied as context to the Groq LLM.
7. The LLM generates a natural-language response.
8. The response is returned to the student.

---

🧠 Retrieval-Augmented Generation (RAG)

The project uses Retrieval-Augmented Generation to provide answers based on uploaded college policy documents.

RAG combines two major processes:

1. Retrieval

ChromaDB retrieves relevant policy information using vector similarity search.

2. Generation

The Groq-configured LLM uses the retrieved information as context to generate a natural-language response.

Why RAG?

- Provides document-grounded answers.
- Reduces dependence on the LLM's general training knowledge.
- Allows policy information to be updated without retraining the LLM.
- Supports retrieval from active policy versions.
- Helps students access information from lengthy documents.

---

🗄️ Database Management

The project uses two databases for different purposes.

MongoDB Atlas

Stores:

- User information.
- Policy document metadata.
- Document references.
- Policy comparison reports.
- Notification records.

ChromaDB

Stores:

- Extracted policy text chunks.
- Text embeddings.
- Document metadata.
- Active policy document registry.

Active Policy Version Management

The system uses two ChromaDB collections:

- "college_policies" – Stores chunks from all uploaded policy versions.
- "active_college_policies" – Maintains the active document ID for each policy.

This allows the system to retain historical policy versions for comparison while restricting normal student retrieval to the active version.

---

📁 Project Structure

college-policy-intelligence/
│
├── ai-service/
│   └── Python / FastAPI AI service
│
├── backend/
│   └── Node.js / Express backend
│
├── data/
│   └── Project data
│
├── frontend/
│   └── Flutter application
│
├── tests/
│   └── Project tests
│
└── README.md

---

⚙️ Installation and Setup

Prerequisites

Make sure the following tools are installed:

- Flutter SDK
- Dart SDK
- Node.js and npm
- Python 3
- MongoDB Atlas account
- ChromaDB
- Git

1. Clone the Repository

git clone https://github.com/Adarsha231/college-policy-intelligence.git

cd college-policy-intelligence

2. Start the Backend

cd backend
npm install
npm run dev

The backend runs on:

http://localhost:5000

3. Start the AI Service

Open another terminal:

cd ai-service

Install the Python dependencies using the project's dependency file and configure the required environment variables.

Start FastAPI:

uvicorn app.main:app --reload --port 8000

AI service URL:

http://localhost:8000

Health check:

curl http://localhost:8000/

4. Start the Flutter Frontend

Open another terminal:

cd frontend

Install Flutter dependencies:

flutter pub get

Run the application:

flutter run -d chrome

Note: Configure the required MongoDB connection string, JWT secret, Groq API key, Firebase credentials, and service URLs using the project's environment configuration. Never commit API keys, passwords, or credentials to GitHub.

---

🔐 Authentication and Authorization

The application uses JSON Web Tokens (JWT) for authentication.

- "protect" middleware verifies authenticated requests.
- "adminOnly" middleware restricts administrator-specific operations.
- Students and administrators have different access permissions.
- Backend authorization protects sensitive operations.

---

🚀 Advantages

- Centralized college policy management.
- Reduces manual searching through lengthy PDF documents.
- Natural-language access to college information.
- Automatic comparison of policy revisions.
- Maintains historical policy versions.
- Helps prevent retrieval from outdated policy documents.
- Separates frontend, backend, and AI responsibilities.
- Provides role-based access control.

---

🔮 Future Enhancements

- OCR support for scanned policy documents.
- Multilingual student queries.
- Improved PDF table and layout extraction.
- Student feedback and response evaluation.
- Administrator audit logs.
- Improved policy comparison accuracy.
- Automated testing of document upload and retrieval workflows.
- More reliable push notification delivery.

---

📊 Project Status

The project has demonstrated MongoDB connectivity, backend startup, FastAPI health checks, PDF ingestion, and policy activation in the development tests.

Some functionality still requires further verification:

- Student chatbot retrieval encountered a ChromaDB API compatibility error.
- Firebase push notification delivery failed in the observed test.
- Complete end-to-end functionality requires additional testing.

---

👨‍💻 Repository

GitHub: https://github.com/Adarsha231/college-policy-intelligence

---

🎯 Conclusion

College Policy Intelligence aims to transform traditional college policy management into an intelligent and centralized system.

By combining Flutter, Node.js, Python, MongoDB, ChromaDB, and Retrieval-Augmented Generation, the application provides administrators with tools to manage and compare policy documents while helping students retrieve institutional information through an AI-powered chatbot.
