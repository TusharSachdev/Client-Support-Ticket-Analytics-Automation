# 🎟️ Ticket Category Predictor

A machine learning-based web app that predicts the category of a support ticket based on its **subject** and **description**. Built using `scikit-learn`, deployed via `Streamlit` and tunneled to the internet using `ngrok.`

This tool can serve as a prototype for integrating automated ticket triage systems into helpdesk workflows — particularly within platforms like Odoo ERP, where customer support tickets are routed through the Helpdesk module. By reducing the need for manual ticket categorization, this solution can directly improve response time and team efficiency.

---

## 📌 Table of Contents

- [🔍 Problem Statement](#-problem-statement)
- [🎯 Objectives](#-objectives)
- [🧰 Tools & Technologies Used](#-tools--technologies-used)
- [📂 Dataset Overview](#-dataset-overview)
- [🔬 Data Preprocessing](#-data-preprocessing)
- [🤖 Model Training](#-model-training)
- [📈 Model Evaluation](#-model-evaluation)
- [🧪 Streamlit App](#-streamlit-app)
- [🌐 Ngrok Tunneling in Colab](#-ngrok-tunneling-in-colab)
- [📊 Key Learnings](#-key-learnings)
- [🔮 Future Improvements](#-future-improvements)
- [📄 License](#-license)

---

## 🔍 Problem Statement

Support ticket management systems often categorize tickets manually, which is time-consuming and error-prone. Automating ticket categorization can improve workflow efficiency and help route tickets faster to the appropriate teams.

---

## 🎯 Objectives

- Build a **text classification model** to predict the category of a ticket.
- Preprocess and clean the textual data.
- Train and evaluate the performance of different ML models.
- Deploy the best model using a **Streamlit web interface**.
- Expose the web app publicly via **ngrok** in Google Colab.

---

## 🧰 Tools & Technologies Used

| Tool              | Purpose                              |
|------------------|--------------------------------------|
| Python           | Programming language                 |
| pandas           | Data manipulation                    |
| scikit-learn     | ML modeling, preprocessing           |
| joblib           | Model serialization                  |
| Streamlit        | App interface                        |
| pyngrok          | Public URL tunneling (Colab)         |
| nltk             | Text preprocessing (stopwords)       |

---

## 📂 Dataset Overview

- The dataset consists of support tickets with the following features:
  - `Subject`: Short summary of the issue
  - `Description`: Detailed explanation of the issue
  - `Category`: Target variable (e.g., Hardware, Software, Networking, etc.)

---

## 🔬 Data Preprocessing

- Combined `Subject` and `Description` into a single input text.
- Applied **text cleaning**:
  - Lowercasing
  - Removing punctuation
  - Removing digits
  - Removing stopwords (using `nltk`)
- Vectorized text using `TfidfVectorizer`.

---

## 🤖 Model Training

- Tried multiple models:
  - Logistic Regression
  - Random Forest
  - Multinomial Naive Bayes
- Final model chosen: **Logistic Regression**
- Serialization:
  - Saved model: `ticket_category_model.joblib`
  - Saved vectorizer: `tfidf_vectorizer.joblib`

---

## 📈 Model Evaluation

| Metric        | Score       |
|---------------|-------------|
| Accuracy      | ~88%        |
| F1 Score      | Good for all categories |
| Confusion Matrix | Analyzed for error patterns |

---

## 🧪 Streamlit App

The app allows users to:

- Enter the **subject** and **description** of a ticket.
- Click "Predict Category".
- Get the predicted ticket category instantly.

Sample code from `app.py`:

```python
st.title("Ticket Category Predictor")

subject = st.text_input("Ticket Subject")
description = st.text_area("Ticket Description")

if st.button("Predict Category"):
    if subject and description:
        category = predict_category(subject, description)
        st.success(f"Predicted Category: {category}")
    else:
        st.error("Please enter both subject and description.")

---
