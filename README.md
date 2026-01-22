# Revenue Optimization Engine for E-commerce

A data-driven pricing optimization system that analyzes 530K+ transactions to identify revenue opportunities through price elasticity analysis.

## 📊 Project Overview

**Business Problem:** How can an e-commerce retailer optimize product pricing to maximize revenue without sacrificing volume?

**Solution:** Built a price elasticity analysis engine that identifies optimal pricing strategies across 2,831 products, projecting **£183K in annual revenue lift** (1.9% increase).

**Tech Stack:** Python, pandas, NumPy, scikit-learn, XGBoost, Matplotlib, Seaborn

---

## 🎯 Key Results

- **£183,000** projected annual revenue increase
- **2,831 products** analyzed with actionable pricing recommendations
- **70% of products** identified as price inelastic → can increase prices 10-15%
- **Top 3 opportunities** generate £45K in revenue lift alone

**Top Revenue Opportunities:**
1. Ceramic Storage Jar: £1.47 → £1.69 (+15%) = **+£16K**
2. White Hanging Heart T-Light: £3.12 → £3.58 (+15%) = **+£15K**  
3. Party Bunting: £5.79 → £6.66 (+15%) = **+£14K**

---

## 🔧 Technical Approach

### 1. Exploratory Data Analysis (`01_eda.ipynb`)
- Analyzed 541,909 transactions from UK-based online retailer (2010-2011)
- Identified and removed 10,624 returns/cancellations (2%)
- Discovered strong seasonality patterns (Q4 revenue peaks)
- Found £9.7M total revenue with 8.6% return rate

**Key Finding:** 84% of transactions fall in £0-5 price range → high-volume, low-margin business model ideal for price optimization.

### 2. Feature Engineering (`02_feature_engineering.ipynb`)
Created 26 pricing features including:
- **Price elasticity** - Correlation between price and quantity (core driver)
- **Seasonality score** - Revenue variation across quarters
- **Price volatility** - Historical pricing flexibility
- **Revenue concentration** - Product importance to overall revenue
- **Pricing tier** - Market positioning (Budget/Mid/Premium/Luxury)

**Price Elasticity Calculation:**
```python
elasticity = correlation(UnitPrice, Quantity)
# Negative = normal demand curve (lower price → higher volume)
# -0.1 to 0 = Inelastic (price insensitive)
# -0.2 to -1.0 = Elastic (price sensitive)
```

### 3. Optimization & Modeling (`03_modeling.ipynb`)

**Approach Evolution:**

**Initial Attempt - ML Predictive Models:**
- Tried Random Forest and XGBoost to predict optimal prices
- **Issue #1:** Data leakage (target derived from features)
- **Issue #2:** Severe overfitting (Train R²=0.98, Test R²=0.78)
- **Issue #3:** Lack of true experimental data (no A/B tests)

**Final Approach - Elasticity-Based Optimization:**

Pivoted to economic theory-based optimization using price elasticity formulas:
```python
def calculate_optimal_price(current_price, elasticity):
    if elasticity > -0.1:  # Inelastic
        return current_price * 1.15  # +15% increase
    elif elasticity < -0.25:  # Highly elastic
        return current_price * 0.95  # -5% to boost volume
    else:  # Moderately elastic
        return current_price * 1.05  # +5% modest increase
```

**Why This Works Better:**
- ✅ Based on established economic principles
- ✅ No overfitting (deterministic, not predictive)
- ✅ Interpretable to business stakeholders
- ✅ Accounts for demand curves via elasticity

---

## 📈 Business Insights

### Product Segmentation by Elasticity

**Inelastic Products (70% of catalog):**
- Demand remains stable despite price changes
- **Strategy:** Increase prices 10-15%
- **Examples:** White Hanging Heart, Party Bunting, Cake Tins
- **Impact:** £150K+ revenue opportunity

**Elastic Products (30% of catalog):**
- Demand highly responsive to price
- **Strategy:** Small discounts or promotions to drive volume
- **Examples:** Jumbo bags, storage bags
- **Impact:** Volume-based revenue growth

### Implementation Priority Framework

**High Priority (20 products):**
- High volume (500+ orders)
- Clear elasticity signal
- **Impact:** £120K revenue lift (66% of total opportunity)

**Medium Priority (100+ products):**
- Moderate volume (100-500 orders)
- **Impact:** £50K revenue lift

**Low Priority (remaining):**
- Lower volume or unclear signals
- **Impact:** £13K revenue lift

---

## 📁 Project Structure
```
RevEngine/
├── data/
│   ├── raw/                    # Original dataset (not tracked)
│   └── processed/              # Clean data & features
├── notebooks/
│   ├── 01_eda.ipynb           # Exploratory analysis
│   ├── 02_feature_engineering.ipynb  # Feature creation
│   └── 03_modeling.ipynb       # Optimization approach
├── README.md
└── requirements.txt
```

---

## 🚀 How to Run

1. **Clone the repository:**
```bash
git clone https://github.com/YOUR-USERNAME/RevEngine.git
cd RevEngine
```

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Download the dataset:**
- Get the [Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail)
- Place `Online_Retail.xlsx` in `data/raw/`

4. **Run notebooks in order:**
- `01_eda.ipynb` - Explore the data
- `02_feature_engineering.ipynb` - Build features
- `03_modeling.ipynb` - Generate pricing recommendations

---

## 💡 Key Learnings

1. **Price elasticity is the key driver** - 70% feature importance in attempted ML models confirmed elasticity dominates pricing decisions

2. **Not every problem needs ML** - Tried predictive models but elasticity-based optimization using economic theory proved more appropriate and interpretable

3. **Business context matters** - Understanding that this is a high-volume, low-margin business shaped the entire analysis

4. **Data quality is critical** - Removing returns, handling missing CustomerIDs, and filtering to products with sufficient data was essential

---

## 🔮 Next Steps

- [ ] Build Streamlit dashboard for business users to explore recommendations
- [ ] A/B test top 20 products to validate projections
- [ ] Implement dynamic pricing based on seasonality patterns
- [ ] Expand to include competitor pricing data

---

## 📝 Lessons: When ML Isn't the Answer

This project demonstrates an important data science principle: **the best solution isn't always the most complex one.**

While machine learning is powerful, this problem was better solved through:
- Statistical analysis (price-quantity correlations)
- Economic theory (elasticity optimization)
- Domain knowledge (retail pricing strategies)

The attempted ML models suffered from fundamental issues (data leakage, lack of experimental data) that couldn't be solved without true A/B test results. Recognizing when to pivot from ML to statistical/theoretical approaches is a critical skill.

---

## 📧 Contact

**Your Name** - Nikhil Thamma
LinkedIn: https://www.linkedin.com/in/nikhilthamma/
Portfolio: https://nikhilthamma.replit.app/
