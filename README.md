# Predicting Trust and Distrust in Bitcoin Web-of-Trust Networks

Final Project for **ID2211 – Data Mining**
**KTH Royal Institute of Technology**
June 2026

* Course Responsible: [**Sarunas Girdzijauskas**](https://www.kth.se/profile/sarunasg?l=en)
* Teaching Assistant: [**Rémi Bourgerie**](https://www.kth.se/profile/remibo)

## Deliverables
- 📑 [Project Report](deliverables/project_report.pdf)
- 🚩 [Project Milestone Report](deliverables/project_milestone.pdf)
- 🔗 [Project Code](deliverables/ID2211_code.ipynb)



---

## Project Overview

Online reputation systems play a crucial role in decentralized platforms, where users often interact without knowing each other personally. In Bitcoin Web-of-Trust networks, users can assign positive or negative ratings to other participants based on previous transactions, creating a signed social network.

The goal of this project is to **predict whether a future interaction between two users will result in a trust or distrust relationship**. Given an interaction between two users, the objective is to predict whether the corresponding edge represents:

* **Trust (+1)**
* **Distrust (-1)**
  
The project combines graph analysis, feature engineering inspired by social network theories such as Balance Theory and Status Theory, and machine learning techniques. We compare a feature-based approach using Random Forests with a graph neural network model (SGCN) and evaluate their ability to predict the sign of future interactions.

Beyond predictive performance, the project also investigates which structural properties of signed networks are most informative and whether trust dynamics learned on one platform can generalize to another.

---

## Datasets

The datasets are publicly available from the Stanford [SNAP](http://snap.stanford.edu/data/) repository:

* [`soc-sign-bitcoinalpha`](data/soc-sign-bitcoinalpha.csv)
* [`soc-sign-bitcoinotc`](data/soc-sign-bitcoinotc.csv)

Each edge contains:

* source node
* target node
* rating in [-10, +10]
* timestamp

Ratings are converted into binary labels:

* rating > 0 → Trust (+1)
* rating ≤ 0 → Distrust (-1)

---

## Main Components

### Exploratory Data Analysis

The project performs:

* Class imbalance analysis
* Degree distribution analysis
* Reciprocity analysis
* Triad census
* Structural graph statistics

### Feature Engineering

A 14-dimensional feature vector is built using:

#### Local Node Features

* Out-degree
* In-degree
* Mean rating given
* Mean rating received
* Positive rating fractions

#### Balance Theory Features

* Common neighbors
* Balance predictions
* Balance signal

#### Status Theory Feature

* Status difference between source and target nodes

#### Reciprocity Features

* Presence of reverse edge
* Sign of reverse edge

### Models

#### Random Forest

* 5-fold stratified cross-validation
* Grid search hyperparameter tuning
* Class balancing

#### Signed Graph Convolutional Network (SGCN)

* Implemented with PyTorch Geometric
* Two-layer architecture
* Temporal train/test evaluation

---

## Requirements

Install the required Python packages:

```bash
pip install pandas numpy networkx matplotlib scikit-learn torch torch-geometric
```

---

## Running the Project

Execute the notebook:

```bash
jupyter notebook ID2211.ipynb
```

The notebook will:

1. Download the Bitcoin Alpha and Bitcoin OTC datasets.
2. Perform exploratory data analysis.
3. Generate all engineered features.
4. Train and evaluate the Random Forest model.
5. Train and evaluate the Signed Graph Convolutional Network.
6. Produce the figures and processed datasets used in the report.

---

## Key Findings

- Structural features derived from user behavior, reciprocity, and signed network topology provide strong predictive signals for trust and distrust relationships.
- Reciprocity emerged as one of the most informative sources of information for sign prediction.
- The feature-engineered Random Forest consistently outperformed the Signed Graph Convolutional Network under a realistic temporal evaluation setting.
- Cross-dataset experiments showed that models trained on one Bitcoin trust network can be successfully applied to the other. This result is likely facilitated by the strong structural similarities between Bitcoin Alpha and Bitcoin OTC, which exhibit comparable network statistics and trust dynamics.

For a detailed discussion of the experiments and quantitative results, see the project report.

## Authors

* Bilal Soussane:       [soussane@kth.se](mailto:soussane@kth.se) 
* Edoardo F. A. de Cal: [efadc@kth.se](mailto:efadc@kth.se)       
* Giorgia Savo:         [giorgias@kth.se](mailto:giorgias@kth.se) 
* Marta Guzman Alarcón: [martaga@kth.se](mailto:martaga@kth.se)   

