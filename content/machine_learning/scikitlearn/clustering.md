---
title: "Clustering: K-means, agglomerative with dendrograms, and DBSCAN"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
There are three types of clustering algorithms:    
    * **Prototype based clustering**: *k-means* which clusters into spherical shapes based on a specified number of cluster centroids. Downside is that it assumes this spherical structure and you need to input the number of centroids.   
    * **Hierarchical clustering**: *Agglomerative* clustering does not require specifying the number of clusters up front and the result can be visuzlized with a dendrogram.   
    * **Density based clustering**: *DBSCAN* groups points based on local densities and is capable of handling outliers and identifying non-globular shapes.    
    * **Density based clustering**: Not included here.   

### k-means vs. Agglomerative vs DBSCAN: Case of half moons


```python
import matplotlib.pyplot as plt 
from sklearn.datasets import make_moons

X, y = make_moons(n_samples=200, noise=0.05, random_state=0)
plt.scatter(X[:, 0], X[:, 1])
plt.tight_layout()
#plt.savefig('images/11_14.png', dpi=300)
plt.show()
```


![png](clustering_3_0.png)



```python
f, (ax1, ax2, ax3) = plt.subplots(1, 3, figsize=(16, 3))

# K-means
from sklearn.cluster import KMeans
km = KMeans(n_clusters=2, random_state=0)
y_km = km.fit_predict(X)
ax1.scatter(X[y_km == 0, 0], X[y_km == 0, 1],
            edgecolor='black',
            c='lightblue', marker='o', s=40, label='cluster 1')
ax1.scatter(X[y_km == 1, 0], X[y_km == 1, 1],
            edgecolor='black',
            c='red', marker='s', s=40, label='cluster 2')
ax1.set_title('K-means clustering')

# Agglomerative
from sklearn.cluster import AgglomerativeClustering
ac = AgglomerativeClustering(n_clusters=2,
                             affinity='euclidean',
                             linkage='complete')
y_ac = ac.fit_predict(X)
ax2.scatter(X[y_ac == 0, 0], X[y_ac == 0, 1], c='lightblue',
            edgecolor='black',
            marker='o', s=40, label='Cluster 1')
ax2.scatter(X[y_ac == 1, 0], X[y_ac == 1, 1], c='red',
            edgecolor='black',
            marker='s', s=40, label='Cluster 2')
ax2.set_title('Agglomerative clustering')

# DBSCAN
from sklearn.cluster import DBSCAN
db = DBSCAN(eps=0.2, min_samples=5, metric='euclidean')
y_db = db.fit_predict(X)
ax3.scatter(X[y_db == 0, 0], X[y_db == 0, 1], c='lightblue',
            edgecolor='black',
            marker='o', s=40, label='Cluster 1')
ax3.scatter(X[y_db == 1, 0], X[y_db == 1, 1], c='red',
            edgecolor='black',
            marker='s', s=40, label='Cluster 2')
ax3.set_title('DBSCAN clustering')

plt.legend()
plt.tight_layout()
#plt.savefig('images/11_15.png', dpi=300)
plt.show()
```


![png](clustering_4_0.png)


### K-means with elbow plot and silhouette


```python
# Make and plot data
import matplotlib.pyplot as plt
from sklearn.datasets import make_blobs

X, y = make_blobs(n_samples=150, 
                  n_features=2, 
                  centers=3, 
                  cluster_std=0.5, 
                  shuffle=True, 
                  random_state=0)

plt.scatter(X[:, 0], X[:, 1], 
            c='white', marker='o', edgecolor='black', s=50)
plt.grid()
plt.tight_layout()
#plt.savefig('images/11_01.png', dpi=300)
plt.show()
```


![png](clustering_6_0.png)



```python
# K-means clustering
from sklearn.cluster import KMeans

km = KMeans(n_clusters=3, 
            init='random', 
            n_init=10, 
            max_iter=300,
            tol=1e-04,
            random_state=0)

y_km = km.fit_predict(X)

# Plot the clusters with their centroids
plt.scatter(X[y_km == 0, 0],
            X[y_km == 0, 1],
            s=50, c='lightgreen',
            marker='s', edgecolor='black',
            label='Cluster 1')
plt.scatter(X[y_km == 1, 0],
            X[y_km == 1, 1],
            s=50, c='orange',
            marker='o', edgecolor='black',
            label='Cluster 2')
plt.scatter(X[y_km == 2, 0],
            X[y_km == 2, 1],
            s=50, c='lightblue',
            marker='v', edgecolor='black',
            label='Cluster 3')
plt.scatter(km.cluster_centers_[:, 0],
            km.cluster_centers_[:, 1],
            s=250, marker='*',
            c='red', edgecolor='black',
            label='Centroids')
plt.legend(scatterpoints=1)
plt.grid()
plt.tight_layout()
#plt.savefig('images/11_02.png', dpi=300)
plt.show()
```


![png](clustering_7_0.png)


Distortion: Within a cluster sum of squared error (SSE)  

$SSE = \sum_{i=1}^n\sum_{j-1}^k w^{(i,j)} ||x^{(i)} - \mu^{(j)}||_2^2$ 

