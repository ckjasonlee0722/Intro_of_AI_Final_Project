# LoL Ban/Pick Recommendation & Win Rate Prediction System

A machine learning system for **League of Legends professional draft analysis**, providing champion recommendation and win-rate prediction during the Ban/Pick phase.

📊 **Project Presentation**

[View Presentation](https://drive.google.com/file/d/1aOiGjeC4FWUaJkFXYO2ZJWX6_28NVgrS/view?usp=sharing)

---

# 📖 Overview

In professional League of Legends matches, the Ban/Pick phase plays an important role in determining the final game outcome. Draft decisions involve complex interactions between:

- Champion synergy
- Counter relationships
- Team composition
- Historical performance statistics

This project develops a data-driven draft assistant that predicts:

1. **Top-k champion recommendations**
2. **Blue-side win rate changes during the draft process**

The system builds a complete machine learning pipeline:

```
Professional Match Data
          |
          v
Data Preprocessing
          |
          v
Feature Engineering
          |
          +----------------+
          |                |
          v                v
Champion Pick Model   Win Rate Prediction Model
(LightGBM)            (LightGBM)
          |                |
          +----------------+
                   |
                   v
          Interactive Draft Simulator
                   |
                   v
             Streamlit Interface
```

---

# 🎯 Project Goals

The goal of this project is to explore how machine learning can assist strategic decision-making in competitive esports.

Given the current draft state, the system attempts to answer:

> "Which champion should be selected next, and how does this decision affect the predicted game outcome?"

---

# 🧠 Machine Learning Approach

## 1. Champion Recommendation Model

### Task

Predict suitable champion choices given:

- Current picked champions
- Current banned champions
- Team composition information
- Historical professional match statistics


### Method

- Feature engineering from professional match data
- LightGBM classifier
- Optuna hyperparameter optimization


### Output

The model provides:

- Top-k recommended champions
- Prediction confidence scores


---

## 2. Win Rate Prediction Model

### Task

Estimate blue-side winning probability throughout the draft process.


### Method

Features include:

- Champion selections
- Champion statistics
- Draft state information


Model:

- LightGBM


### Output

The system generates a real-time win-rate curve:

```
Draft Step
     |
     v
Feature Update
     |
     v
Win Rate Prediction
```

---

# 📊 Results

## Champion Recommendation

| Model | Result |
|---|---|
| LightGBM + Optuna | Top-5 Recommendation Accuracy ≈ **67.3%** |

---

## Example Win Rate Prediction

| Step | Blue Picks | Red Picks | Predicted Blue Win Rate |
|---:|---|---|---:|
| 1 | `[1]` | `[]` | 52.1% |
| 2 | `[1]` | `[11]` | 50.3% |
| 3 | `[1]` | `[11,64]` | 48.7% |
| ... | ... | ... | ... |
| 10 | `[1,105,55,238,61]` | `[11,64,103,157,121]` | 59.8% |

---

# 🖥️ Interactive Draft Simulator

The project provides a Streamlit-based interface supporting:

- Ban/Pick input
- Champion availability filtering
- Top-k recommendation
- Real-time win-rate visualization


Workflow:

```
User Draft Input
        |
        v
Feature Processing
        |
        v
Machine Learning Model
        |
        v
Recommendation + Win Rate Curve
```

---

# 📂 Project Structure

```
LoL_BP_Project/

│
├── data/
│   ├── matches.csv
│   ├── participants.csv
│   ├── teamstats.csv
│   ├── teambans.csv
│   ├── stats1.csv
│   ├── stats2.csv
│   └── champs.csv
│
├── models/
│   ├── pick_lgb_v3.txt
│   ├── pick_encoder_v3.pkl
│   └── wr_lgb_v4.txt
│
├── output/
│   ├── match_dataset.parquet
│   ├── pick_dataset.parquet
│   └── champ_wr.parquet
│
├── scripts/
│   ├── data_preprocess_v2.py
│   ├── train_pick_v3_tqdm.py
│   ├── train_wr.py
│   └── search.py
│
├── ui/
│   └── app.py
│
└── reports/
    ├── train_pick_v3.log
    ├── pick_cv_v3.txt
    └── wr_cv_v4.txt
```

---

# ⚙️ Installation

## Environment

```bash
conda create -n lolbp python=3.10
conda activate lolbp
```

Install dependencies:

```bash
pip install -U streamlit lightgbm pandas scikit-learn optuna
```

---

# 🚀 Usage

## 1. Data Preprocessing

```bash
cd scripts/

python data_preprocess_v2.py
```

---

## 2. Train Win Rate Prediction Model

```bash
python train_wr.py
```

---

## 3. Train Champion Recommendation Model

```bash
python train_pick_v3_tqdm.py --n_trials 10 --num_boost 400
```

---

## 4. Command Line Testing

Example:

```bash
python search.py --team blue --ban 1,2,3 --topk 5
```

---

## 5. Launch Streamlit Interface

```bash
cd ui/

streamlit run app.py
```

---

# 📁 Dataset

The system uses historical professional League of Legends match data.

Main information includes:

- Match results
- Champion picks and bans
- Team statistics
- Champion performance statistics


Processed datasets:

```
output/

├── match_dataset.parquet
├── pick_dataset.parquet
└── champ_wr.parquet
```

---

# 🔧 Model Files

| File | Description |
|---|---|
| `models/pick_lgb_v3.txt` | Champion recommendation model |
| `models/wr_lgb_v4.txt` | Win-rate prediction model |
| `models/pick_encoder_v3.pkl` | Feature encoder |

---

# 👤 Contribution

My main contributions include:

- Building the machine learning pipeline
- Data preprocessing and feature engineering
- Model training and evaluation
- Developing the interactive draft simulation interface

---

# 📦 Git LFS Support

Large files are managed using Git Large File Storage.

Install Git LFS:

```bash
git lfs install
```

Tracked files include:

```
models/
data/
output/
```

---

# 📌 Future Improvements

Possible extensions:

- Incorporating champion embedding methods
- Modeling team synergy and counter relationships
- Exploring sequential draft modeling approaches
- Applying deep learning methods for draft representation learning
