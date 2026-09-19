# AI_SHIFA_HOSPITAL_ASSISTANT
🏥 Hospital RAG Assistant

A clean and interactive Hospital Knowledge Base RAG application built with Streamlit, FAISS, Sentence Transformers, and Groq GPT-OSS 120B.

The application allows an authorized department user to ask questions and receive answers based only on the relevant documents stored in the hospital knowledge base.

Important: The hospital documents used in this project are synthetic/practice documents. They are not official hospital policies and should not be treated as medical advice.

✨ Features

🏥 Clean hospital-themed Streamlit interface

💬 Interactive chat interface

🔎 Semantic document retrieval using FAISS

🧠 Sentence Transformer embeddings

🤖 Groq openai/gpt-oss-120b for answer generation

🔐 Department-specific document filtering

📚 Shows the documents used to generate each answer

🔑 Groq API key is read securely from Streamlit Secrets

💊 Medicine-themed UI element

🚑 Ambulance/emergency-themed UI element

🩺 Patient safety section

📝 Admissions section

🏢 Hospital operations section

💾 Chat history maintained during the Streamlit session

🧠 How the RAG System Works

The application follows this flow:

User Question
      ↓
Create Question Embedding
      ↓
Search FAISS Index
      ↓
Filter by Authorized Department
      ↓
Select Relevant Chunks
      ↓
Send Retrieved Context to Groq LLM
      ↓
Generate Answer
      ↓
Display Answer + Source Documents

The LLM is instructed to answer only from the retrieved hospital knowledge-base context and not invent information.

📁 Project Structure

Your project should have this structure:

hospital-rag-assistant/
│
├── app.py
├── requirements.txt
├── README.md
│
└── faiss_index/
    ├── index.faiss
    ├── metadata.pkl
    ├── metadata.json
    └── config.json

File descriptions

File

Purpose

app.py

Main Streamlit application

requirements.txt

Python dependencies

README.md

Project documentation

faiss_index/index.faiss

FAISS vector index

faiss_index/metadata.pkl

Retrieved chunk metadata

faiss_index/metadata.json

Readable metadata

faiss_index/config.json

Index/embedding configuration

📚 Hospital Knowledge Base

The current knowledge base contains these departments:

01_Admissions/
02_Departments/
03_Emergency/
04_Hospital/
05_Patient_Safety/

The department documents are used for retrieval and access filtering.

Department mapping

Folder

Department

01_Admissions

Admissions

02_Departments

Departments

03_Emergency

Emergency

04_Hospital

Hospital Operations

05_Patient_Safety

Patient Safety

🛠️ Technologies Used

Streamlit

Used to create the interactive web application and chat interface.

FAISS

Used for fast similarity search over the stored document embeddings.

Sentence Transformers

The application uses:

sentence-transformers/all-MiniLM-L6-v2

to convert user questions into embeddings.

Groq

Groq is used to generate the final answer using:

openai/gpt-oss-120b

NumPy

Used for numerical processing of embedding vectors.

📦 Installation

Make sure Python is installed.

Install all dependencies using:

pip install -r requirements.txt

The required packages are:

streamlit
groq
faiss-cpu
sentence-transformers
numpy

🔑 Configure Groq API Key

The application does not display an API-key textbox.

The key should be stored using Streamlit Secrets.

Create:

.streamlit/secrets.toml

and add:

GROQ_API_KEY = "your_groq_api_key_here"

Streamlit Cloud

If deploying on Streamlit Cloud:

Open your application.

Open the app settings.

Go to Secrets.

Add:

GROQ_API_KEY = "your_groq_api_key_here"

Save the secret.

Restart/redeploy the application if required.

Never upload your real API key to GitHub or put it directly inside app.py.

▶️ Run the Application

Open a terminal in the project folder and run:

streamlit run app.py

Streamlit will start the application and provide a local URL.

Usually it will be available at:

http://localhost:8501

