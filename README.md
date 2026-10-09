# US-Arrests-PCA-Clustering-Unsupervised-Learning-
Using Principal Component Analysis (PCA) and two clustering methods, K-Means and hierarchical (Ward) clustering, to find groups of US states with similar violent-crime and urbanisation profiles.

This project was completed as part of the Artificial Intelligence online bootcamp (Stellenbosch University in partnership with HyperionDev).

What's inside
File	Description
unsupervised_task1.ipynb	Full notebook: exploration, scaling, PCA, biplot, both clustering methods and comparison
Dataset

The classic USArrests dataset: 1973 arrest rates for Murder, Assault and Rape (per 100,000 residents) and the percentage of urban population for each of the 50 US states. There are no missing values. The CSV is not included in this repo; add UsArrests.csv next to the notebook to run it.

Approach
Exploration: shape, data types, missing values and summary statistics. The features are on very different scales (Assault runs into the hundreds, UrbanPop is a percentage).
Standardisation: StandardScaler, so no feature dominates PCA just because of its units.
Correlation analysis: the three crime variables are positively correlated (0.56 to 0.80), with Murder and Assault the strongest pair. UrbanPop is only weakly related to them (0.07 with Murder, 0.41 with Rape at most).
PCA: explained variance, scree plot, and a biplot of PC1 vs PC2.
Choosing components: kept 2 components after the elbow in the scree plot.
Clustering on the 2 principal components: K-Means (k chosen with the elbow method and silhouette scores) and Agglomerative clustering with Ward linkage and a dendrogram, then a cross-tabulation to compare the two.
Results

PCA

Component	Variance explained	Cumulative
PC1	62.0%	62.0%
PC2	24.7%	86.8%
PC3	8.9%	95.7%
PC4	4.3%	100%
PC1 is an overall violent crime axis: Murder, Assault and Rape all load in the same direction.
PC2 is mainly urbanisation (UrbanPop), largely independent of crime.

K-Means (k = 3), silhouette score 0.401

Cluster	States	Murder	Assault	UrbanPop	Rape
High crime	20	12.2	255	68	29.2
Moderate crime, most urban	18	5.8	140	72	18.7
Low crime, least urban	12	3.5	77	51	11.8

Hierarchical (Ward, 3 clusters), silhouette score 0.377: produces groups of 19, 19 and 12 states with very similar profiles to K-Means. The two methods assign 45 of the 50 states (90%) to matching clusters.

Choosing k: k = 3 has a lower silhouette score (0.401) than k = 2 (0.476) or k = 4 (0.444). It was chosen because the elbow flattens around 3 to 4 and three groups (high, moderate, low) are easy to interpret.

Key takeaways
Four correlated features compress well into two components that keep about 87% of the variance.
Essentially two factors drive the differences between states: how violent and how urban.
Two different clustering algorithms agree on 90% of assignments, so the groupings look like real structure rather than an artefact of one method.
The five states grouped differently by the two methods sit near cluster boundaries.
Limitations
The data is from 1973 and only has four variables, so the findings describe that period and are not current.
Silhouette scores of 0.4 or lower mean the clusters overlap rather than forming clearly separate groups.
Tech stack

Python · pandas · NumPy · scikit-learn · SciPy · matplotlib · seaborn · Jupyter

How to run
Clone the repo.
Install dependencies:
bash
   pip install pandas numpy scikit-learn scipy matplotlib seaborn jupyter
Place UsArrests.csv in the same folder as the notebook.
Run all cells in unsupervised_task1.ipynb. The plots are also saved as PNG files.
