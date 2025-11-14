#  Robot Adviser — NLP-Powered Product Review Website

**Turning noisy customer feedback into clear buying decisions.**

Robot Adviser is an **end-to-end NLP system** that classifies product reviews, clusters products into meaningful groups, and generates human-like product recommendation articles using **state-of-the-art LLMs**.

This repository contains the full workflow:  
data preprocessing → model training → evaluation → deployment.

---
## Data Folder

The repository includes a dedicated **`data/`** folder containing:

- The **raw datasets** used as input for the project  
- The **cleaned CSV files** generated after each preprocessing step  
- Intermediate datasets:
  - After noise removal (Model 1)
  - After clustering assignment (Model 2)
  - After summary generation metadata (Model 3)

This ensures complete transparency and reproducibility across all stages of the pipeline.

---

##  Project Goals

This project aims to **automate product review analysis** using modern NLP:

1. **Sentiment Classification**  
   Classify customer reviews into **positive, neutral, or negative** sentiment to help businesses understand customer satisfaction.

2. **Product Clustering**  
   Group products into **4–6 meta-categories** using unsupervised learning, enabling easier category insights and recommendation grouping.

3. **AI-Generated Product Summaries (LLMs)**  
   Use extractive + abstractive **Generative AI models** to summarize thousands of reviews into:
   - buyer-friendly articles  
   - top product recommendations per category  

    *Only LLMs were used for summarization — no classical techniques.*

---

## 🏗 System Architecture

```
[Architecture diagram text already shown in conversation]
```

---

## 1. Sentiment Classification (Model 1)

**Goal:** predict whether a review is *positive*, *neutral*, or *negative*.

### Techniques Used
- TF-IDF vectorization  
- Support Vector Machine (LinearSVC)  
- Class imbalance strategies (class weights)  
- **LLM-based noise removal:**  
  - Detect mismatches between *text sentiment vs star rating*  
  - Remove rows caused by **errors or sarcasm**

### Results  
- **F1 Macro:** 0.71  
- **F1 Weighted:** 0.97  
- Noise reduced from **67k → 60k reviews**

---

## 2. Product Clustering (Model 2)

**Goal:** group products into **4–6** meaningful categories.

### Pipeline  
- Text cleaning and preprocessing  
- TF-IDF vectorization  
- K-Means clustering  
- k-selection using:
  - Elbow method  
  - Silhouette score  

### Results  
- Final clusters: **6 meta-categories**  
- Evaluation metrics:  
  - Silhouette: **0.283** (fair)  
  - Davies-Bouldin: **1.71**  
  - Balanced cluster sizes  

---

##  3. Review Summarization (Model 3)

**Goal:** transform thousands of reviews into **clear, useful product recommendations**.

### Two-step LLM pipeline
1. **Extractive Summary**  
   - Model: `distilbert-base-nli-mean-tokens` (SBERT)

2. **Abstractive Summary**  
   - Model: `facebook/bart-large-cnn`  
   - + LoRA optimization for faster fine-tuning

### Evaluation
- **ROUGE-1:** 0.34  
- **ROUGE-2:** 0.09  
- **BERTScore F1:** 0.88–0.89  

---

##  Deployment

The models were integrated into a **Streamlit demo website** that enables users to:
- Upload datasets  
- View sentiment distribution  
- Explore meta-clusters  
- Generate summaries and final product recommendation articles  

---

##  Repository Structure

```
├── clean data
├── data
├── notebooks/
│   ├── m1.ipynb
│   ├── m2.ipynb
│   └── m3.ipynb
├── models/
├── app/
│   └── streamlit_app.py
├── utils/
└── README.md
```

---

##  Team (Group 5)

- Inna 
- Adrián  
- Khushboo    
- Ralitza  

---

##  Key Takeaways

- Noise removal (sarcasm + mistakes) significantly improved sentiment classification.  
- Clustering required tuning metrics and validating cluster stability.  
- LLM summarization produced high-quality recommendation articles.  
- Full workflow integrated preprocessing → modeling → deployment.  
- Team collaborated both individually and collectively through iterations.

---

## 📖 License

MIT License.
