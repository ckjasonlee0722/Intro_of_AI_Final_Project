# LoL Ban/Pick Recommendation & Win Rate Prediction System

## 🔧 Summary

This PR includes the full migration of the LoL_BP_Project from local development to GitHub with:

- ✅ Cleaned Git history (previous large-file commits removed)
- ✅ Proper usage of Git LFS for large files:
  - `models/pick_lgb_v3.txt`
  - `data/stats1.csv` / `data/stats2.csv`
  - Other large `.csv`, `.parquet`, `.pkl` files
- ✅ Organized directory structure: `data/`, `models/`, `scripts/`, `ui/`, `output/`, `reports/`
- ✅ Git ignore rules for intermediate files, system cache, and local logs
- ✅ Dev branch is ready to be merged into `main`

---

## 📖 Overview

A complete hero recommendation and win rate prediction system for the **Ban/Pick phase** in *League of Legends*. Using historical professional match data, the model predicts the top-k recommended champions and the blue side's real-time win rate at each draft step. The system includes a full **Streamlit** UI that accepts pick/ban inputs and returns live recommendations and win rate curves.

📊 **[View Project Presentation](https://drive.google.com/file/d/1aOiGjeC4FWUaJkFXYO2ZJWX6_28NVgrS/view?usp=sharing)**
---

## 📂 Project Structure
```bash
LoL_BP_Project/
│
├── data/
│   ├── matches.csv / participants.csv / teamstats.csv / teambans.csv
│   ├── stats1.csv, stats2.csv        # OraclesElixir match data
│   └── champs.csv                    # Champion ID ↔ Name mapping
│
├── models/
│   ├── pick_lgb_v3.txt               # Pick recommendation model
│   ├── pick_encoder_v3.pkl           # Label encoder
│   └── wr_lgb_v4.txt                 # Win rate prediction model
│
├── output/
│   ├── match_dataset.parquet
│   ├── pick_dataset.parquet
│   └── champ_wr.parquet              # Per-champion blue/red win rates
│
├── scripts/
│   ├── data_preprocess_v2.py
│   ├── train_pick_v3_tqdm.py
│   ├── train_wr.py
│   └── search.py
│
├── ui/
│   ├── app.py                        # Streamlit frontend
│   └── ngrok/                        # External sharing tool
│
└── reports/
    ├── train_pick_v3.log
    ├── pick_cv_v3.txt
    └── wr_cv_v4.txt
```

---

## ✅ Installation
```bash
conda activate lolbp
pip install -U streamlit lightgbm pandas scikit-learn
```

---

## ✅ Required Files

| File Path | Description |
|-----------|-------------|
| `models/wr_lgb_v4.txt` | LightGBM win rate model (trained by `train_wr.py`) |
| `output/champ_wr.parquet` | Per-champion blue/red avg win rate |
| `data/champs.csv` | Champion ID → English name mapping |
| `ui/app.py` | Streamlit frontend for recommendations and win rate curve |

---

## 🚀 Usage

**1. Data Preprocessing**
```bash
cd scripts/
python data_preprocess_v2.py
```

**2. Train Win Rate Model**
```bash
python train_wr.py
```

**3. Train Pick Recommendation Model**
```bash
python train_pick_v3_tqdm.py --n_trials 10 --num_boost 400
```

**4. CLI Test**
```bash
python search.py --team blue --ban 1,2,3 --topk 5
```

**5. Launch Web UI**
```bash
cd ui/
streamlit run app.py
```

**6. (Optional) Ngrok External Sharing**
```bash
ngrok http 8501
```

---

## 🧠 Features

- **ML Model** — LightGBM + Optuna auto-tuning, Top-5 recommendation accuracy ≈ **67.3%**
- **Draft Support** — Auto-filters already picked/banned champions
- **Interactive UI** — Displays Top-5 picks with predicted probability and win rate curve
- **External Access** — Ngrok support for sharing over the internet

---

## 🎯 Win Rate Prediction Curve (Example)

| Step | Blue Picks | Red Picks | Predicted Blue WR |
|-----:|------------|-----------|------------------:|
| 1 | `[1]` | `[]` | 52.1% |
| 2 | `[1]` | `[11]` | 50.3% |
| 3 | `[1]` | `[11, 64]` | 48.7% |
| ... | ... | ... | ... |
| 10 | `[1,105,55,238,61]` | `[11,64,103,157,121]` | 59.8% |

---

## 📦 Git LFS Tracked Files

> ⚠️ Install Git LFS before cloning: `git lfs install`

- `models/pick_lgb_v3.txt`
- `models/pick_encoder_v3.pkl`
- `data/stats1.csv` / `data/stats2.csv`
- `output/pick_dataset.parquet`
- `output/match_dataset.parquet`
- `output/champ_wr.parquet`
