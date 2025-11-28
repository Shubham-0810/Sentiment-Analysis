# Movie Review Sentiment Analysis

This project is an end-to-end sentiment analysis system built using:

- FastAPI for the backend API
- Streamlit for the frontend user interface
- HuggingFace RoBERTa model for text classification
- Scikit-learn Pipeline for preprocessing and inference

The application predicts whether a movie review is positive or negative and returns confidence scores.

---

## Features

### Frontend (Streamlit)

- Text input to enter a movie review
- Sends review text to the backend API for prediction
- Displays:
  - Predicted sentiment (0 = Negative, 1 = Positive)
  - Confidence score for the prediction
  - Confidence scores for all classes

### Backend (FastAPI)

- Loads the RoBERTa model and pipeline during startup
- Provides a POST endpoint at `/get-sentiment`
- Uses Pydantic for request validation
- Returns sentiment predictions in JSON format

### Machine Learning Pipeline

- Uses HuggingFace RoBERTa tokenizer and model
- Includes a preprocessing transformer for cleaning and tokenizing text
- Wraps model inference inside a Scikit-learn pipeline
- Outputs:
  - Predicted sentiment class
  - Softmax probabilities for each class

---

## Installation and Setup (using uv)

### 1. Clone the repository

git clone <your-repo-url>
cd project

shell
Copy code

### 2. Create a virtual environment

uv venv

shell
Copy code

### 3. Activate the environment

macOS / Linux
source .venv/bin/activate

Windows
.venv\Scripts\activate

csharp
Copy code

### 4. Install dependencies

This project uses a `pyproject.toml`, so install everything using:

uv sync

yaml
Copy code

---

## Environment Variable (Optional)

The frontend uses the following environment variable:

API_URL=http://localhost:8000/get-sentiment

yaml
Copy code

If not set, it defaults to the same value.

---

## Running the Application

### 1. Start the FastAPI backend

uvicorn backend.main:app --reload --port 8000

shell
Copy code

### 2. Start the Streamlit frontend

streamlit run frontend/app.py

shell
Copy code

### 3. Open the application in your browser

http://localhost:8501

yaml
Copy code

---

## API Example

### Endpoint: POST /get-sentiment

**Request Body:**

{
"review": "The movie was amazing!"
}

markdown
Copy code

**Response Example:**

{
"sentiment": 1,
"confidence": 0.97,
"all_confidence": [0.03, 0.97]
}

yaml
Copy code

---

## Logging

All logs are handled through:

config/logger.py

yaml
Copy code

Logging includes:

- Model loading messages
- Incoming request logs
- Prediction and error details

---

## Model Files

Place your HuggingFace model folders inside the `artifacts/` directory:

roberta-sentiment-tokenizer/
roberta-sentiment-analysis/

yaml
Copy code

These must include files such as:

- config.json
- tokenizer.json
- vocab files (if required)
- pytorch_model.bin

---

## License

MIT License (or your preferred license)