🔐 Department Access

The application provides a department selector in the sidebar.

Example:

Authorized Department
        ↓
Admissions
        ↓
Only Admissions chunks are passed to the LLM

The retrieval process checks the department stored in the FAISS metadata before adding a chunk to the LLM context.

This prevents chunks from other departments from being included in the answer-generation context.

Important security note

The department dropdown is a demo/project-level access filter. It is not a complete authentication system.

For a production hospital system, users should be authenticated and their authorized department should be assigned server-side rather than allowing users to freely select their department.

🔎 Retrieval Process

When a user asks a question:

The question is converted into an embedding.

FAISS searches the vector index.

Multiple candidate chunks are retrieved.

Chunks belonging to other departments are removed.

The most relevant authorized chunks are selected.

The selected chunks are sent to the Groq model.

The model generates an answer from the supplied context.

The application displays the source documents.

The current application retrieves up to:

TOP_K = 5

relevant authorized chunks.

📚 Source Display

After an answer is generated, the application displays the documents used as context.

The source section can show:

📄 Document name
🏢 Department
📁 Source path

This makes the RAG response easier to verify.

💬 Example Questions

Depending on the selected department, users can ask questions such as:

Admissions

What is the admission procedure?

What documents are required for admission?

Emergency

What is the emergency department procedure?

What should staff do during an emergency escalation?

Patient Safety

What is the patient safety procedure?

How should an incident be reported?

Hospital Operations

What are the hospital visitor policies?

What are the hospital operational procedures?

Departments

What are the responsibilities of hospital departments?

🧪 Important Dataset Note

This project uses a synthetic hospital knowledge base for educational/project purposes.

The application should therefore be presented as a:

Hospital Knowledge Base RAG Demonstration

rather than as a real clinical decision-support system.

The LLM is also instructed not to create information that is not present in the retrieved documents.

⚠️ Troubleshooting

1. FAISS index not found

If you see:

FAISS index not found

make sure the folder is located beside app.py:

app.py
faiss_index/

and that the folder contains:

index.faiss
metadata.pkl
metadata.json
config.json

2. Metadata file not found

Make sure:

faiss_index/metadata.pkl

exists.

The application uses this file to map FAISS results back to their document information.

3. GROQ_API_KEY is not configured

Make sure your Streamlit Secrets contain:

GROQ_API_KEY = "your_groq_api_key_here"

Do not put the key inside the source code.

4. Package installation error

Run:

pip install -r requirements.txt

If using a virtual environment, make sure the environment is activated before installing the packages.

5. Streamlit does not start

Try:

streamlit run app.py

If Streamlit is not recognized, try:

python -m streamlit run app.py

🚀 Future Improvements

Possible future improvements include:

👤 Real user authentication

🔐 Server-side role/department authorization

🗂️ Separate FAISS indexes for each department

📄 PDF and DOCX table extraction

🔄 Document upload and automatic re-indexing

💬 Conversation memory

📊 Admin dashboard

📝 Chat/export history

🔍 Advanced source highlighting

🏥 More hospital departments

🚑 Dedicated emergency workflow

💊 Medicine information module based on approved documents

🌐 Production deployment

📌 Project Summary

This project demonstrates how Retrieval-Augmented Generation (RAG) can be used to build a hospital knowledge assistant.

The system combines:

Hospital Documents
       +
Sentence Transformer Embeddings
       +
FAISS Vector Search
       +
Department Access Filtering
       +
Groq GPT-OSS 120B
       ↓
Grounded Hospital Assistant

The main goal is to provide answers based on retrieved hospital documents while showing the source documents used for each response.

👩‍💻 Project Type

Educational / Academic AI Project

Core concept: Retrieval-Augmented Generation (RAG)

Interface: Streamlit

Vector Database: FAISS

Embedding Model: sentence-transformers/all-MiniLM-L6-v2

LLM: openai/gpt-oss-120b via Groq
