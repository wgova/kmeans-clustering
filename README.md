This tutorial explores different visualisations and multivariate analysis techniques on the iris dataset to benchmark and evaluate the effectiveness of k-means classification against its assumptions.

[Colab notebook](https://colab.research.google.com/github/wgova/kmeans-clustering/blob/master/notebooks/iris_analysis.ipynb)

## Exploratory data analysis
The iris dataset has some evidence of groups based on the species, but with evidence that two of the three species (Iris versicola and Iris virginica) have closely related properties. A clustering algorithm like k-means clustering might be able to separate these two species better, or find another dimension to separate the species.   
  
![Pairwise plot](https://github.com/wgova/eda_iris/blob/master/img/pairwise.png)

Poor separation of these species is clearly visible in the radviz plot, a multi-variate data based on a simple spring tension minimization algorithm.

![Radviz plot](https://github.com/wgova/eda_iris/blob/master/img/radviz.png)

These two species are also not easy to separate using Andrews curves, another simple multivariate visualisation aid plotted using the attributes of samples as coefficients for Fourier series.

![Andrews plot](https://github.com/wgova/eda_iris/blob/master/img/andrews.png)

The difficulty in separating the two iris species seems to be due to the fact that all their properties have comparable magnitudes of measurement, i.e Sepals (lengths and widths) and Petals (lengths and widths) 

![Measures against average for sepals](https://github.com/wgova/eda_iris/blob/master/img/aboveavg_scatter.png)

![Measures against average for petals](https://github.com/wgova/eda_iris/blob/master/img/petals.png)

As previously observed, based on the properties provided, there are two iris species that cannot be separated into separate groups.

![Ground truth groupings](https://github.com/wgova/eda_iris/blob/master/img/petals.png)

## K-means clustering

The elbow method and silhouette method both suggest that 3 clusters will be sufficient to cluster samples in the iris dataset

![Optimum clusters](https://github.com/wgova/eda_iris/blob/master/img/optimisation.png)

The k-means clustering algorithm was set up to have _n_init_ of 1 to prevent the same centroid from being initialised multiple times. In order to speed up convergence, _n_jobs_ was set to 4 to initialise multiple centroids at a time. Because the kmeans algorithm does not always find the global optimum, _max_iter_ used were 10000 and the _algorithm_ was set to "auto", in case the *elkan* setup outperforms the classical Lloyd's algorithm depending on how dense the data is. Unfortunately, k-means clustering did not result in formation of highly homogenous clusters, as intended. 

![Optimum clusters](https://github.com/wgova/eda_iris/blob/master/img/kmeans_clusters.png)

The formation of more homogenous clusters might be achieved by a dimensionality reduction algorithm like Principal Component Analysis (PCA) to transform properties from Euclidean to unit matrices. This will allow properties that are closely related between the species to be averaged in a dimension that minimizes distance from a point to the line, such as squared distance,to improve signal to noise ratio.







