# Statupbox AI-Powered Sports Quiz Generation Agent

An interactive, production-ready web application built using Python, Streamlit, and an LLM orchestration layer. The agent uses Retrieval-Augmented Generation (RAG) to generate factually grounded multiple-choice quizzes by combining historical data from a local vector store with live news from the internet.

---

## 🏗️ Architecture & Core Concepts
- **Retrieval-Augmented Generation (RAG)**: Acts like an "open-book exam" for the AI, pulling text context before prompting the LLM to eliminate hallucinations.
- **Local Knowledge Store**: Powered by ChromaDB, which vectorizes historical sports data using mathematical embeddings.
- **Live Knowledge Retrieval**: Powered by DuckDuckGo Search to fetch real-time match results and tournament updates dynamically.

---

## 📁 Project Directory Structure
Maintain this exact folder setup to ensure clean code separation:

```text
sports-quiz-agent/
├── .env                  # Hidden file containing sensitive API keys
├── requirements.txt      # List of project dependencies to install
├── README.md             # Guide on installation and execution
├── app.py                # Front-end UI (coordinates everything)
├── data/
│   └── sports_facts.json # Local historic database (raw facts in JSON)
├── chroma_db/            # Created automatically by ChromaDB for vectors
└── src/
    ├── __init__.py       # Treats src as an importable module
    ├── config.py         # Handles API keys and pathing configurations
    ├── database.py       # Interacts only with ChromaDB (Insert & Query)
    ├── search.py         # Interacts only with DuckDuckGo Search API
    └── generator.py      # Combines contexts, builds prompt, and runs LLM
```

---

## 🛠️ Installation & Setup Instructions

### 1. System Prerequisites
- **Python Version**: Use Python 3.9, 3.10, or 3.11. Avoid Python 3.12+ to ensure clean compilation of older ChromaDB C-dependencies.
- **API Access**: An active OpenAI API Key (or Google Gemini API Key) loaded with prepaid credits.

### 2. Workspace Initialization
Open your terminal inside your project directory and configure your isolated environment:

```bash
# Initialize project folder
cd sports-quiz-agent

# Build a virtual environment
python3 -m venv venv

# Activate the virtual environment
source venv/bin/activate
```

### 3. Install Dependencies
Populate your `requirements.txt` file with the exact version requirements and run the installation:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Configure Private Variables
Create a hidden file named `.env` in the root directory:
```bash
nano .env
```
Paste your secret key inside without spaces or quotes:
```env
GEMINI_API_KEY=AQ.Ab......yourActualSecretKeyHere
```
*(Crucial Note: Always add `.env` and `chroma_db/` to a `.gitignore` file before pushing code to GitHub to avoid automated key revoking).*

### 5. Establish the Knowledge Base
Ensure your raw sports facts are added to `data/sports_facts.json`. The database will initialize, vectorize, and persist itself locally inside the `chroma_db/` folder on your first database operations execution.

---

## 💻 Running the Application

Start the interactive Streamlit user dashboard from the root directory:
```bash
streamlit run app.py
```

### How to use the Dashboard:
1. Select a **Sport** and target **Difficulty Level** from the sidebar controls.
2. Click the generate action button to orchestrate data aggregation.
3. The RAG engine will instantly combine database history and live news into custom questions.
4. Answer the multiple-choice questions in the UI and receive automated, contextual explanations.
