# 🧹 Data Cleaning: Amazon Sales Dataset

![Python](https://img.shields.io/badge/Python-3.x-blue)
![pandas](https://img.shields.io/badge/pandas-Data%20Cleaning-150458)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

**Oasis Infobyte Summer Internship Program (SIP) | Data Analytics | Level 1 | Task 3**

---

## 📌 Overview
Real-world data is rarely analysis-ready. This project takes the raw **Amazon India product dataset** (1,465 rows, 16 columns) and turns it into a clean, validated dataset, with every decision documented and explained.

## 🎯 Objectives
- Audit the raw data and report quality problems
- Fix data types, missing values and duplicates with justified strategies
- Standardise text and split the category hierarchy
- Detect outliers and decide, column by column, whether to keep, cap or remove them
- Prove the improvement with a before vs. after comparison
- Save an analysis-ready dataset

## 🛠️ Tech Stack
| Tool | Purpose |
|---|---|
| Python 3 | Core language |
| pandas, NumPy | Cleaning and transformation |
| Matplotlib, Seaborn | Visualisation |
| Jupyter Notebook | Documentation and execution |

## 📂 Dataset
**Amazon Sales Dataset** (Kaggle): product listings from Amazon India.

| Column | Description |
|---|---|
| `product_id`, `product_name` | Product identifier and title |
| `category` | Pipe-separated category hierarchy |
| `discounted_price`, `actual_price` | Prices in ₹ (stored as text in raw data) |
| `discount_percentage` | Discount (stored as text, e.g. `64%`) |
| `rating`, `rating_count` | Average rating and number of ratings |
| `about_product`, `user_id`, `user_name`, `review_id`, `review_title`, `review_content` | Product description and review details |
| `img_link`, `product_link` | Links |

## 🔍 Problems Found in the Raw Data
| Problem | Detail |
|---|---|
| Numbers stored as text | `₹1,099`, `64%`, `24,269` in 5 columns |
| Missing / invalid values | 2 blank `rating_count` values; 1 non-numeric `rating` |
| Repeated product IDs | 114 rows share a `product_id` |
| Packed category column | `Electronics\|HomeTheater,TV&Video\|...` in one string |

## ⚙️ Cleaning Workflow & Decisions
| Step | Action | Why |
|---|---|---|
| 1 | Data quality report | Find problems before fixing anything |
| 2 | Removed `₹`, `,` and `%`; converted to numeric | Needed for any calculation; `errors="coerce"` exposes bad values as NaN |
| 3 | Filled missing values with the **median** | `rating_count` is highly right-skewed, so the mean would be misleading |
| 4 | Removed duplicate `product_id` rows (kept first) | One row per product needed for product-level analysis |
| 5 | Trimmed text; split `category` into main / sub / leaf | Allows analysis at each category level |
| 6 | Validated ratings (1-5), prices (>0) and discount % vs. prices | Catch silent data errors |
| 7 | IQR outlier detection; **all outliers retained** | High prices and large rating counts are genuine premium and popular products, not errors |
| 8 | Saved `amazon_cleaned.csv` | Analysis-ready output |

## 📊 Before vs After
| Metric | Before | After |
|---|---|---|
| Rows | 1,465 | 1,351 |
| Columns | 16 | 20 (added `main_category`, `sub_category`, `leaf_category`, `discount_amount`) |
| Null values | 2 | 0 |
| Duplicate product IDs | 114 | 0 |
| Numeric columns with correct dtype | 0 of 5 | 5 of 5 |

## 📈 Key Insights from the Cleaned Data
- **Concentrated catalogue:** Electronics, Home & Kitchen and Computers & Accessories make up about 97% of products.
- **Right-skewed pricing:** median discounted price ≈ ₹899 vs. mean ≈ ₹3,305; Electronics has the highest prices.
- **Heavy discounting:** average discount ≈ 47%; Computers & Accessories and Electronics discount the most.
- **Consistently high ratings:** average ≈ 4.09; 61% of products rated between 4.0 and 4.5.
- **Weak relationships:** discount % vs. rating ≈ -0.16; rating vs. number of ratings ≈ 0.10.

## 🖼️ Visualisations
| Quality Report | Before vs After |
|---|---|
| ![Quality report](screenshots/01_quality_report.png) | ![Before vs After](screenshots/02_before_vs_after.png) |

| Product & Category Charts | Price Charts |
|---|---|
| ![Products](screenshots/03_product_charts.png) | ![Price](screenshots/04_price_charts.png) |

## 📁 Project Structure
```
DataAnalytics-L1-CleaningData/
├── Cleaning_Data_Amazon.ipynb   # Full cleaning notebook
├── amazon.csv                   # Raw dataset
├── amazon_cleaned.csv           # Cleaned dataset
├── README.md                    # Project documentation
└── screenshots/                 # Output screenshots
```

## ▶️ How to Run
```bash
# 1. Clone the repository
git clone https://github.com/TurpunatiVenkatesh/OIBSIP.git
cd OIBSIP/DataAnalytics-L1-CleaningData

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 3. Launch the notebook
jupyter notebook Cleaning_Data_Amazon.ipynb
```
Run **Kernel → Restart & Run All**. Keep `amazon.csv` in the same folder as the notebook.

## ⚠️ Limitations
- The dataset has no date or sales column, so the number of ratings was used as a proxy for popularity.
- Some categories contain only 1-2 products, so their averages are not reliable.

## 💡 Skills Demonstrated
Data auditing · type conversion · missing-value imputation · de-duplication · feature engineering · outlier analysis (IQR) · data validation · exploratory visualisation · technical documentation

## 👤 Author
**[Turpunati Venkatesh]**
Data Analytics Intern, Oasis Infobyte
🔗 [LinkedIn](https://www.linkedin.com/in/turpunati-venkatesh-440b3b301?utm_source=share_via&utm_content=profile&utm_medium=member_android) · 🔗 [GitHub](https://github.com/TurpunatiVenkatesh)

#oasisinfobyte #dataanalytics #python #datacleaning
