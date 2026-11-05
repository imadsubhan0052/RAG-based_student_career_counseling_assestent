# RAG-based_student_career_counseling_assestent

# 1. Use Case Description
This project presents a Retrieval-Augmented Generation (RAG) based intelligent assistant designed to help students across various disciplines (Science, Arts, Commerce, etc.) make informed career decisions.
Provide career recommendations based on user interests, qualifications, and goals.
Retrieve and present relevant career data from educational repositories.
Use natural language generation to simulate personalized counselor-like responses.

# 2. Dataset and Preprocessing
The dataset comprises over 500 text chunks extracted from government portals, job sites, and educational blogs. The data is cleaned, deduplicated, and tokenized into chunks of ~100 words. Embeddings are created using Sentence-BERT.
Preprocessing Steps:
Normalization: Converted all data to lowercase and removed punctuations.
Tokenization: Applied sentence and word tokenization.
Embedding Preparation: Used Sentence-BERT to vectorize documents for similarity-based retrieval.
Indexing: All documents were stored in a FAISS index for efficient semantic retrieval.

# 3. System Design and Architecture
The system consists of a retriever (FAISS + Sentence-BERT) and a generator (T5-base). The retriever selects top-k relevant chunks from the dataset, which are passed to the generator to produce context-aware responses.

# 4. Retrieval and Generation Components
Retrieval Component:
Technology Used: FAISS + Sentence-BERT
Function: Retrieves top-k most semantically relevant documents from the corpus based on user query embeddings.
Example: For the query "What career can I pursue with strong math skills?", relevant entries on Data Science, Actuarial Science, and Engineering are retrieved.
Generation Component:
Model Used: Retrivel and generator.
RAG Pipeline: The user query + retrieved context is passed as a prompt to the LLM, which generates personalized recommendations.
Example Output:
"Based on your strong math skills, you may consider becoming a Data Scientist, Actuary, or Quantitative Analyst. Each role requires analytical thinking, statistical knowledge, and problem-solving abilities..."

# 5. Evaluation
Metrics include ROUGE and BERTScore for generation quality and Recall@k for retrieval precision.
ROUGE: ~0.70
BERTScore: ~0.88
Recall@5: 1.0
MRR: 0.96

# 6. Sample Outputs
Q: Can Arts students work in the public sector?
A: Yes, Arts graduates can pursue roles in civil services, social work, education, and NGOs.

Q: Is BBA good for entrepreneurship?
A: BBA offers strong foundations in business management, making it suitable for aspiring entrepreneurs.
# Load dataset:

<img width="720" height="289" alt="image" src="https://github.com/user-attachments/assets/69aff3ff-4500-404b-afdb-3cf1d2e4ae61" />

# Chunking:

<img width="719" height="98" alt="image" src="https://github.com/user-attachments/assets/b8f44011-b87f-4dca-98cc-72a62d7b8162" />


# Embedding:

<img width="720" height="390" alt="image" src="https://github.com/user-attachments/assets/0f2b098f-fe3f-4bdc-a965-a777e4490cc5" />


# Generator model
# 7. Challenges and Limitations
Hallucinations: Restricted generator to retrieved context.
Latency: Acceptable performance on CPU.
Diverse Needs: Extended dataset to include multiple disciplines.

# 8. Future Improvements
- Source highlighting in responses
- Web UI using Streamlit
- Student profile filtering
- Confidence scores
- Speech and multilingual support

# 9. Required Libraries
pip install pandas faiss-cpu sentence-transformers transformers evaluate rouge_score absl-py
import pandas: To load and manage the dataset (career_chunks.csv) containing career-related text information.
from langchain.text_splitter import RecursiveCharacterTextSplitter: To split large career documents into smaller, context-preserving chunks suitable for embedding and retrieval.
from tqdm import tqdm:  To visually track the progress of operations like embedding multiple text chunks.
from sentence_transformers import SentenceTransformer: To convert each text chunk into a dense numerical embedding used for semantic similarity search.
import faiss: To store and efficiently retrieve the most relevant text chunks using vector similarity search during query time.
import numpy:  To manipulate embedding arrays and perform operations like distance/similarity calculations.
from transformers import T5Tokenizer, T5ForConditionalGeneration: To tokenize input and generate context-aware answers to student queries using a T5 generative language model.
from evaluate import load: To compute evaluation metrics like ROUGE and BERTScore for assessing the quality and fluency of generated answers.
import time: To measure response time and latency of the retrieval and generation pipeline.
