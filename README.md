DMBI Experiment 7 – Bank Customer Churn System
Experiment Title
To Implement K-Means Clustering Using RapidMiner on the Bank Customer Churn System Dataset
Aim
To implement the K-Means clustering algorithm using RapidMiner (Altair AI Studio) on the Bank Customer Churn System dataset and group customers according to similarities in their numerical characteristics.
Theory
1. Data Mining
Data mining is the process of discovering useful patterns, relationships and knowledge from large datasets. It combines techniques from statistics, databases and machine learning to convert raw data into meaningful information. In banking, it can help understand customer behaviour, identify customer segments, study account usage patterns and support business decisions.
2. Clustering
Clustering is an unsupervised machine learning technique used to divide a dataset into groups called clusters. Records placed in the same cluster are expected to have similar characteristics, while records in different clusters should be comparatively dissimilar. Unlike classification, clustering does not require a pre-defined target class during model training.

For this experiment, the Exited attribute is excluded from clustering because it represents the known churn outcome. It can be examined separately after clustering, but it must not influence cluster formation.
3. K-Means Clustering
K-Means is a partition-based clustering algorithm. The user specifies the number of clusters, represented by K. The algorithm initially selects K cluster centres, called centroids. Each data record is assigned to the nearest centroid, usually using Euclidean distance. The centroid of each cluster is recalculated as the mean of the records assigned to it. These steps repeat until assignments stop changing significantly or the maximum number of iterations is reached.

The objective is to minimize the within-cluster sum of squared distances.
4. Main Steps of K-Means
1. Choose the number of clusters K.
2. Initialize K cluster centroids.
3. Calculate the distance between each record and every centroid.
4. Assign each record to the nearest centroid.
5. Recalculate each centroid using the mean of its assigned records.
6. Repeat the assignment and update steps until convergence.
5. Distance Measurement
K-Means commonly uses Euclidean distance:

d(x, y) = sqrt((x1-y1)^2 + (x2-y2)^2 + ... + (xn-yn)^2)

A smaller distance indicates that two records are more similar in the selected feature space. Since attributes may have different units and ranges, normalization is important before calculating distances.
6. Normalization using Z-Transformation
Z-transformation standardizes a numerical attribute by subtracting its mean and dividing by its standard deviation:

z = (x - μ) / σ

Here, x is the original value, μ is the attribute mean and σ is its standard deviation. This prevents large-range attributes such as Balance and EstimatedSalary from dominating distance calculations.
7. Advantages and Limitations
Advantages
- Simple to understand and implement.
- Works efficiently on large numerical datasets.
- Produces clear cluster assignments for every record.
Limitations
- K must be selected before running the algorithm.
- Results may depend on initial centroid positions.
- Sensitive to outliers and improperly scaled features.
- Works best when clusters are reasonably compact and separated.
8. RapidMiner / Altair AI Studio
RapidMiner, now known as Altair AI Studio, is a visual data science platform. It provides operators that can be connected to form a workflow. Operators retrieve data, select attributes, handle missing values, normalize data and apply machine learning algorithms. Results can be inspected through data tables, statistics, visualizations and model descriptions.
Tool and Dataset Information
- Tool: RapidMiner / Altair AI Studio
- Dataset: Bank Customer Churn System
- File name: Churn_Modelling.csv
- Number of records: 10,000
- Original attributes: 14
- Selected clustering features: 8 numerical attributes
- Number of clusters: K = 4
Selected Attributes
Attribute	Description
CreditScore	Credit score of the customer
Age	Age of the customer
Tenure	Number of years the customer has been with the bank
Balance	Account balance of the customer
NumOfProducts	Number of bank products held by the customer
HasCrCard	Whether the customer has a credit card (0/1)
IsActiveMember	Whether the customer is an active member (0/1)
EstimatedSalary	Estimated salary of the customer


