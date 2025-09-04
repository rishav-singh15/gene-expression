#  Breast Cancer Gene-Expression Clustering

This mini-project explores how to use machine-learning techniques to visualise and cluster normal vs. tumour breast-cancer samples using TCGA gene-expression data.

---

##  Input Data

Two tab-delimited text files containing gene expression:

- `BC-TCGA-Normal.txt` – expression profiles of normal breast tissue samples.
- `BC-TCGA-Tumor.txt` – expression profiles of breast tumour tissue samples.

Each file’s first column = gene names, subsequent columns = samples.

---

##  Data Processing Steps

1. **Load and Align**
   - Read both files with `pandas`.
   - Set gene names as index.
   - Keep only genes present in both datasets.
   - Concatenate columns to combine all samples.
   - Transpose so rows = samples, columns = genes.

2. **Labelling**
   - Assign `0` = Normal, `1` = Tumour.

3. **Cleaning and Scaling**
   - Fill missing values with the mean expression per gene.
   - Standardise each gene (zero mean, unit variance) using `StandardScaler`.

4. **Feature Selection**
   - Compute variance of each gene across samples.
   - Select the top 2000 most variable genes for downstream analysis.

---

##  Exploratory Visualisation

- **t-SNE scatter plot**  
  2-D embedding of the top-genes matrix, coloured by true labels (Normal vs Tumour).  
  Shows how well expression profiles separate in low-dimensional space.

---

##  Dimensionality Reduction & Clustering

1. **PCA (Principal Component Analysis)**
   - Reduce 2000 genes → 50 PCs to denoise and speed up clustering.
   - Report total variance explained by first 50 PCs.

2. **K-Means Clustering (k=2)**
   - Cluster samples in the 50-PC space into two groups without labels.
   - Compare cluster assignments with true labels:
     - **Confusion matrix**
     - **Adjusted Rand Index (ARI)**
   - Compute **Silhouette score** to quantify cluster cohesion/separation.

3. **Hierarchical Clustering**
   - Compute Ward’s linkage on PCA data.
   - Plot dendrogram to visualise how samples merge into clusters.
   - Optionally cut the tree into 2 clusters.

---

##  Visualisations Produced

- **Dendrogram**: shows hierarchical relationships between samples.
- **t-SNE (KMeans colours)**: 2-D map coloured by cluster ID.
- **t-SNE (True labels)**: same map coloured by Normal/Tumour status.
- **Confusion matrix + ARI + Silhouette**: quantitative cluster quality metrics.

---

##  Gene-Level Signature Plot

- Compute the mean expression per gene per cluster.
- Find the 20 genes with the largest absolute difference between clusters.
- Plot a **heatmap** (samples × top 20 genes):
  - Columns = samples (sorted by cluster)
  - Rows = top marker genes
  - Red = higher than average expression; Blue = lower

This heatmap highlights which genes drive the separation between the two groups.

---

##  How to Run

1. Place your two BC-TCGA files(https://www.kaggle.com/datasets/orvile/gene-expression-profiles-of-breast-cancer) in the working directory.
2. Run the Python notebook or script step-by-step.
3. Inspect each generated plot:
   - t-SNE of true labels
   - Dendrogram
   - t-SNE of KMeans clusters
   - Heatmap of top marker genes
4. Check ARI and Silhouette scores in the console for clustering quality.
