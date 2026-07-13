# Shopping_agent
 🛍 Intelligent Shopping Agent

> An AI-powered command-line shopping assistant that recommends the best product based on your budget, star ratings, and real customer review sentiment.

---

## 📌 Project Overview

The **Intelligent Shopping Agent** is a beginner-friendly Python project that simulates an AI shopping assistant. Instead of relying on external machine learning libraries, it uses a hand-crafted **multi-factor scoring engine** and **keyword-based sentiment analysis** to evaluate products and surface the best recommendation for any user.

Simply tell the agent your name, pick a product category, and set your budget — the agent does the rest.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🗂 Product Database | 20 sample products across 4 categories stored in JSON |
| 🔍 Smart Search | Filters by category and budget automatically |
| 💬 Review Analysis | Scores each product's reviews using keyword-based sentiment analysis |
| 🏆 Recommendation Engine | Ranks products with a weighted composite score (rating + sentiment + price efficiency) |
| 💡 Plain-English Explanation | Tells the user *why* a product was recommended |
| 🔄 Alternatives | Shows up to 3 runner-up products within budget |
| ✅ Input Validation | Handles invalid input gracefully with helpful error messages |
| 🧱 Zero Dependencies | Runs on Python 3.8+ with no third-party packages |

---

## 🗂 Folder Structure

```
shopping_agent/
│
├── app.py                  ← Main entry point — run this to start the agent
├── requirements.txt        ← Dependency list (standard library only)
├── README.md               ← This file
│
├── data/
│   └── products.json       ← Product database (20 items, 4 categories)
│
└── src/
    ├── __init__.py         ← Makes src a Python package
    ├── utils.py            ← Shared helpers: validation, formatting, display
    ├── product_search.py   ← Loads and filters the product database
    ├── review_analysis.py  ← Keyword-based sentiment scoring of reviews
    └── recommendation.py   ← Weighted scoring engine + recommendation output
```

---

## 🛒 Supported Product Categories

| # | Category | Products in Database |
|---|---|---|
| 1 | Laptop | Dell Inspiron 15, HP Pavilion 14, MacBook Air M2, Lenovo IdeaPad 3, ASUS ZenBook 14 |
| 2 | Mobile | Samsung Galaxy S23, iPhone 14, OnePlus Nord CE 3, Xiaomi Redmi Note 12, Google Pixel 7 |
| 3 | Headphones | Sony WH-1000XM5, Bose QC45, JBL Tune 760NC, AirPods Pro 2, Anker Soundcore Q30 |
| 4 | Smartwatch | Apple Watch S8, Samsung Galaxy Watch 5, Garmin Venu 2, Xiaomi Mi Band 8, Fitbit Versa 4 |

---

## ⚙️ How the Recommendation Engine Works

The agent scores every product that matches your category and budget using three factors:

```
Final Score = (Rating Score  × 0.40)
            + (Sentiment Score × 0.30)
            + (Price Efficiency × 0.30)
```

### Factor Details

| Factor | Weight | How It's Calculated |
|---|---|---|
| **Rating Score** | 40 % | `rating / 5.0` — normalised to 0–1 |
| **Sentiment Score** | 30 % | Keyword hits in reviews → normalised to 0–1 |
| **Price Efficiency** | 30 % | `1 - (price / budget)` — rewards affordable picks |

The product with the **highest composite score** is recommended. Alternatives are shown ranked by score.

---

## 🚀 Installation & Setup

### Prerequisites

