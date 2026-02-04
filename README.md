Here’s a **clean, professional README** you can drop directly into your backend repo.
It’s written to sound **industry-grade**, **hackathon-appropriate**, and **judge-friendly**.

---

# Customer Value Prediction Backend

This repository contains the **backend service** for predicting **customer future spend** and **purchase likelihood** using transaction-derived features.
The service exposes a REST API built with **FastAPI**, integrates a **trained machine learning model**, and augments predictions with **LLM-based business insights**.

---

## 🚀 Features

* Predicts **future spend over the next 30 days**
* Estimates **probability of purchase in the next 30 days**
* Uses a **trained ML regression model** (`model.pkl`)
* Applies a **heuristic-based intent signal** (recency + frequency)
* Generates **business-friendly insights and recommended actions** using an LLM
* Production-ready FastAPI architecture
* Deployed on **Render**

---

## 🧠 Model Overview

The trained model was built using the following customer-level features:

| Feature       | Description                   |
| ------------- | ----------------------------- |
| Recency       | Days since last purchase      |
| Frequency     | Number of transactions        |
| Total Spend   | Cumulative spend              |
| Average Spend | Average spend per transaction |

At inference time, the API **explicitly selects and orders these features** to match the model’s training configuration, ensuring correctness and forward compatibility.

---

## 🏗️ Architecture

1. Client (Frontend / Postman) sends customer features
2. FastAPI backend:

   * Maps input features to model-expected format
   * Runs ML prediction
   * Computes purchase probability (heuristic)
3. Prediction + probability are passed to an LLM
4. LLM returns:

   * Customer segment
   * Business insight
   * Recommended action
5. Structured JSON response returned to client

---

## 📦 Tech Stack

* **FastAPI** – API framework
* **scikit-learn** – ML model inference
* **NumPy** – numerical processing
* **Groq LLM API** – insight generation
* **Uvicorn** – ASGI server
* **Render** – cloud deployment

---

## 📁 Project Structure

```
backend/
├── app.py                # FastAPI application
├── model/
│   └── model.pkl         # Trained ML model
├── requirements.txt
├── .env                  # Environment variables
└── README.md
```

---

## ⚙️ Environment Variables

Create a `.env` file with:

```env
GROQ_API_KEY=your_groq_api_key
```

---

## ▶️ Running Locally

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Start the server

```bash
uvicorn app:app --reload
```

### 3. Open API docs

```
http://127.0.0.1:8000/docs
```

---

## 🌐 Production Deployment (Render)

**Start Command**

```bash
uvicorn app:app --host 0.0.0.0 --port $PORT
```

The backend listens on the port provided by Render and is publicly accessible.

---

## 🔗 API Endpoint

### `POST /predict_customer_value`

#### Request Body

```json
{
  "customer_id": "13085",
  "features": [345.7, 49.3, 7, 12, 5, 4]
}
```

#### Feature Order

```
[
  total_spend,
  avg_spend,
  num_transactions,
  total_units,
  unique_products,
  recency_days
]
```

---

#### Response

```json
{
  "customer_id": "13085",
  "predicted_future_spend_30d": 512.4,
  "purchase_probability_30d": 0.83,
  "customer_segment": "High Value",
  "insight": "Customer shows strong recent engagement and high spending potential.",
  "recommended_action": "Offer personalized promotions or loyalty rewards."
}
```

---

## 📊 Purchase Probability Logic

Purchase probability is computed using a deterministic heuristic:

* **Recency decay** – recent customers are more likely to return
* **Frequency boost** – frequent buyers have higher intent

This signal complements spend prediction by capturing **customer intent**, not just value.

---

## 🧪 Testing

* API tested via **Postman**
* Multiple customer archetypes validated:

  * High-value active
  * At-risk churn
  * New customer
  * Habitual buyer
  * Low-value inactive

---

## 🧩 Design Decisions

* **Model-agnostic API** – inference layer adapts to model features
* **Explicit feature mapping** – avoids silent mismatches
* **Forward-compatible schema** – allows future feature expansion
* **Business guardrails** – prevents unrealistic outputs

---

## 🏁 Summary

This backend demonstrates:

* End-to-end ML inference
* Production-ready API design
* Clear separation of concerns
* Business-aligned outputs
* Cloud deployment best practices

Absolutely — here’s the **updated README section** with a clean, professional **Contributors** block added.
You can paste this directly into your backend README.

---

## 👥 Contributors

This project was developed collaboratively with clearly defined responsibilities:

* **Lakshya Tiwari**
  *Backend Development, Deployment & System Integration*

  * Designed and implemented the FastAPI backend
  * Integrated ML inference and LLM-based insights
  * Handled cloud deployment and end-to-end integration

* **Raghav**
  *Prediction Models (Random Forest & Lasso Regression)*

  * Feature engineering for customer-level modeling
  * Trained and validated regression models
  * Exported trained models for backend inference

* **Paghallavan**
  *Frontend Development & Presentation*

  * Built the TypeScript-based frontend
  * Integrated backend APIs into UI workflows
  * Designed presentation and demo narrative
---
