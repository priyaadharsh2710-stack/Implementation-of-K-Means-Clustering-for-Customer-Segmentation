# Implementation-of-K-Means-Clustering-for-Customer-Segmentation

## AIM:
To write a program to implement the K Means Clustering for Customer Segmentation.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
1. Import the necessary packages using import statement.
2. Read the given csv file using read_csv() method and print the number of contents to be displayed using df.head().
3. Import KMeans and use for loop to cluster the data.
4. Predict the cluster and plot data graphs.
5. Print the outputs and end the program.
## Program:
```
/*
Program to implement the K Means Clustering for Customer Segmentation.
Developed by: Priyadharshini V
RegisterNumber:212225230219

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.cluster import KMeans
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import silhouette_score

import warnings
warnings.filterwarnings("ignore")

# Load Dataset
df = pd.read_csv("Mall_Customers.csv")   # Update path if needed

print("Dataset Loaded Successfully!")
print("Shape:", df.shape)

print("\nFirst 5 Rows:")
print(df.head())

print("\nDataset Info:")
print(df.info())

print("\nMissing Values:")
print(df.isnull().sum())

# Features for clustering
features = ["Annual Income (k$)", "Spending Score (1-100)"]

X = df[features]

print("\nFeatures Used:", features)

# Feature Scaling
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# ---------------------------------------------------
# Elbow Method
# ---------------------------------------------------

inertia = []

K_range = range(1, 11)

for k in K_range:
    km = KMeans(n_clusters=k, random_state=42)
    km.fit(X_scaled)
    inertia.append(km.inertia_)

plt.figure(figsize=(6, 4))

plt.plot(K_range, inertia, marker='o')

plt.xlabel("Number of Clusters (k)")
plt.ylabel("Inertia / SSE")
plt.title("Elbow Method")

plt.grid(True)
plt.show()

# ---------------------------------------------------
# Silhouette Method
# ---------------------------------------------------

sil_scores = []

for k in range(2, 11):
    km = KMeans(n_clusters=k, random_state=42)
    labels = km.fit_predict(X_scaled)

    sil_scores.append(
        silhouette_score(X_scaled, labels)
    )

plt.figure(figsize=(6, 4))

plt.plot(
    range(2, 11),
    sil_scores,
    marker='o',
    color="orange"
)

plt.xlabel("Number of Clusters (k)")
plt.ylabel("Silhouette Score")
plt.title("Silhouette Method")

plt.grid(True)
plt.show()

# ---------------------------------------------------
# Final K-Means Model
# ---------------------------------------------------

k_final = 5

kmeans = KMeans(
    n_clusters=k_final,
    random_state=42
)

cluster_labels = kmeans.fit_predict(X_scaled)

# Add cluster labels to dataframe
df["Cluster"] = cluster_labels

print("\nCluster Counts:")
print(df["Cluster"].value_counts())

# Cluster centers
centers_scaled = kmeans.cluster_centers_

centers_original = scaler.inverse_transform(
    centers_scaled
)

centers_df = pd.DataFrame(
    centers_original,
    columns=features
)

centers_df["Cluster"] = range(k_final)

print("\nCluster Centers (Original Values):")
print(centers_df.round(2))

# ---------------------------------------------------
# Visualization
# ---------------------------------------------------

plt.figure(figsize=(8, 6))

sns.scatterplot(
    data=df,
    x="Annual Income (k$)",
    y="Spending Score (1-100)",
    hue="Cluster",
    palette="tab10",
    s=70
)

plt.scatter(
    centers_df["Annual Income (k$)"],
    centers_df["Spending Score (1-100)"],
    s=250,
    c="black",
    marker="X",
    label="Centroids"
)

plt.title("Customer Segmentation using K-Means (k=5)")

plt.legend()
plt.grid(True)

plt.show()
*/
```

## Output:
<img width="1008" height="753" alt="Screenshot 2026-05-19 120208" src="https://github.com/user-attachments/assets/33997dda-ef6a-4fc7-bf7e-72ca664a0d8d" />
<img width="886" height="495" alt="Screenshot 2026-05-19 120219" src="https://github.com/user-attachments/assets/1bde0fcd-910b-4f85-9afd-b510783339e8" />
<img width="991" height="503" alt="Screenshot 2026-05-19 120226" src="https://github.com/user-attachments/assets/e3bedad8-38a2-45cb-87be-8a8afa45c428" />
<img width="920" height="375" alt="Screenshot 2026-05-19 120236" src="https://github.com/user-attachments/assets/83b7a58c-9699-42a1-a4c3-5c6bdb9aea88" />
<img width="1091" height="707" alt="Screenshot 2026-05-19 120249" src="https://github.com/user-attachments/assets/988cac04-cbd4-4ab6-84b8-96440ec3a63d" />

## Result:
Thus the program to implement the K Means Clustering for Customer Segmentation is written and verified using python programming.
