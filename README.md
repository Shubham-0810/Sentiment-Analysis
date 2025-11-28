🎬 Movie Review Sentiment Analysis

A complete end-to-end sentiment analysis system built using:

FastAPI (backend API)

Streamlit (frontend UI)

HuggingFace RoBERTa (transformer model)

Scikit-learn Pipeline (preprocessing + model wrapper)

The system predicts whether a movie review is Positive or Negative, along with confidence scores for each class.

📁 Project Structure
project/
│
├── frontend/
│   └── app.py                     # Streamlit UI
│
├── backend/
│   └── main.py                    # FastAPI backend API
│
├── pipeline/
│   └── pipeline_module.py         # Preprocessing + model inference pipeline
│
├── artifacts/
│   ├── roberta-sentiment-tokenizer/
│   └── roberta-sentiment-analysis/
│
├── config/
│   └── logger.py                  # Logging configuration
│
└── pyproject.toml                 # Dependencies for uv / pip

✨ Features
Frontend (Streamlit)

Input text box for entering a movie review

Calls FastAPI endpoint for prediction

Displays:

Sentiment label

Confidence of predicted class

Confidence scores for all classes

Backend (FastAPI)

Loads the RoBERTa model pipeline at startup

Provides REST endpoint:
POST /get-sentiment

Validates input using Pydantic

Returns structured prediction output

Pipeline

HuggingFace RoBERTa tokenizer + model

Custom preprocessing transformer (lowercasing + tokenization)

Scikit-learn Pipeline wrapper

Outputs:

Predicted label

Softmax probabilities

⚙️ Installation & Setup

This project uses uv for environment management and dependency installation.

1. Clone the Repository
git clone <your-repo-url>
cd project

2. Create a uv Environment
uv venv

3. Activate the Environment
# Linux / macOS
source .venv/bin/activate

# Windows
.venv\Scripts\activate

4. Install Dependencies

Since you have a pyproject.toml, just run:

uv sync


This installs all dependencies defined in the project.

🌐 Environment Variables

The Streamlit app uses:

API_URL=http://localhost:8000/get-sentiment


If not set, it defaults to:

http://localhost:8000/get-sentiment


You can export it if needed:

export API_URL="http://localhost:8000/get-sentiment"

🚀 Running the Application
1. Start the Backend
uvicorn backend.main:app --reload --port 8000

2. Start the Frontend
streamlit run frontend/app.py

3. Open in Browser
http://localhost:8501


Enter a review → Receive sentiment prediction → View confidence scores.

📤 API Usage
POST /get-sentiment
Request
{
  "review": "The movie was amazing!"
}

Response
{
  "sentiment": 1,
  "confidence": 0.97,
  "all_confidence": [0.03, 0.97]
}

📝 Logging

The app uses a centralized logging utility:

config/logger.py


Logs include:

Backend startup events

Model loading status

Incoming reviews

Prediction & errors

📦 Model Files (Important)

Place the following inside the artifacts/ directory:

roberta-sentiment-tokenizer/

roberta-sentiment-analysis/

These must be HuggingFace-style directories containing:

config.json

tokenizer.json

vocab.json (if applicable)

pytorch_model.bin

etc.

Otherwise, the pipeline will not load.

📜 License

Feel free to add a license of your choice (MIT recommended).