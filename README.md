# 🎓 COLLEGE RAG CHATBOT
## Retrieval-Augmented Generation (RAG) Chatbot for College Regulations and Syllabus Queries

---

# 👥 TEAM DETAILS

**Project Batch:** Batch 3

**Institution:** Vignan's Foundation for Science, Technology and Research (VFSTR)

### Team Members

| S. No. | Student Name | Registration Number |
|:---:|---|:---:|
| 1 | V. Nagamani Susmitha | 251FA04D58 |
| 2 | Vuyyuru Hasini | 251FA04D60 |
| 3 | Vuyyuru Madhuri | 251FA04D62 |
| 4 | Chatla Barghava Reddy | 251FA04E70 |

**Project Domain:** Artificial Intelligence, Machine Learning and Natural Language Processing


# 1. PROJECT OVERVIEW

The College RAG Chatbot is an intelligent question-answering system designed to help students find information about college regulations, academic policies, examinations, attendance, grading, fees, hostel facilities, library services and first-semester syllabus-related queries.

College information is often scattered across multiple documents, making it difficult for students to find accurate answers quickly.

This project develops a centralised chatbot that retrieves relevant information from a structured college knowledge base using a hybrid retrieval algorithm.

The system identifies the most relevant stored answer and rejects unrelated questions using a confidence threshold.

# 2. PROBLEM STATEMENT

College rules, academic regulations and syllabus information are distributed across different documents. Students often face difficulties finding accurate information, while faculty and administrative staff repeatedly answer similar questions.

General-purpose chatbots may also provide incorrect or misleading college information.

Therefore, this project aims to develop a College RAG Chatbot that retrieves relevant answers from a structured knowledge base and provides reliable responses to student queries.

# 3. OBJECTIVES

- Build a clean and categorised college question-answer knowledge base.
- Retrieve relevant answers using a hybrid retrieval algorithm.
- Handle different question formats and spelling variations.
- Identify unrelated questions using a confidence threshold.
- Reduce incorrect answers by returning only stored knowledge-base responses.
- Evaluate retrieval performance using appropriate evaluation metrics.
- Develop an interactive chatbot for college-related queries.

# 4. TECHNOLOGIES USED

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Google Colab | Development environment |
| Pandas | Dataset handling |
| NumPy | Numerical operations |
| Scikit-learn | TF-IDF and similarity calculations |
| MiniLM | Semantic sentence embeddings |
| FAISS | Similarity-based vector search |
| Matplotlib | Data visualisation |
| Seaborn | Statistical visualisation |
| IPyWidgets | Interactive chatbot interface |

# 5. DATASET DESCRIPTION

The project uses a structured CSV dataset named `college_rag_qa.csv`.

The dataset contains college-related questions and their corresponding answers, organised into different categories.

### Dataset Information

- Fact ID
- Institution Type
- Category
- Semester
- Subject
- Unit
- Question
- Answer
- Source Type
- Policy Status
- Question Style

### Major Categories

- Attendance
- Examination
- Academic Regulations
- College Administration
- Practical Student Problems
- Syllabus

**Note:** The current notebook contains sample institutional regulations and syllabus information. Official college documents must replace the sample information before real-world deployment.

# 6. ALGORITHM – HYBRID RETRIEVAL

The project uses a Hybrid Retrieval Algorithm that combines three different techniques to improve question matching.

### 6.1 Word-Level TF-IDF

TF-IDF (Term Frequency–Inverse Document Frequency) identifies similarities between words and phrases in student queries and stored questions.

It uses word n-grams of sizes 1 and 2.

### 6.2 Character-Level TF-IDF

Character N-gram TF-IDF identifies similarities at the character level.

It uses character n-grams from 3 to 5 characters and helps handle spelling mistakes and variations in student queries.

### 6.3 MiniLM Sentence Embeddings

MiniLM converts sentences into numerical vector representations.

It identifies semantic similarities between questions, even when they use different words but express similar meanings.

### 6.4 FAISS Similarity Search

FAISS is used to perform efficient similarity searches over the generated sentence embeddings.

### Final Hybrid Score

The final retrieval score is calculated using:

S_final = w_word × S_word + w_char × S_char + w_sem × S_sem

Where:

- S_word = Word-level similarity score.
- S_char = Character-level similarity score.
- S_sem = Semantic similarity score.
- w_word, w_char and w_sem = Experimentally selected weights.

The weights are selected through validation experiments rather than assuming fixed optimal values.

# 7. TEXT PREPROCESSING

Before retrieving answers, the chatbot performs text preprocessing.

The preprocessing steps include:

1. Converting text into lowercase.
2. Removing unnecessary punctuation.
3. Normalising spaces.
4. Removing common filler words.
5. Expanding common student abbreviations.
6. Preserving important technical terms, numbers and unit information.

This helps improve the matching process between student queries and stored questions.

# 8. PROJECT WORKFLOW

