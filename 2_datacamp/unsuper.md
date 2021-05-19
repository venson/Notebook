# Unsupervised learning in Python

## Clustering 
### 1. KMeans() -- pipeline support

```{python}
model = KMeans(n_clusters = n)
model.fit(samples)
labels = model.predict(samples)
labels = model.fit_predict(samples)
```

how to determine `n_clusters`, choose and "elbow" in the inertia plot.


```{python}
print(model.inertia_)
```
### 2. preprocessing

```{python}
from sklearn.preprocessing import StandardScaler
```
transforms each feature to have mean 0 and variance 1

```{python}
from sklearn.preprocessing import Normalizer
MaxAbsScaler
```

## 2. Hierachical cluster and t-SNE

### 1. scipy.cluster.hierarchy

```{python}
mergings = linkage(samples, method = 'complete')
dendrogram(mergins, lables = , leaf_rotation = 90, leaf_font_size = 6)
fcluster(mergings, 15, criterion = 'distance')
##extracing cluster labels
```

### 2. sklearn.manifold

t-distributed stochastic neighbor embedding(t-SNE)
.t-SNE map the data to 2D space so the that the proximity of the samples to one another can be visualized.


```{python}
model = TSNE(learning_rate = 100)  # learning_rate 50-200
transformed = model.fit_transform(samples)
```


### APPEND Evaluate

`pd.crosstab(df.labels, df.varieties)`

## 3. Decorrelating your data and dimension
 e
Visualizing the PCA transformation

PCA Principal Component Analysis

- Fundamental
- First step "decorrelation"
- Second step "reduce dimension"


## 4. Discover interpretable features



- "Non-negative matrix factorization"(NMF) expresses samples as combinations of interpretable parts
- Dimension reduction technique
- interpretable (unlike PCA)
- EASY to interpret ,EASY to EXPLAIN!
- MUST BE NON-NEGATIVE !!!!


