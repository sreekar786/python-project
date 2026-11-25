# MetaPick: Meta-Learning Algorithm Selection for Tabular Classification

> Stop guessing. Let the data choose its own algorithm.

MetaPick is a meta-learning framework that studies the shape of a tabular dataset and recommends the best classifier in seconds, without exhaustive trial and error. This repository contains the project's interactive demo, a single self-contained HTML page that runs entirely in your browser.

**Domain:** AI & Machine Learning · **Task:** Tabular classification · **Status:** Research project, first version (rule-based demo)

---

## Table of Contents

- [The Problem](#the-problem)
- [How the Framework Works](#how-the-framework-works)
- [Live Demo](#live-demo)
- [Candidate Algorithms](#candidate-algorithms)
- [Evaluation Plan](#evaluation-plan)
- [Roadmap](#roadmap)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Limitations](#limitations)
- [Author](#author)

---

## The Problem

No single classifier wins on every dataset. Choosing the right one usually means hours of manual experiments.

- **Trial and error is costly.** Training and tuning many models on every new dataset burns compute and time.
- **Expertise doesn't scale.** Experienced practitioners pick well from intuition, but beginners and busy teams can't rely on it.
- **Meta-learning learns to learn.** Past results on many datasets can teach a model which algorithm fits which kind of data.

MetaPick targets this algorithm selection problem: **extract 20+ meta-features per dataset, rank 8 candidate classifiers, in 1 pass instead of training every model.**

---

## How the Framework Works

A meta-model is trained once on a large collection of datasets. After that, every new dataset gets a recommendation instantly.

1. **Collect datasets.** Gather many tabular classification benchmarks, such as those on OpenML.
2. **Extract meta-features.** Size, class balance, feature types, correlation, entropy, landmarkers.
3. **Run algorithms.** Cross-validate candidate classifiers and record each score.
4. **Train the meta-model.** Learn the link between dataset traits and the best-performing algorithm.
5. **Recommend.** For a new dataset, output a ranked list of algorithms.

---

## Live Demo

Open the HTML file in any modern browser. No server, install, or build step required.

**Features**

- **Dataset profile sliders:** rows, features, categorical share, class imbalance, noise level, missing values.
- **Ranked recommendations:** a live ranking of the 8 candidate algorithms with fit scores.
- **Upload your own CSV:** the demo reads the file in your browser and fills the sliders from its profile. The last column is treated as the target. *Nothing is uploaded.*
- **Explainability:** shows why the top algorithm was picked, plus warnings (for example high class imbalance, many missing values, features outnumbering rows).
- **Export:** copy a ready-to-run scikit-learn Python snippet, a Markdown report, or a JSON summary of the recommendation.
- **Game mode, "Beat the Meta-Model":** get a mystery dataset, guess the winning classifier, and see if you can out-predict MetaPick. Includes an ML Intuition Score, win streak, and rounds.

> The demo is **illustrative** and based on common rules of thumb. In Game mode, the ground-truth winner comes from a simulated benchmark, not real experiments. The full framework replaces these rules with a meta-model trained on real benchmark results.

---

## Candidate Algorithms

| Algorithm | Strong when | Weak when |
|---|---|---|
| Random Forest | Mixed features, noise | Very high dimensions |
| Gradient Boosting (XGBoost / LightGBM) | Medium to large tabular data | Tiny or very noisy data |
| Logistic Regression | Linear patterns, small data | Complex interactions |
| SVM | Small to medium, numeric data | Huge datasets |
| k-Nearest Neighbors | Small, clean, low dimension | Many features |
| Naive Bayes | Tiny data, many categories | Correlated features |
| Decision Tree | Interpretability needed | Overfits easily |
| MLP Neural Network | Large numeric data | Small data |

---

## Evaluation Plan

The framework will be judged on how often its top picks match the true best algorithm:

- **Top-k accuracy:** how often the truly best algorithm appears in the top 1, 3, and 5 recommendations.
- **Performance regret:** the gap between the recommended model's score and the best model's score.
- **Time saved:** compute cost versus brute-force search across all candidates.

> No measured accuracy, top-k, or regret numbers are reported yet. They will come from cross-validated experiments.

---

## Roadmap

| Priority | Item | Description |
|---|---|---|
| High | Trained meta-model | Replace hand-written rules with a meta-model trained on hundreds of benchmark datasets. |
| High | Real benchmark results | Report measured top-k accuracy and regret from cross-validated experiments. |
| Done | Upload your own CSV | The demo reads a CSV in-browser and fills the sliders from its profile. |
| Medium | Missing-value handling | Meta-features for datasets with many missing values, plus built-in imputation advice. |
| Medium | Hyperparameter suggestions | Suggest settings such as tree depth or learning rate, not just the algorithm. |
| Medium | Explainable recommendations | Show which dataset traits drove each pick, for example with SHAP. |
| Later | Landmarking features | Run fast, simple models on a data sample to add stronger meta-features. |
| Later | Compare with AutoML | Benchmark against brute-force search and tools such as Auto-sklearn or FLAML. |
| Later | Regression and multi-label tasks | Extend beyond tabular classification. |

---

## Getting Started

```bash
# Clone the repository
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

# Open the demo (or just double-click the file)
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

If hosting on **GitHub Pages**: go to *Settings → Pages*, choose the `main` branch and root folder, and your demo will be live at `https://<your-username>.github.io/<your-repo>/`. Rename the HTML file to `index.html` so it loads as the home page.

---

## Project Structure

```
.
├── index.html   # Self-contained demo (HTML + CSS + JavaScript)
└── README.md
```

---

## Limitations

- Recommendations in this version come from **hand-written rules**, not a trained meta-model.
- The demo recommends the **algorithm only**, not hyperparameters.
- Scope is **tabular classification** only.
- Fonts load from Google Fonts; everything else runs offline.

---

## Author

**Sreekar Karthikeya**
Student researcher · AI & Machine Learning

*Meta-Learning-Based Algorithm Selection Framework for Tabular Classification Tasks*
