### NexusChat --- Intelligent AI Chat Assistant - https://docs.google.com/document/d/1jWuliGox0ghSwMQEByIUeFO5-qxbxdjZC2VfG3ObOw8/edit?usp=sharing

NexusChat is a web-based AI chat application designed to help users ask
questions, manage conversations, and work with documents in one place.
The interface includes a conversation sidebar, model selector, message
composer, and areas for documents and settings. 

**Project status:** Development in progress. Features below are
planned or in progress unless they have been tested end to end in the
current version. 

### Overview

The goal of NexusChat is to provide a familiar chat experience with
reliable AI responses and useful document-based question answering. The
project is intended to use a modular architecture so AI providers,
document processing, and user-facing features can be improved
independently. 

### Screenshots


### Features

* **AI chat:** Send prompts and continue conversations in a chat-style
interface.
* **Conversation management:** Start new chats and return to previous
conversations.
* **Model selection:** Google Gemini support, with OpenAI integration
planned or optional.
* **Document management:** Upload and manage supported documents.
* **Document question answering (RAG):** Retrieve relevant passages
from uploaded documents to ground answers in source material.
* **User accounts:** Sign-in, protected API routes, and account
settings.
* **Responsive interface:** A dark chat layout designed for desktop
and smaller screens.
* **Diagnostics and error handling:** Clear feedback for connection
failures, invalid configuration, and provider limits.

Actual availability depends on which features are implemented and
enabled in the current codebase. 

### Technology Stack

Area                           Technology 

Frontend                       React, Vite, JavaScript, Tailwind CSS
Backend                        Python, FastAPI, Uvicorn
Database                       PostgreSQL
Database access / migrations   SQLAlchemy and Alembic, if configured
Vector search                  pgvector, when enabled
AI providers                   Google Gemini; OpenAI integration planned or optional 

Check the current source code and dependency files for the exact
versions and enabled components. 

### Architecture

text

User's browser
     |
     v
React + Vite frontend
     |
     | HTTPS requests
     v
FastAPI backend
     |             \
     |              \--> Gemini / OpenAI APIs
     v
PostgreSQL
     |
     \--> pgvector document embeddings (if enabled)

Use code with caution.

The frontend should call the backend through a configurable API base
URL. AI provider keys must stay on the server and must never be exposed
in browser code. 

### Example Project Structure

Adjust this example to match the actual repository layout. 

text

NexusChat/
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.js
├── backend/
│   ├── app/
│   ├── main.py
│   └── requirements.txt
├── Screenshot 2026-10-10 171834.png
├── Screenshot 2026-10-10 172551.png
├── README.md
└── .gitignore

Use code with caution.

### Local Development

### Requirements

* Node.js and npm
* Python version supported by the backend dependencies
* PostgreSQL
* Git

### 1. Clone the repository

Replace the URL with your actual GitHub repository URL. 

bash

git clone https://github.com/YOUR_GITHUB_USERNAME/NexusChat.git
cd NexusChat

Use code with caution.

### 2. Start the frontend

Open a terminal in the frontend directory: 

bash

npm install
npm run dev

Use code with caution.

Vite will print the local development URL, commonly
http://localhost:5173. 

### 3. Start the backend

Open a second terminal in the backend directory. Create and activate a
virtual environment: 

bash

python -m venv .venv

Use code with caution.

On Windows PowerShell: 

powershell

.venv\Scripts\Activate.ps1
pip install -r requirements.txt

Use code with caution.

Start the API using the entry point configured in your project. For
example, if the FastAPI instance is named app in main.py: 

bash

uvicorn main:app --reload

Use code with caution.

This command is only an example. Check the actual backend entry point
before using it. 

### 4. Environment variables

Create a local .env file in the location expected by your backend. Use
the exact variable names required by your code. Common examples are: 

env

DATABASE_URL=your_postgresql_connection_string
JWT_SECRET_KEY=replace_with_a_long_random_secret
GEMINI_API_KEY=your_gemini_api_key
OPENAI_API_KEY=your_openai_api_key

Use code with caution.

These names are examples and may differ from your implementation. Never
commit real secrets to GitHub. Add .env to .gitignore; use an
.env.example file with placeholder values only. 

### 5. Database setup

Make sure PostgreSQL is running and the connection string points to the
correct database. If the project uses Alembic, apply the configured
migrations. If pgvector is required and available, enable it in the
target database: 

sql

CREATE EXTENSION IF NOT EXISTS vector;

Use code with caution.

### Response Quality and Document Grounding

For dependable responses, the application should: 

1. Validate the request and confirm that the selected provider and
model are supported.
2. Keep provider credentials on the backend.
3. Handle timeouts, quota limits, rate limits, and provider errors with
clear messages.
4. Retrieve relevant document passages before answering
document-specific questions.
5. Show source references when available and say when documents do not
contain enough information.
6. Avoid claiming that a file was processed if extraction or indexing
failed.

AI output can still be incorrect. Important information should be
verified. 

### Security

* Never commit .env files, API keys, access tokens, or passwords.
* Hash passwords on the server; never store plaintext passwords.
* Protect private endpoints with authentication and check ownership
for every conversation and document.
* Validate upload types and file sizes.
* Store uploaded files outside public web directories or use private
object storage.
* Restrict CORS to trusted frontend origins in production.
* Avoid logging secrets or unnecessary private document contents.
* Use HTTPS for the deployed application.

### Deployment Plan

A possible hosting arrangement is: 

* **Frontend:** Vercel or another static frontend host.
* **Backend:** Render or another host that supports a FastAPI service.
* **Database:** Managed PostgreSQL with pgvector support if vector
search is required.
* **Documents:** Persistent disk or private object storage.

Before deployment, configure the production database, environment
variables, CORS origins, frontend API URL, file storage, and migrations.
Test login, AI provider calls, chat persistence, document uploads, and
document retrieval using the deployed URLs. 

### Testing Checklist

* [ ] Frontend installs and builds successfully.
* [ ] Backend starts and connects to PostgreSQL.
* [ ] Login and protected API routes behave correctly.
* [ ] New chats and previous messages work as expected.
* [ ] Gemini requests use the intended model and handle errors.
* [ ] OpenAI works if its integration is enabled.
* [ ] Documents upload, persist, and can be managed by their owner.
* [ ] Document questions use retrieved content and do not invent
citations.
* [ ] User data is isolated between accounts.
* [ ] No secrets are exposed in the frontend bundle or Git history.
* [ ] Production deployment works after a refresh and a new login.

### Contributing

Keep changes focused and test them locally before pushing. When adding a
feature, update this README so it reflects what is actually implemented.
Do not mark a feature as complete until it has been tested through the
frontend, backend, and any required database or provider integrations. 

### License

No license has been selected yet. Unless a license is added to this
repository, do not assume that others have permission to reuse, modify,
or distribute the code.
