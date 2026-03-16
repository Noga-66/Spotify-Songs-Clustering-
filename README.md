# 🎵 Sound DNA — Spotify Clustering Engine

> **AI-powered music clustering** that groups songs by sonic similarity using K-Means, Hierarchical, and DBSCAN algorithms — with a live interactive web app powered by Claude AI.

---

## 📸 Project Overview

This project analyzes **232,725 Spotify songs** across **26 genres** using **9 audio features** to discover hidden musical patterns. It includes:

- 📓 A full **Jupyter Notebook** for data exploration, model training, and evaluation
- 🌐 An **interactive web app** with real-time AI clustering powered by Claude
- 📊 Visual tools: Radar charts, DNA bar profiles, PCA scatter plots, dendrograms

---

## 🗂️ Project Structure

```
spotify-clustering/
│
├── index.html                  # Web app (black + cyan, animated UI)
├── Spotify_Clustering.ipynb    # Full analysis notebook
├── SpotifyFeatures.csv         # Dataset (232K songs)
├── requirements.txt            # Python dependencies
└── README.md                   # This file
```

---

## 🚀 Quick Start

### 1. Clone / Download

```bash
git clone https://github.com/your-username/spotify-clustering.git
cd spotify-clustering
```

### 2. Install Python Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the Jupyter Notebook

```bash
jupyter notebook Spotify_Clustering.ipynb
```

### 4. Open the Web App

Just open `index.html` in any browser — no server needed.

> To enable the AI clustering feature, you need an [Anthropic API key](https://console.anthropic.com/).

---

## 📊 Dataset

| Property | Value |
|---|---|
| Source | [Spotify Features — Kaggle](https://drive.google.com/file/d/1gz74jdqc42xVzE7oh2TU6Tn3chFANFlB/view?usp=drive_link) |
| Records | 232,725 songs |
| Genres | 26 (Pop, Rock, Jazz, Hip-Hop, Classical…) |
| Features | 18 columns |
| Missing values | 1 (track_name) |

### Audio Features Used for Clustering

| Feature | Range | Description |
|---|---|---|
| `danceability` | 0.0 – 1.0 | How suitable a track is for dancing |
| `energy` | 0.0 – 1.0 | Perceptual measure of intensity and activity |
| `acousticness` | 0.0 – 1.0 | Confidence the track is acoustic |
| `valence` | 0.0 – 1.0 | Musical positiveness / mood |
| `tempo` | 30 – 243 BPM | Overall estimated tempo |
| `speechiness` | 0.0 – 1.0 | Presence of spoken words |
| `liveness` | 0.0 – 1.0 | Presence of a live audience |
| `instrumentalness` | 0.0 – 1.0 | Predicts whether track has no vocals |
| `loudness` | -52 – 4 dB | Overall loudness of the track |

---

## 🔬 Notebook Walkthrough

The notebook (`Spotify_Clustering.ipynb`) is organized into 10 sections:

```
1️⃣  Import Libraries
2️⃣  Load & Explore Data          → distributions, missing values, genre counts
3️⃣  Data Preprocessing           → scaling with StandardScaler, sampling 30K rows
4️⃣  PCA Analysis                 → explained variance, 2D/3D projections
5️⃣  K-Means Clustering           → Elbow Method, Silhouette Score, optimal K
6️⃣  Hierarchical Clustering      → Dendrogram (Ward linkage), AgglomerativeClustering
7️⃣  DBSCAN Clustering            → K-Distance Graph, epsilon tuning
8️⃣  Model Comparison             → Silhouette, Davies-Bouldin, Calinski-Harabasz
9️⃣  Cluster Insights             → Radar chart, genre distribution, sample songs
🔟  Save Results                  → Export clustered CSV
```

---

## 🤖 Algorithms

### K-Means
- Partitions songs into **K groups** by minimizing within-cluster variance (WCSS)
- Best for: large datasets, spherical clusters
- Tuning: use the **Elbow Method** + **Silhouette Score** to find optimal K

### Hierarchical Clustering (Ward Linkage)
- Builds a **dendrogram** by merging clusters that minimize total variance
- Best for: understanding cluster hierarchy, smaller samples
- Visualized via dendrogram (truncated to 30 leaves)

### DBSCAN
- Finds clusters of **arbitrary shape** based on point density
- Automatically marks outlier songs as **noise** (label = -1)
- Tuning: use the **K-Distance Graph** to find optimal `epsilon`

---

## 📈 Evaluation Metrics

| Metric | Goal | Interpretation |
|---|---|---|
| **Silhouette Score** | Maximize | Close to 1 = well-separated clusters |
| **Davies-Bouldin Score** | Minimize | Close to 0 = compact, well-separated clusters |
| **Calinski-Harabasz Score** | Maximize | Higher = better-defined clusters |

---

## 🌐 Web App Features

The `index.html` app provides a live clustering experience:

- **9 interactive sliders** — tune any audio feature in real time
- **3 algorithm tabs** — switch between K-Means, Hierarchical, DBSCAN
- **AI Analysis** — sends features to Claude API, returns cluster assignment
- **Audio DNA Profile** — bar chart comparing your input vs cluster centroid
- **Animated UI** — floating musical notes canvas, scan lines, waveform loader
- **Analysis History** — stores last 6 cluster results

### Web App Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML / CSS / JavaScript |
| Fonts | Syne, Space Mono, DM Sans (Google Fonts) |
| AI Backend | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Deployment | Static file — no server required |

---


## ⚙️ Configuration

To use the live AI clustering in the web app, the Anthropic API key must be injected via a backend proxy or directly (dev only). The app calls:

```
POST https://api.anthropic.com/v1/messages
Model: claude-sonnet-4-20250514
```

> ⚠️ **Security note:** Never expose your API key in a public frontend. For production, route requests through a backend proxy (Node.js / Python / Cloudflare Worker).

---

## 📦 Python Environment

```bash
# Create virtual environment (recommended)
python -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Launch notebook
jupyter notebook
```

**Minimum Python version:** `3.8`
**Recommended:** `3.10+`

---

## 📋 Sample Results

Example cluster profiles discovered from the dataset:

| Cluster | Name | Danceability | Energy | Valence | Description |
|---|---|---|---|---|---|
| 0 | Acoustic Chill | 0.42 | 0.28 | 0.38 | Soft, intimate, organic |
| 1 | High Energy Floor | 0.78 | 0.88 | 0.65 | Loud, fast, dancefloor-ready |
| 2 | Dark Atmospheres | 0.48 | 0.55 | 0.18 | Moody, low valence, dense |
| 3 | Feel-Good Pop | 0.71 | 0.72 | 0.75 | Bright, catchy, mainstream |
| 4 | Experimental Edge | 0.44 | 0.61 | 0.40 | Unconventional, niche |
| 5 | Soulful Groove | 0.68 | 0.58 | 0.56 | Rhythmic, warm, R&B-influenced |

---

## 🛠️ Tech Stack (Full Project)

| Component | Technology |
|---|---|
| Language | Python 3.10 |
| Data manipulation | pandas, numpy |
| Clustering | scikit-learn |
| Statistics | scipy |
| Visualization | matplotlib, seaborn |
| Notebook | Jupyter |
| Web frontend | HTML5 / CSS3 / Vanilla JS |
| AI API | Anthropic Claude |

---


## 📄 License

MIT License — free to use, modify, and distribute.

---

## 👤 Author

Built  BY Nada Hossam ❤️ using Python, scikit-learn, and Claude AI.

---

*Sound DNA · Spotify Clustering Engine .