- **Python 3.8 or higher** — [Download Python](https://www.python.org/downloads/)
- No third-party packages required.

### 1. Clone or Download the Project

```bash
# Option A — Clone via Git
git clone https://github.com/your-username/shopping-agent.git
cd shopping-agent

# Option B — Download the ZIP and extract it, then navigate to the folder
cd shopping_agent
```

### 2. (Optional) Create a Virtual Environment

```bash
# Create a virtual environment
python -m venv venv

# Activate it
# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

> Since all modules are from the standard library, this step is a no-op — but it's good practice to run it anyway.

---

## ▶️ How to Run

```bash
python app.py
```

### Example Session

```
════════════════════════════════════════════════════════════
  🛍   Intelligent Shopping Agent  v1.0.0
  AI-powered product recommendations tailored to you.
════════════════════════════════════════════════════════════

  Welcome! I will help you find the perfect product
  based on your budget, ratings, and real reviews.

  👤  What is your name? → Alex

  Hello, Alex! Let's find the best product for you.

  ────────────────────────────────────────────────────────
  STEP 1 — Choose a Product Category
  ────────────────────────────────────────────────────────

  Available categories:
    1. Laptop
    2. Mobile
    3. Headphones
    4. Smartwatch

  🔍  Enter category name or number → 1

  ✅  Category selected: Laptop

  ────────────────────────────────────────────────────────
  STEP 2 — Set Your Budget
  ────────────────────────────────────────────────────────

  💵  Your budget (USD) → $900

  ✅  Budget set: $900.00

  ────────────────────────────────────────────────────────
  STEP 3 — Searching Products
  ────────────────────────────────────────────────────────

  Category  : Laptop
  Budget    : $900.00
  Found in category  : 5 product(s)
  Within your budget : 4 product(s)

  ⚙   Analysing reviews and computing scores…

════════════════════════════════════════════════════════════
  🏆  TOP RECOMMENDATION FOR ALEX
════════════════════════════════════════════════════════════

  ✨  ASUS ZenBook 14  —  ASUS
  Category  : Laptop
  Price     : $799.00  (Budget: $900.00)
  Rating    : ★★★★★  (4.5/5)
  Score     : 82.4 / 100

  ────────────────────────────────────────────────────────
  🔧  Key Features
  ────────────────────────────────────────────────────────
  • Intel Core i7
  • 16GB RAM
  • 512GB SSD
  • 14-inch OLED
  • Windows 11
  • Thunderbolt 4

  ────────────────────────────────────────────────────────
  💬  Review Analysis
  ────────────────────────────────────────────────────────
  💬  Sentiment  : Excellent 🌟
  📝  Reviews    : 4 analysed
      Score      : +0.0889  (+12 positive / -2 negative keywords)

  🗣  Top customer quotes:
      ❝ The OLED display is breathtaking. ❞
      ❝ Powerful and portable, great combination. ❞

  ────────────────────────────────────────────────────────
  💡  Why We Recommend This
  ────────────────────────────────────────────────────────
  'ASUS ZenBook 14' is your best match because it carries
  a strong rating of 4.5/5, customer reviews are
  overwhelmingly positive, and it fits comfortably within
  your budget (saving you $101.00). Overall recommendation
  confidence score: 82.4 / 100.

  ────────────────────────────────────────────────────────
  🔄  Other Options Within Your Budget ($900.00)
  ────────────────────────────────────────────────────────
  #2  Dell Inspiron 15  (Dell)  |  $649.00  |  ⭐ 4.2  |  Score: 74.3
  #3  HP Pavilion 14   (HP)    |  $549.00  |  ⭐ 4.0  |  Score: 71.8
  #4  Lenovo IdeaPad 3 (Lenovo)|  $429.00  |  ⭐ 3.8  |  Score: 68.2

════════════════════════════════════════════════════════════
  Happy Shopping! 🛒
════════════════════════════════════════════════════════════
```

---

## 🧩 Module Reference

### `src/utils.py`
Shared helper functions for the entire project.

| Function | Purpose |
|---|---|
| `validate_name()` | Prompts for a non-empty user name |
| `validate_budget()` | Prompts for a positive numeric budget |
| `validate_category()` | Prompts for a valid category (name or number) |
| `format_currency()` | Formats `649` → `$649.00` |
| `get_star_rating()` | Converts `4.2` → `★★★★☆  (4.2/5)` |
| `display_product_card()` | Prints a formatted product summary block |
| `print_header()` | Prints a styled `═══` header |

### `src/product_search.py`
Loads and filters the product database.

| Function | Purpose |
|---|---|
| `load_products()` | Reads and parses `data/products.json` |
| `search_by_category()` | Returns all products matching a category |
| `filter_by_budget()` | Returns products at or below the budget |
| `search_products()` | Full pipeline: load → filter by category → filter by budget |
| `get_search_summary()` | Returns a human-readable search summary string |

### `src/review_analysis.py`
Keyword-based sentiment scoring for product reviews.

| Function | Purpose |
|---|---|
| `analyse_reviews()` | Scores a single product's reviews |
| `analyse_all_products()` | Runs analysis on a full product list |
| `display_review_summary()` | Prints the sentiment report for a product |

### `src/recommendation.py`
Multi-factor scoring engine and recommendation display.

| Function | Purpose |
|---|---|
| `compute_score()` | Calculates composite score for one product |
| `rank_products()` | Sorts a product list by score (highest first) |
| `get_recommendation()` | Full pipeline: sentiment → score → rank → return best |
| `generate_explanation()` | Produces a plain-English recommendation reason |
| `display_recommendation()` | Prints the complete recommendation output |

---

## 🔧 Extending the Project

### Add More Products
Open [`data/products.json`](data/products.json) and add a new entry to the `products` array following the existing schema:

```json
{
  "id": 21,
  "name": "Your Product Name",
  "category": "Laptop",
  "brand": "Brand Name",
  "price": 699,
  "rating": 4.3,
  "features": ["Feature 1", "Feature 2"],
  "reviews": ["Review text 1", "Review text 2"],
  "stock": true
}
```

### Add a New Category
1. Add products with the new category name in `products.json`.
2. Add the category name to `VALID_CATEGORIES` in [`src/utils.py`](src/utils.py).

### Adjust Scoring Weights
Edit the constants at the top of [`src/recommendation.py`](src/recommendation.py):
```python
WEIGHT_RATING    = 0.40   # increase to prioritise star rating
WEIGHT_SENTIMENT = 0.30   # increase to prioritise review quality
WEIGHT_PRICE_EFF = 0.30   # increase to prioritise affordability
```
> The three weights must always sum to `1.0`.

---

## 🐍 Python Concepts Used

This project is an excellent learning resource for:

- **Functions** and modular design (each file is a focused module)
- **Dictionaries and lists** (products stored as dicts)
- **File I/O** (`json.load` for reading the database)
- **Type hints** (`List[Dict]`, `Optional[Dict]`, `Tuple[int, int]`)
- **Input validation** with `while True` loops and `try/except`
- **String manipulation** (sentiment keyword matching)
- **Sorting** with custom `key` functions (`sorted(..., key=lambda p: p["score"])`)
- **Relative imports** and Python package structure (`src/__init__.py`)
- **`os.path`** for cross-platform file paths

---

## 📄 License

This project is released under the [MIT License](https://opensource.org/licenses/MIT).  
Free to use, modify, and distribute for personal and commercial projects.

---

## 🤝 Contributing

Pull requests are welcome! Please open an issue first to discuss significant changes.

---

*Built with ❤️ in Python — no magic, just good engineering.*
