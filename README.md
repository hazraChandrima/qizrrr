# 📄 PDF & Text to Quiz Generator

Automatically generate quizzes from **PDF documents** or **text inputs** using OpenAI's GPT API. This FastAPI-based backend allows you to extract content and generate relevant questions that can be used in educational apps, study tools, or interactive learning platforms.

## ✨ Features

- Extracts content from PDF files and converts it into quiz questions.
- Accepts raw text input and turns it into multiple-choice quizzes.
- ⚡FastAPI-powered backend with async processing for efficiency.
- Flexible: Use individual APIs or run both under one server.


## 📦 Installation & Setup

1. **Clone the repository and install dependencies**
   ```bash
   git clone --depth=1 https://github.com/hazraChandrima/qizrrr.git
   cd qizrrr/
   pip install -r requirements.txt
   ```

2. **Create a .env file in the root directory to store your OpenAI credentials:**
   ```ini
   OPENAI_API_KEY=your_openai_api_key
   IP_ADDRESS=your_local_ip_address
   ```


## 🚀 How to Run the API

### Option 1: Run Both Functionalities in a Unified API (Recommended)
This runs both PDF to Quiz and Text to Quiz endpoints under a single FastAPI server on port 8000:

```bash
uvicorn main:app --host 127.0.0.1 --port 8000 --reload
```

Access:
- PDF to Quiz: POST http://127.0.0.1:8000/pdf_to_quizz/
- Text to Quiz: POST http://127.0.0.1:8000/text_to_quizz/



### Option 2: Run APIs Separately
You can also run each API independently on different ports:


1. **Move to the src/api directory and run the following commands**
   ```bash
   cd ./src/api/
   ```


PDF to Quiz (Port 8000):
```bash
uvicorn api_pdf:app --host 127.0.0.1 --port 8000 --reload
```

Text to Quiz (Port 8001):
```bash
uvicorn api_text:app --host 127.0.0.1 --port 8001 --reload
```


## 🧪 How to Use the API

### PDF to Quiz
**Endpoint:**
POST /pdf_to_quizz/

**cURL Example:**
```bash
curl -X POST "http://127.0.0.1:8000/pdf_to_quizz/?num_questions=5" \
  -H "accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@path_to_your_pdf/sample.pdf"
```

**Query Parameter:**
- num_questions (optional, default is 5, min=1, max=20)

### Text to Quiz
**Endpoint:**
POST /text_to_quizz/

**cURL Example:**
```bash
curl -X POST "http://127.0.0.1:8000/text_to_quizz/" \
  -H "Content-Type: application/json" \
  -d '{
    "content": "The mitochondria is the powerhouse of the cell.",
    "num_questions": 3
}'
```

**JSON Payload:**
- content: Raw input text
- num_questions: Number of questions to generate (min=1, max=20)