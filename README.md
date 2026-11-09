CollegeBot – RAG Chatbot for College Regulations & Syllabus

A Retrieval-Augmented Generation (RAG) chatbot that answers student questions about college regulations (attendance, grading, CGPA, backlogs, exams, fees, hostel, library) and the syllabus of 16 subjects.

It answers only from a verified CSV knowledge base and replies "not found" when a question is outside it, so it does not guess or hallucinate.

AI Mini-Capstone Project · Artificial Intelligence (25CS301) · Category 3.4 – LLMs and Transformer Models

Problem Statement

Information about college rules and syllabus is scattered across many documents. Students cannot find answers quickly, staff answer the same questions every semester, and general chatbots may give confident but wrong rules.

Goal: a chatbot that takes a student's question (spelling mistakes allowed), finds the answer in a knowledge base, and refuses safely when it is not sure.

Input	Process	Output
Student question	Clean → search 5,000 stored Q&As → best match → check score	Answer + matched question + confidence, or "not found"
Core Contribution – Hybrid Retrieval Algorithm

Three scores are combined into one final score:

Method	What it does	Weight
TF-IDF (word match)	Matches whole words	0.30
Character n-grams (3–5 letters)	Survives spelling mistakes (e.g. "attendence")	0.40
MiniLM embeddings + FAISS (meaning)	Matches meaning when wording differs	0.30
S_final = 0.30 × S_word + 0.40 × S_char + 0.30 × S_sem

If S_final ≥ 0.35 the stored answer is returned. Otherwise the bot replies: "Sorry, I could not find this in the college regulations or syllabus. Please contact the Academic Office."

How It Works

Phase 1 – Offline index preparation

Load the CSV knowledge base
Clean questions (lower-case, remove filler words and special symbols)
Build the TF-IDF word matrix
Build the character n-gram matrix
Create MiniLM sentence embeddings (all-MiniLM-L6-v2, 384 numbers per question)
Build the FAISS index

Phase 2 – Online answering

Clean the student's question
Compute word, letter and meaning scores against all stored questions
Combine them into the final score and take the best match
Check the confidence threshold, then return the answer or "not found"
Knowledge Base
File: college_rag_qa_5000.csv
5,000 Q&A rows, 12 categories (Syllabus, CGPA, Attendance, Grading, Academics, Exams, Backlogs, Project, Fees, Placements, Library, Hostel)
Columns: id, category, fact_id, question, answer
To update the bot, edit the CSV and rebuild the index. No model training is needed.
Results

Tested on 800 questions with spelling mistakes and changed wording:

Method	Top-1	Top-3
Word matching only	76.9%	81.4%
Letter matching only	97.2%	98.1%
Hybrid (ours)	97.6%	98.4%
About 3 ms per question
60/60 unrelated questions refused, 300/300 college questions answered (threshold 0.35)
17 of 18 test cases correct (Syllabus 96.5%, other categories 100%)
Remaining errors come from near-identical questions (for example 72% vs 75% attendance) and short forms such as "DBMS" that are not in the dataset
UI Screens (web app)
#	Screen
01	Login
02	Dashboard – chatbot overview
03	Chat assistant with retrieval details
04	Knowledge base (5,000 Q&A)
05	Index builder – Phase 1
06	Retrieval lab – hybrid score breakdown
07	Accuracy report
08	Threshold and weights settings
09	Query logs and unanswered questions
10	Category analytics

You can add screenshots here, for example ![Login](screenshots/01_login.png).

Tech Stack
Language: Python
Environment: Google Colab
Libraries: pandas, scikit-learn (TF-IDF), sentence-transformers (all-MiniLM-L6-v2), FAISS
Getting Started
bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. Install dependencies
pip install pandas scikit-learn sentence-transformers faiss-cpu

# 3. Open the notebook (Google Colab or Jupyter) and run all cells
#    Make sure college_rag_qa_5000.csv is in the same folder
Example
Student : I have 72% attendance can i write exam
CollegeBot : With 72% attendance: You can apply for condonation with valid proof and a fee.
             (confidence 0.87)

Student : What is the weather today?
CollegeBot : Sorry, I could not find this in the college regulations or syllabus.
             Please contact the Academic Office.   (confidence 0.25)
Limitations
The sample dataset is small and covers only the college's regulations and syllabus
Answers only from the CSV
English only
No conversation memory
Near-identical questions and short forms can still cause errors
Future Scope
Read official PDFs directly
LLM-written, friendlier answers that still follow the rules
Short forms and nicknames (DBMS, OS, CN, ML) added to the dataset
Telugu, Hindi and voice support
Conversation memory
Website and WhatsApp deployment
Team
Name	Roll No.
Vura Nagamani Susmitha	251FA04D58
Vuyyuru Madhuri	251FA04D62
Vuyyuru Hasini	251FA04D60
Chatla Barghava Reddy	251FA04E70