where i is the sample index, and j is the cluster index. $\mu$ is the centroid for cluster j, and $w^{(i,j)}=1$ if the sample $x^i$ is in cluster j, 0 otherwise.


```python
# Find the elbow
distortions = []
for i in range(1, 11):
    km = KMeans(n_clusters=i, 
                init='k-means++', 
                n_init=10, 
                max_iter=300, 
                random_state=0)
    km.fit(X)
    distortions.append(km.inertia_)
plt.plot(range(1, 11), distortions, marker='o')
plt.xlabel('Number of clusters')
plt.ylabel('Distortion')
plt.tight_layout()
#plt.savefig('images/11_03.png', dpi=300)
plt.show()
```


![png](clustering_9_0.png)


#### Quantifying the quality of clustering via silhouette plots


```python
import numpy as np
from matplotlib import cm
from sklearn.metrics import silhouette_samples

km = KMeans(n_clusters=3, 
            init='k-means++', 
            n_init=10, 
            max_iter=300,
            tol=1e-04,
            random_state=0)
y_km = km.fit_predict(X)

cluster_labels = np.unique(y_km)
n_clusters = cluster_labels.shape[0]
silhouette_vals = silhouette_samples(X, y_km, metric='euclidean')
y_ax_lower, y_ax_upper = 0, 0
yticks = []
for i, c in enumerate(cluster_labels):
    c_silhouette_vals = silhouette_vals[y_km == c]
    c_silhouette_vals.sort()
    y_ax_upper += len(c_silhouette_vals)
    color = cm.jet(float(i) / n_clusters)
    plt.barh(range(y_ax_lower, y_ax_upper), c_silhouette_vals, height=1.0, 
             edgecolor='none', color=color)

    yticks.append((y_ax_lower + y_ax_upper) / 2.)
    y_ax_lower += len(c_silhouette_vals)
    
silhouette_avg = np.mean(silhouette_vals)
plt.axvline(silhouette_avg, color="red", linestyle="--") 

plt.yticks(yticks, cluster_labels + 1)
plt.ylabel('Cluster')
plt.xlabel('Silhouette coefficient')

plt.tight_layout()
#plt.savefig('images/11_04.png', dpi=300)
plt.show()
```


![png](clustering_11_0.png)


#### Quantifying the quality of clustering via silhouette plots for bad clusters


```python
km = KMeans(n_clusters=2,
            init='k-means++',
            n_init=10,
            max_iter=300,
            tol=1e-04,
            random_state=0)
y_km = km.fit_predict(X)

plt.scatter(X[y_km == 0, 0],
            X[y_km == 0, 1],
            s=50,
            c='lightgreen',
            edgecolor='black',
            marker='s',
            label='Cluster 1')
plt.scatter(X[y_km == 1, 0],
            X[y_km == 1, 1],
            s=50,
            c='orange',
            edgecolor='black',
            marker='o',
            label='Cluster 2')

plt.scatter(km.cluster_centers_[:, 0], km.cluster_centers_[:, 1],
            s=250, marker='*', c='red', label='Centroids')
plt.legend()
plt.grid()
plt.tight_layout()
#plt.savefig('images/11_05.png', dpi=300)
plt.show()


cluster_labels = np.unique(y_km)
n_clusters = cluster_labels.shape[0]
silhouette_vals = silhouette_samples(X, y_km, metric='euclidean')
y_ax_lower, y_ax_upper = 0, 0
yticks = []
for i, c in enumerate(cluster_labels):
    c_silhouette_vals = silhouette_vals[y_km == c]
    c_silhouette_vals.sort()
    y_ax_upper += len(c_silhouette_vals)
    color = cm.jet(float(i) / n_clusters)
    plt.barh(range(y_ax_lower, y_ax_upper), c_silhouette_vals, height=1.0, 
             edgecolor='none', color=color)

    yticks.append((y_ax_lower + y_ax_upper) / 2.)
    y_ax_lower += len(c_silhouette_vals)
    
silhouette_avg = np.mean(silhouette_vals)
plt.axvline(silhouette_avg, color="red", linestyle="--") 

plt.yticks(yticks, cluster_labels + 1)
plt.ylabel('Cluster')
plt.xlabel('Silhouette coefficient')

plt.tight_layout()
#plt.savefig('images/11_06.png', dpi=300)
plt.show()
```


![png](clustering_13_0.png)



![png](clustering_13_1.png)


### Understanding hierarchical clustering on a distance matrix


