# 🎬 AI Video Assistant (Meeting Intelligence & Analytics Platform)

An intelligent meeting assistant that extracts insights, summaries, and action items from meeting video/audio files or YouTube links, and lets you chat with your meeting using Retrieval-Augmented Generation (RAG).

---

## 🚀 Key Features

* **Flexible Input Sources**: Paste a YouTube URL or path to a local audio/video file.
* **Dual-Language Transcription**:
  * **English**: Runs a local **OpenAI Whisper** model.
  * **Hinglish/Hindi**: Uses **Sarvam AI's translation API** to transcribe and translate Hindi/Hinglish speech to English.
* **Automated Meeting Analytics (via Mistral AI)**:
  * Short, professional title generation.
  * Map-reduce transcript summarisation.
  * Structured Action Item extraction (Task, Owner, Deadline).
  * Key Decisions tracker.
  * Unresolved Questions / Follow-ups tracker.
* **Conversational RAG Chat**: Ask questions directly about the meeting transcript using a local **Chroma DB** vector store and HuggingFace's `all-MiniLM-L6-v2` embeddings.
* **Interactive UIs**:
  * **Streamlit App**: Clean, premium, dark-themed dashboard.
  * **CLI**: A terminal-based pipeline and chat interface.

---

## 🛠️ Architecture & Project Structure

```text
├── core/
│   ├── transcriber.py     # Local Whisper & Sarvam AI routing
│   ├── summarizer.py      # Map-reduce summary & title generation
│   ├── extractor.py       # Action items, decisions, and questions extraction
│   ├── vector_store.py    # Text splitter, embeddings, and Chroma DB configuration
│   └── rag_engine.py      # LCEL LangChain RAG pipeline
├── utils/
│   └── audio_processor.py # Video/audio downloading (yt-dlp) and conversion (pydub/ffmpeg)
├── app.py                 # Streamlit web interface
├── main.py                # Command-line interface
├── requirements.txt       # Project dependencies
└── .gitignore             # Excluded files
```

---

## ⚙️ Prerequisites & Setup

### 1. Install FFmpeg
The audio processor relies on **FFmpeg** to convert media files to wav format.
* **Windows**: Download from [ffmpeg.org](https://ffmpeg.org/download.html), extract it, and add the `bin/` directory to your system's environment `Path` variable.
* **macOS**: Run `brew install ffmpeg`
* **Linux**: Run `sudo apt install ffmpeg`

### 2. Install Project Dependencies
Initialize a virtual environment and install the required Python libraries:
```bash
# Create virtual environment
python -m venv .venv

# Activate virtual environment
# Windows (PowerShell):
.venv\Scripts\Activate.ps1
# macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory and configure your API keys:
```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key

# Optional settings
WHISPER_MODEL=small             # Choices: tiny, base, small, medium, large
SARVAM_STT_MODEL=saaras:v3
```

---

## 🏃 Running the Application

### Option A: Streamlit Dashboard (Recommended)
Launch the interactive web application:
```bash
streamlit run app.py
```
Open **[http://localhost:8501](http://localhost:8501)** in your web browser.

### Option B: Terminal CLI
Execute the terminal-based interface:
```bash
python main.py
```

---

## 📦 Core Technologies Used
* **Frontend**: [Streamlit](https://streamlit.io/)
* **AI Orchestration**: [LangChain](https://www.langchain.com/) (LCEL)
* **LLM**: [Mistral AI API](https://mistral.ai/)
* **Local Embeddings**: [Sentence-Transformers](https://huggingface.co/sentence-transformers) (`all-MiniLM-L6-v2`)
* **Vector Store**: [Chroma DB](https://www.trychroma.com/)
* **Speech to Text**: [OpenAI Whisper](https://github.com/openai/whisper) & [Sarvam AI](https://www.sarvam.ai/)
* **Media Handling**: `yt-dlp` & `pydub`
