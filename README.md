# ⛏️ Mining Quality Prediction using ML & DL

![Python](https://img.shields.io/badge/Python-3.11-blue?style=flat&logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?style=flat&logo=tensorflow)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.x-green?style=flat&logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-Enabled-red?style=flat)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat)

> Predicting **% Silica Concentrate** in real-time from flotation plant sensor data using 6 Machine Learning and Deep Learning models — enabling faster quality control decisions in iron ore mining.

---

## 📌 Problem Statement

In iron ore mining, **silica (SiO₂) is the primary impurity** in the final iron concentrate. High silica levels reduce ore grade and selling price. Traditional laboratory testing takes **up to 2 hours** to return results.

This project builds a **real-time prediction system** using sensor data recorded every 20 seconds from a Brazilian iron ore flotation plant — allowing operators to take corrective action immediately instead of waiting for lab results.

---

## 📊 Dataset

| Property | Details |
|---|---|
| Source | [Kaggle — Quality Prediction in a Mining Process](https://www.kaggle.com/datasets/edumagalhaes/quality-prediction-in-a-mining-process) |
| Rows | 737,453 |
| Columns | 24 |
| Recording Interval | Every 20 seconds |
| Period | March – September 2017 |
| Target Variable | % Silica Concentrate |

> **Note:** Download the dataset from Kaggle and place it as `mining_data.csv` in the root directory before running the notebook.

---

## 🧠 Models Trained & Results

| Model | R² Score | RMSE | MAE |
|---|---|---|---|
| Linear Regression | 0.6782 | 0.6379 | 0.4925 |
| Decision Tree | 0.8578 | 0.4240 | 0.2883 |
| Random Forest | 0.8844 | 0.3823 | 0.2691 |
| XGBoost | 0.8902 | 0.3727 | 0.2656 |
| LSTM | 0.8840 | 0.3830 | 0.2769 |
| **ANN** | **0.9369** | **0.2825** | **0.1936** |

✅ **ANN achieved the best performance** — with an MAE of **0.1936%**, meaning predictions are within 0.2% silica concentration on average. This is sufficient accuracy for real-time flotation process control.

---

## 🔍 Key Findings

- **ANN outperforms all models** with R² of 0.9369 across all three metrics
- **Decision Tree without depth constraint overfits** — R² dropped from 0.99 (fake) to 0.85 (honest) after adding `max_depth=10`; train and test scores became nearly identical (0.8495 vs 0.8474) confirming no overfitting
- **XGBoost edges out Random Forest** (0.8902 vs 0.8844) — gradient boosting learns from previous tree errors, giving it an advantage over bagging
- **LSTM and Random Forest perform comparably** — LSTM needs proper sequential windowing with multiple timesteps to fully leverage the temporal nature of sensor data
- The sensor data is recorded every 20 seconds making it inherently time-series — a key domain insight that motivated including LSTM

---

## 🏗️ Project Structure

```
mining-quality-prediction-ml/
│
├── Mining_Quality_Prediction.ipynb   ← Main notebook
├── requirements.txt                  ← Python dependencies
├── README.md                         ← Project documentation
└── assets/
    └── model_comparison.png          ← Results table screenshot
```

---

## ⚙️ Tech Stack

| Category | Libraries |
|---|---|
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Classical ML | Scikit-learn (LR, DT, RF) |
| Gradient Boosting | XGBoost |
| Deep Learning | TensorFlow, Keras (ANN, LSTM) |
| Environment | Jupyter Notebook |

---

## 🚀 How to Run

**1. Clone the repository**
```bash
git clone https://github.com/yourusername/mining-quality-prediction-ml.git
cd mining-quality-prediction-ml
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Download the dataset**

Go to [Kaggle Dataset](https://www.kaggle.com/datasets/edumagalhaes/quality-prediction-in-a-mining-process), download and place the CSV file as:
```
mining_data.csv
```

**4. Launch the notebook**
```bash
jupyter notebook Mining_Quality_Prediction.ipynb
```

**5. Run all cells**

`Kernel → Restart & Run All`

---

## 🔮 Sample Prediction

Given sensor input values, all 6 models predict the % Silica Concentrate in real-time:

```
Decision Tree Prediction  :  4.1192 % Silica
Random Forest Prediction  :  3.7435 % Silica
ANN Prediction            :  3.3927 % Silica
LSTM Prediction           :  3.4720 % Silica
XGBoost Prediction        :  3.5841 % Silica
```

> The average silica in the dataset is ~2.32%. These predictions indicate a **below-average quality batch** — exactly the kind of real-time insight that helps plant operators intervene early.

---

## 📈 Workflow

```
Raw Sensor Data → Drop Date Column → EDA & Visualization
→ StandardScaler → Train/Test Split (70/30)
→ Train 6 Models → Evaluate (R², RMSE, MAE)
→ Compare → Real-time Prediction
```

---

## 🌐 Domain Context

> This project was built with domain understanding of the iron ore flotation process. Silica concentrate directly impacts iron ore grade and pricing in global commodity markets. Making this prediction available every 20 seconds — instead of waiting 2 hours for lab results — has direct commercial value for mining operations.

---

## 📄 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgements

- Dataset by [Eduardo Magalhães on Kaggle](https://www.kaggle.com/datasets/edumagalhaes/quality-prediction-in-a-mining-process)
- Flotation plant process domain reference: [Natural Resources Canada](https://www.nrcan.gc.ca/digital-accelerator/current-artificial-intelligence-projects/22577)