Excluded attributes: RowNumber, CustomerId, and Surname are identifiers; Geography and Gender are categorical attributes not used in this numerical-feature workflow; Exited is the known churn outcome and is excluded to keep clustering unsupervised.
RapidMiner / Altair AI Studio Procedure
1. Data Preprocessing
1. Open RapidMiner / Altair AI Studio and create a new process.
2. Import Churn_Modelling.csv into the Repository.
3. Add Retrieve and select the Bank Customer Churn System dataset.
4. Add Select Attributes and retain the eight numerical features listed above.
5. Add Replace Missing Values and use the average method for numerical attributes, if missing values are present.
6. Add Normalize and select Z-transformation.
7. Connect the output to the K-Means clustering operator.
2. Applying K-Means
1. Add the K-Means (Clustering) operator after Normalize.
2. Enable the option to add a cluster attribute.
3. Set the number of clusters (K) to 4.
4. Keep other parameters at their default values unless instructed otherwise.
5. Connect the clustered ExampleSet and Cluster Model outputs to result ports.
6. Run the process and inspect the generated results.
3. Workflow
Retrieve → Select Attributes → Replace Missing Values → Normalize → K-Means
Python Equivalent Implementation
The supplied bank_customer_churn_system_exp7.py implements the same main clustering workflow in Python:
1. Load the dataset.
2. Select the same eight numerical attributes.
3. Replace missing numerical values with the mean.
4. Apply Z-transformation using StandardScaler.
5. Apply K-Means with K = 4.
6. Display cluster counts and create an Age-versus-Balance scatter plot.
7. Calculate Silhouette Score and Davies-Bouldin Index.
8. Calculate a sampled Dunn Index estimate.
9. Save cluster assignments and summary CSV files.
Install dependencies
pip install pandas numpy matplotlib seaborn scikit-learn scipy
Run locally
Keep Churn_Modelling.csv in the same folder as the Python script, then run:
python bank_customer_churn_system_exp7.py
Run in Google Colab
Run the script in a Colab notebook. It detects Google Colab and asks you to upload Churn_Modelling.csv.
Output Files Generated
- bank_customer_churn_cluster_counts.csv – number of customers in each cluster.
- bank_customer_churn_clustered_dataset.csv – dataset with an added Cluster column.
- bank_customer_churn_kmeans_clusters.png – Age versus Balance cluster visualization.
- bank_customer_churn_cluster_churn_profile.csv – optional churn percentages by cluster, calculated after clustering only.
Understanding the Outputs
- Cluster Model / cluster counts: Shows the number of records assigned to each cluster.
- Clustered ExampleSet: Shows customer records with their assigned cluster labels.
- Cluster Visualization: Shows a two-dimensional projection using Age and Balance. The K-Means model uses all eight selected features, so the plot is only a projection of the clustering result.
- Clustering Performance: Silhouette, Davies-Bouldin and Dunn indices can be used to assess clustering quality. Their interpretation depends on the exact definition and implementation.
Important about the supplied PDF figures: The PDF explicitly states that the output panels are illustrative mock-ups, not verified captures of an actual RapidMiner run. The cluster counts and performance values shown in those figures must not be reported as measured results. Run the process and record actual results from your own execution.
Result
The K-Means clustering workflow for the Bank Customer Churn System dataset is implemented using eight selected numerical customer attributes. The workflow includes attribute selection, missing-value handling, Z-transformation normalization and K-Means clustering with K = 4. Actual cluster counts and evaluation values should be entered only after running the process.
Conclusion
K-Means is an unsupervised clustering algorithm that groups similar records using distance measurements. In this experiment, it is applied to the Bank Customer Churn System dataset using CreditScore, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember and EstimatedSalary. Data preprocessing and Z-transformation are important because K-Means is distance-based. The generated cluster labels can support customer segmentation and further analysis of customer characteristics. The Exited attribute is excluded from cluster formation and may be examined separately after clustering.
