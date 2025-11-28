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
```bash
git clone <your-repo-url>
cd project
```

### 2. Create a virtual environment
```bash
uv venv
```


### 3. Activate the environment

macOS / Linux
```bash
source .venv/bin/activate
```
Windows
```bash
.venv\Scripts\activate
```

### 4. Install dependencies

This project uses a `pyproject.toml`, so install everything using:
```bash
uv sync
```


---

## Environment Variable (Optional)

The frontend uses the following environment variable:
```bash
API_URL=http://localhost:8000/get-sentiment
```

If not set, it defaults to the same value.

---

## Running the Application

### 1. Start the FastAPI backend
```python
uvicorn backend.main:app --reload --port 8000
```

### 2. Start the Streamlit frontend
```python
streamlit run frontend/app.py
```


### 3. Open the application in your browser
```bash
http://localhost:8501
```

---

## API Example

### Endpoint: POST /get-sentiment

**Request Body:**
```yaml
{
"review": "The movie was amazing!"
}
```

**Response Example:**
```markdown
{
"sentiment": 1,
"confidence": 0.97,
"all_confidence": [0.03, 0.97]
}
```


---

## Logging

All logs are handled through:

config/logger.py

Logging includes:

- Model loading messages
- Incoming request logs
- Prediction and error details

---

## Model Files

Place your HuggingFace model folders inside the `artifacts/` directory:

roberta-sentiment-tokenizer/
roberta-sentiment-analysis/


These must include files such as:

- config.json
- tokenizer.json
- vocab files (if required)
- pytorch_model.bin

---

## License

MIT License (or your preferred license)
