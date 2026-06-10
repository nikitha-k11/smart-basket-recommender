# smart-basket-recommender

A price-aware, nutrition-coherent hybrid recommender system that predicts a user's weekly grocery basket.
Built to fix two real gaps in current retail ML systems:
- Recommending items outside a user's budget
- Recommending junk food to health-conscious shoppers

---
## The Problem
Ever noticed that grocery apps don't care about your budget?
I added healthy items to my cart — fiber, protein, whole foods.
The app recommended chips and candy.

I once had a $5 chicken go out of stock.
The substitution? A $15 one. No warning. No budget-friendly alternative.

Current retail recommenders optimize for **basket size and margin** — not for you.
This project fixes that.

---

## The Solution
A hybrid recommender that combines three signals:

| Signal | What It Does |
|---|---|
| Collaborative Filtering | Finds users with similar shopping patterns |
| Nutrition Scoring | Boosts healthy items for health-conscious users |
| Price Tier Scoring | Penalizes premium items for budget-conscious users |

---

## Results
| Metric | Baseline (CF only) | Hybrid | Improvement |
|---|---|---|---|
| Precision@10 | 0.0127 | 0.0140 | +10.5% |
| Recall@10 | 0.0110 | 0.0155 | +41.0% |
| NDCG@10 | 0.0154 | 0.0184 | +19.5% |

---

## Dataset
**Instacart Online Grocery Shopping Dataset 2017**
- 3.4M orders
- 206K users
- 49K unique products
- 32M+ prior order interactions

---

## 🏗️ Architecture

    Raw Data (6 CSV files)
            ↓
    Product Intelligence Layer
    ├── Nutrition Category  →  healthy / junk / neutral
    └── Price Tier          →  budget / mid / premium
            ↓
    User Behavior Layer
    ├── healthy_ratio   (0 = all junk, 1 = all healthy)
    ├── budget_ratio    (0 = all premium, 1 = all budget)
    └── reorder_rate    (habit signal)
            ↓
    Hybrid Recommender Engine
    ├── Collaborative Filtering  (KNN, cosine similarity)
    ├── Nutrition Alignment Score
    └── Price Alignment Score
            ↓
    Personalized Weekly Basket

---

## Visualizations
### Product Intelligence Layer
![Product Intelligence](charts/product_intelligence.png)

### Personalization in Action — Same Algorithm, Different Users
![Hybrid Recommendations](charts/hybrid_recommendations.png)

### Model Evaluation — Hybrid vs Baseline
![Evaluation Results](charts/evaluation_results.png)

---

## Key Insight
Two users. Same algorithm. Completely different baskets.

| Rank | User 5 — Healthy + Budget | User 1966 — Junk + Premium |
|---|---|---|
| 1 | Organic Granny Smith Apple | India Pale Ale |
| 2 | Banana | Beer |
| 3 | Yellow Onions | Longboard Island Lager |
| 4 | Organic Baby Broccoli | Cabernet Sauvignon Wine |
| 5 | Bag of Organic Bananas | Blueberries |

This is what **real personalization** looks like.

---

##  Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| Pandas, NumPy | Data processing |
| Scikit-learn | KNN model, cosine similarity |
| Scipy | Sparse matrix operations |
| Matplotlib | Visualizations |

---

## How to Run
1. Download the Instacart dataset from [Kaggle](https://www.kaggle.com/datasets/psparks/instacart-market-basket-analysis)
2. Upload to your Kaggle notebook or local environment
3. Open `notebook/smart_basket_recommender.ipynb`
4. Run all cells top to bottom

---

## Business Context
Current retail recommenders (Kroger, Walmart, Instacart) optimize for:
- Basket size
- Margin
- Promotion lift

They do **not** optimize for:
- Your budget
- Your nutrition goals
- Your household health

This project addresses the two most impactful gaps:
- **Price-insensitive substitutions** — recommending a $15 item when you bought $5
- **Nutrition-incoherent recommendations** — suggesting chips when your cart signals healthy

---

## Author

**Nikitha Kurapati**
Data Scientist | MS Computer Science — University of Cincinnati
[LinkedIn](https://www.linkedin.com/in/nikitha-kurapati) | [GitHub](https://github.com/nikitha-k11)
