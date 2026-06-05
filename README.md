# AI-Powered Resume Screening System

An intelligent system that automatically analyzes resumes and ranks candidates according to a job description using NLP and Machine Learning techniques.

---

## Project Overview

This project builds a resume screening system that:
- Takes a **job description** and **job category** as input from the user
- Scans a dataset of **2484 real resumes** across **24 job categories**
- Extracts skills and detects years of experience from each resume
- Scores every resume using **TF-IDF** and **Cosine Similarity**
- Ranks candidates by a **weighted final score** and displays the top 10

---

## Demo Output

```
==================================================
      AI RESUME SCREENING SYSTEM
==================================================

Category  : INFORMATION-TECHNOLOGY
JD length : 14 words

Running screening...

   Screening 120 resumes for: INFORMATION-TECHNOLOGY
   TF-IDF matrix: 120 resumes x 5000 terms

==================================================
        TOP 10 CANDIDATES
==================================================

 Rank       ID  Final_score  Similarity_score  Skill_ratio  Experience_years  Skills_found
    1 37242217        23.10            0.0555       0.3590                18   cisco, cloud, java, linux, sql, ...
    2 83816738        21.70            0.0802       0.5128                 3   agile, aws, git, java, python, sql, ...
   ...
```

---

## Concepts Used

| Concept | Description |
|---|---|
| NLP | Tokenization, lemmatization, stopword removal using NLTK |
| Resume Parsing | Reading and processing resume text from CSV dataset |
| Skill Extraction | Matching resume tokens against curated skill profiles |
| Experience Detection | Regex-based extraction of years of experience |
| TF-IDF | Term Frequency-Inverse Document Frequency vectorization |
| Cosine Similarity | Mathematical similarity between JD and resume vectors |
| Candidate Ranking | Weighted scoring combining similarity, skills, and experience |

---

## Tech Stack

- **Python 3**
- **Google Colab**
- **Pandas** — data loading and manipulation
- **NumPy** — numerical operations
- **NLTK** — NLP pipeline (tokenization, lemmatization, stopwords)
- **Scikit-learn** — TF-IDF vectorizer and cosine similarity
- **Regex** — experience detection

---

## Dataset

**Resume.csv** — 2484 resumes across 24 job categories

| Column | Description |
|---|---|
| ID | Unique candidate identifier |
| Resume_str | Plain text resume content |
| Resume_html | HTML formatted resume (not used) |
| Category | Job category label |

**24 Categories:**
ACCOUNTANT, ADVOCATE, AGRICULTURE, APPAREL, ARTS, AUTOMOBILE, AVIATION,
BANKING, BPO, BUSINESS-DEVELOPMENT, CHEF, CONSTRUCTION, CONSULTANT,
DESIGNER, DIGITAL-MEDIA, ENGINEERING, FINANCE, FITNESS, HEALTHCARE,
HR, INFORMATION-TECHNOLOGY, PUBLIC-RELATIONS, SALES, TEACHER

---

## How to Run

### Step 1 — Open in Google Colab
Upload `AI_POWERED_RESUME_SCREENING.ipynb` to [colab.research.google.com](https://colab.research.google.com)

### Step 2 — Upload the dataset
Click the **folder icon** on the left sidebar in Colab and upload `Resume.csv`

### Step 3 — Run all cells in order
Run cells **1 through 8** from top to bottom.
> Cell 3 takes ~45 seconds to clean all 2484 resumes — this is normal.

### Step 4 — Enter your inputs in Cell 8
```
Enter job category: INFORMATION-TECHNOLOGY

Enter job description (press Enter twice when done):
We are looking for a Python developer with experience in machine learning,
SQL databases, TensorFlow, and REST APIs.
[blank Enter to submit]
```

---

## Scoring Formula

The final score is calculated as a weighted combination of three signals:

```
Final Score = (Cosine Similarity × 0.60
            + Skill Match Ratio  × 0.30
            + Experience Score   × 0.10) × 100
```

| Signal | Weight | What it measures |
|---|---|---|
| TF-IDF Cosine Similarity | 60% | Overall text match between resume and JD |
| Skill Match Ratio | 30% | Fraction of required skills found in resume |
| Experience Score | 10% | Years of experience (normalised, capped at 20) |

---

## Project Structure

```
📁 AI-Resume-Screening/
│
├── AI_POWERED_RESUME_SCREENING.ipynb   ← main notebook
├── README.md                           
└── dataset/
    └── Resume.zip                      ← dataset (upload to Colab)
```

---

## Sample Job Descriptions to Test

**INFORMATION-TECHNOLOGY**
```
We are looking for a software developer with strong experience in Python and Java.
The candidate must have knowledge of SQL databases, Linux, and REST APIs.
Experience with cloud platforms like AWS and version control using Git is required.
```

**HR**
```
Looking for an HR Manager with experience in recruitment and talent acquisition.
The candidate must have knowledge of payroll management, HRIS systems, and compliance.
Strong skills in employee relations, onboarding, and performance management required.
```

**FINANCE**
```
We need a Finance Analyst with strong knowledge of accounting and financial reporting.
The candidate must have experience in budgeting, forecasting, and audit.
Knowledge of SAP, Excel, and ERP systems is required.
```

---

## Limitations

- No frontend — runs entirely inside Google Colab
- Category must be specified manually by the user
- Scores are relative within the category pool, not absolute percentages
- Dataset resumes do not contain real candidate names

---

## Future Improvements

- Integrate an external skills database (e.g. SkillNer) for more accurate skill extraction
- Add Part-of-Speech filtering to further clean keyword profiles
- Build a simple web interface using Streamlit
- Support PDF resume uploads for evaluating individual candidates