1. Collect and load the college question-answer dataset.
2. Perform data cleaning and preprocessing.
3. Conduct Exploratory Data Analysis (EDA).
4. Generate word-level TF-IDF features.
5. Generate character-level TF-IDF features.
6. Generate MiniLM sentence embeddings.
7. Build the FAISS similarity search index.
8. Combine the retrieval scores using the hybrid algorithm.
9. Select retrieval weights and confidence threshold using validation data.
10. Retrieve the most relevant stored answer.
11. Reject unrelated questions.
12. Evaluate the chatbot using testing queries.

### System Architecture

Student Query → Text Preprocessing → Word-Level TF-IDF + Character-Level TF-IDF + MiniLM Embeddings → Hybrid Similarity Score → Best Matching Question → Confidence Threshold Check → Retrieved Answer / Information Not Available

# 9. CONFIDENCE-BASED ANSWER VALIDATION

The chatbot uses a confidence threshold to determine whether a retrieved answer is sufficiently relevant.

- If the confidence score meets the selected threshold, the corresponding stored answer is returned.
- If the confidence score is below the threshold, the chatbot rejects the query.
- Unrelated questions are not answered using random or invented information.

This mechanism helps reduce incorrect responses.

# 10. TESTING AND EVALUATION

The project evaluates the chatbot using different types of questions, including:

- Exact questions.
- Paraphrased questions.
- Questions containing spelling mistakes.
- Short and long questions.
- Unrelated questions.
- College-related hard-negative questions.

### Evaluation Metrics

| Metric | Purpose |
|---|---|
| Top-1 Accuracy | Measures whether the best retrieved result is correct |
| Top-3 Accuracy | Checks whether the correct result appears among the top three |
| Precision | Measures the correctness of accepted answers |
| Recall | Measures the proportion of answerable queries accepted |
| F1-Score | Measures the balance between precision and recall |
| Rejection Accuracy | Measures correct rejection of unrelated queries |
| Response Latency | Measures the average response time |

The notebook performs validation-based parameter selection and evaluates final performance on a held-out test dataset.

# 11. EXPECTED OUTCOMES

- Retrieve relevant answers to college-related questions.
- Handle different question formats and spelling variations.
- Improve question matching using hybrid retrieval techniques.
- Reject unrelated questions using confidence-based filtering.
- Provide an interactive question-answering system.
- Evaluate retrieval performance through quantitative metrics.

# 12. LIMITATIONS

- The current prototype mainly focuses on B.Tech first-semester information.
- The dataset contains sample institutional regulations and syllabus information.
- Retrieval accuracy depends on the quality of the knowledge base.
- Similarity-based retrieval may sometimes confuse closely related questions.
- The current system supports English queries only.
- The chatbot does not access individual students' attendance or academic records.
- No LLM is used to generate or invent college regulations; answers are retrieved from the CSV knowledge base.

# 13. FUTURE SCOPE

The project can be enhanced through the following improvements:

- Integration of official college PDF documents.
- Support for Telugu and Hindi languages.
- Voice-based question answering.
- Coverage of all semesters and departments.
- LLM-based answer generation with citations to retrieved records.
- Website and WhatsApp deployment.
- Integration with college databases.
- Improved retrieval accuracy through larger and verified datasets.

# 14. HOW TO RUN THE PROJECT

1. Open the notebook in Google Colab.
2. Install the required dependencies.
3. Import the necessary Python libraries.
4. Upload the `college_rag_qa.csv` dataset when prompted.
5. Execute the notebook cells in sequence.
6. Perform dataset preprocessing and exploratory data analysis.
7. Build the hybrid retrieval model.
8. Execute the testing and evaluation sections.
9. Open the interactive chatbot.
10. Enter college-related questions and view the retrieved answers.

### Required Dependencies

- pandas
- numpy
- scikit-learn
- sentence-transformers
- faiss-cpu
- matplotlib
- seaborn
- ipywidgets

# 15. CONCLUSION

The College RAG Chatbot demonstrates how hybrid information retrieval techniques can be used to provide relevant answers to student queries.

By combining word-level TF-IDF, character-level TF-IDF and MiniLM semantic embeddings with FAISS similarity search, the system improves its ability to identify relevant questions.

The confidence-based rejection mechanism helps prevent the chatbot from answering unrelated queries.

This project provides a foundation for developing a more comprehensive college information assistant that can be expanded using official institutional documents and advanced AI technologies.

---

## PROJECT INFORMATION

**Project Title:** Retrieval-Augmented Generation (RAG) Chatbot for College Regulations and Syllabus Queries

**Project Batch:** Batch 3

**Institution:** Vignan's Foundation for Science, Technology and Research

**Programming Language:** Python

**Development Platform:** Google Colab

**Project Domain:** Artificial Intelligence and Natural Language Processing

**Project Type:** Academic Capstone Project

---

**Developed by Team Batch 3**
