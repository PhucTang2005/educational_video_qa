![demo](./docs/images/demo.png)

# Educational Video QA System

### Course Project – CS431: Deep Learning Techniques and Applications
### University of Information Technology – VNU-HCM (UIT)
### Lecturer: Dr. Nguyễn Vinh Tiệp

This project implements an intelligent question-answering system for educational videos using a Retrieval-Augmented Generation (RAG) pipeline. It enables users to upload video lectures, index their content, and ask natural-language questions which the system answers based on retrieved video segments.

## System Pipeline

1. Extract audio transcript from educational videos
2. Extract visual features from video frames
3. Convert multimodal information into structured JSON documents
4. Chunk and index documents using vector embeddings
5. Retrieve relevant content using Hybrid Search (Vector + BM25)
6. Rerank retrieved chunks
7. Generate answers using LLM-based RAG pipeline
8. Evaluate system performance with RAGAS benchmark

## Team Members

| No. | Full Name         | Student ID | Responsibilities                                                                                                                                                                                                                           |
| --- | ----------------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | Pham Nguyen Tuong | 23521751   | Project leader. Designed benchmark dataset from educational videos with 100 QA pairs and references, performed evaluation using RAGAS, and integrated LLM-based answer generation from processed multimodal features.                      |
| 2   | Chuong Hong Van   | 23521769   | Developed visual processing pipeline, implemented demo workflow, and integrated visual/audio feature extraction pipelines into unified Jupyter Notebook processing for JSON-based feature generation used by the RAG system.               |
| 3   | Tang Hoang Phuc   | 23521219   | Developed audio processing pipeline, extracted speech transcripts from educational videos, and prepared transcript-based semantic features for multimodal retrieval and question answering.                                                |

## Features

-   Upload and manage educational videos
-   Intelligent question answering based on video content
-   Workspace management and video organization
-   Semantic search using vector embeddings
-   BM25-based reranking
-   User authentication with JWT

## Evaluation & Experimental Results

We evaluated our RAG pipeline using the **RAGAS framework** across different retrieval and generation configurations. The evaluation focuses on how well the system retrieves relevant context and generates accurate answers.

| Method / Pipeline | Faithfulness | Context Precision | Context Recall | Answer Correctness |
| :--- | :---: | :---: | :---: | :---: |
| **BM25 + Gemini** | 0.9170 | 0.8261 | 0.8167 | 0.6059 |
| **dangvantuan/vietnamese-embedding + Gemini** | 0.7631 | 0.6800 | 0.6880 | 0.5590 |
| **hiieu/halong_embedding + Gemini** | 0.9181 | **0.9400** | 0.8894 | 0.6351 |
| **hiieu/halong_embedding + BM25 + Gemini** | 0.9437 | 0.8776 | **0.9192** | 0.6353 |
| **hiieu/halong_embedding + BAAI/bge-reranker-base + Gemini** | **0.9497** | 0.8800 | 0.8967 | **0.6391** |

> *Note: The best performing score for each metric is highlighted in **bold**.*

## Tech Stack

### Backend
-   FastAPI
-   MongoDB (Motor)
-   LangChain + ChromaDB
-   Google Gemini
-   Sentence Transformers
-   PyTorch + OpenCV

### Frontend
-   React + TypeScript
-   Vite
-   Ant Design
-   TanStack Query
-   Axios

## System Requirements

-   Python 3.9+
-   Node.js 18+
-   MongoDB
-   FFmpeg

## Installation and Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd educational_video_qa
### 2. Backend Setup

```bash
cd backend

python -m venv venv
source venv/bin/activate     # macOS/Linux
# or: venv\Scripts\activate  # Windows

pip install -r requirements.txt

cp .env.example .env

fastapi run app/main.py
```

Backend URL:

```
http://localhost:8000
```

Documentation:

```
http://localhost:8000/docs
```

### 3. Frontend Setup

```bash
cd frontend

npm install
cp .env.example .env

npm run dev
```

Frontend URL:

```
http://localhost:5173
```

## Usage

1. Access the frontend interface
2. Register or log in
3. Create a workspace
4. Upload an educational video
5. Ask questions based on the video content

## Project Structure

```
educational_video_qa/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── models/
│   │   ├── schemas/
│   │   ├── services/
│   │   └── utils/
│   └── storage/
├── frontend/
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── apiServices/
│       └── types/
└── README.md
```

## Environment Variables

### Backend `.env`

```
MONGODB_URL=mongodb://localhost:27017
MONGODB_DATABASE=educational_video_qa
SECRET_KEY=your-secret-key-change-this-in-production
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=43200
UPLOAD_DIR=./storage/videos
CHROMA_PERSIST_DIR=./storage/chroma_db
GEMINI_API_KEYS=your-gemini-api-key,...
```

### Frontend `.env`

```
VITE_API_BASE_URL=http://localhost:8000
```

## Scripts

### Backend

```bash
fastapi run app/main.py
```

### Frontend

```bash
npm run dev
npm run build
npm run preview
```

## Contributing

This project is developed as part of
**CS431 – Deep Learning Techniques and Applications**
University of Information Technology – VNU-HCM.

## License

MIT License