```python
# Start with random numbers
import pandas as pd
import numpy as np

np.random.seed(123)

variables = ['X', 'Y', 'Z']
labels = ['ID_0', 'ID_1', 'ID_2', 'ID_3', 'ID_4']

X = np.random.random_sample([5, 3])*10
df = pd.DataFrame(X, columns=variables, index=labels)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>X</th>
      <th>Y</th>
      <th>Z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ID_0</th>
      <td>6.964692</td>
      <td>2.861393</td>
      <td>2.268515</td>
    </tr>
    <tr>
      <th>ID_1</th>
      <td>5.513148</td>
      <td>7.194690</td>
      <td>4.231065</td>
    </tr>
    <tr>
      <th>ID_2</th>
      <td>9.807642</td>
      <td>6.848297</td>
      <td>4.809319</td>
    </tr>
    <tr>
      <th>ID_3</th>
      <td>3.921175</td>
      <td>3.431780</td>
      <td>7.290497</td>
    </tr>
    <tr>
      <th>ID_4</th>
      <td>4.385722</td>
      <td>0.596779</td>
      <td>3.980443</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calcuate distance matrix
from scipy.spatial.distance import pdist, squareform

row_dist = pd.DataFrame(squareform(pdist(df, metric='euclidean')),
                        columns=labels,
                        index=labels)
row_dist

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID_0</th>
      <th>ID_1</th>
      <th>ID_2</th>
      <th>ID_3</th>
      <th>ID_4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ID_0</th>
      <td>0.000000</td>
      <td>4.973534</td>
      <td>5.516653</td>
      <td>5.899885</td>
      <td>3.835396</td>
    </tr>
    <tr>
      <th>ID_1</th>
      <td>4.973534</td>
      <td>0.000000</td>
      <td>4.347073</td>
      <td>5.104311</td>
      <td>6.698233</td>
    </tr>
    <tr>
      <th>ID_2</th>
      <td>5.516653</td>
      <td>4.347073</td>
      <td>0.000000</td>
      <td>7.244262</td>
      <td>8.316594</td>
    </tr>
    <tr>
      <th>ID_3</th>
      <td>5.899885</td>
      <td>5.104311</td>
      <td>7.244262</td>
      <td>0.000000</td>
      <td>4.382864</td>
    </tr>
    <tr>
      <th>ID_4</th>
      <td>3.835396</td>
      <td>6.698233</td>
      <td>8.316594</td>
      <td>4.382864</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calculate Linkage matrix
from scipy.cluster.hierarchy import linkage
row_clusters = linkage(pdist(df, metric='euclidean'), method='complete')
pd.DataFrame(row_clusters,
             columns=['row label 1', 'row label 2',
                      'distance', 'no. of items in clust.'],
             index=['cluster %d' % (i + 1) 
                    for i in range(row_clusters.shape[0])])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>row label 1</th>
      <th>row label 2</th>
      <th>distance</th>
      <th>no. of items in clust.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>cluster 1</th>
      <td>0.0</td>
      <td>4.0</td>
      <td>3.835396</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>cluster 2</th>
      <td>1.0</td>
      <td>2.0</td>
      <td>4.347073</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>cluster 3</th>
      <td>3.0</td>
      <td>5.0</td>
      <td>5.899885</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>cluster 4</th>
      <td>6.0</td>
      <td>7.0</td>
      <td>8.316594</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
from scipy.cluster.hierarchy import dendrogram

# make dendrogram black (part 1/2)
# from scipy.cluster.hierarchy import set_link_color_palette
# set_link_color_palette(['black'])

row_dendr = dendrogram(row_clusters, 
                       labels=labels,
                       # make dendrogram black (part 2/2)
                       # color_threshold=np.inf
                       )
plt.tight_layout()
plt.ylabel('Euclidean distance')
#plt.savefig('images/11_11.png', dpi=300, 
#            bbox_inches='tight')
plt.show()
```


![png](clustering_18_0.png)


#### Even fancier with heatmaps in the dendrogram


```python
# plot row dendrogram
fig = plt.figure(figsize=(8, 8), facecolor='white')
axd = fig.add_axes([0.09, 0.1, 0.2, 0.6])

# note: for matplotlib < v1.5.1, please use orientation='right'
row_dendr = dendrogram(row_clusters, orientation='left')

# reorder data with respect to clustering
df_rowclust = df.iloc[row_dendr['leaves'][::-1]]

axd.set_xticks([])
axd.set_yticks([])

# remove axes spines from dendrogram
for i in axd.spines.values():
    i.set_visible(False)

# plot heatmap
axm = fig.add_axes([0.23, 0.1, 0.6, 0.6])  # x-pos, y-pos, width, height
cax = axm.matshow(df_rowclust, interpolation='nearest', cmap='hot_r')
fig.colorbar(cax)
axm.set_xticklabels([''] + list(df_rowclust.columns))
axm.set_yticklabels([''] + list(df_rowclust.index))

#plt.savefig('images/11_12.png', dpi=300)
plt.show()
```

    /var/folders/wn/k3vlc_7s4mjcszy_1l54z5qm0000gn/T/ipykernel_13006/1264724331.py:22: UserWarning: FixedFormatter should only be used together with FixedLocator
      axm.set_xticklabels([''] + list(df_rowclust.columns))
    /var/folders/wn/k3vlc_7s4mjcszy_1l54z5qm0000gn/T/ipykernel_13006/1264724331.py:23: UserWarning: FixedFormatter should only be used together with FixedLocator
      axm.set_yticklabels([''] + list(df_rowclust.index))



![png](clustering_20_1.png)

