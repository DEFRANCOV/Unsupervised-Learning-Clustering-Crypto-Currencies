# UNSUPERVISED LEARNING: CLUSTERING

This exercise will use the PCA algorithm along with Kmeans algorithm from sklearn to classify the numerous crypto-currencies.


There are four steps:  
1. Preprocessing: Prepare data for dimension reduction.  
2. Reducing Data Dimensions Using PCA.
3. Use K-Means to predict clusters.
4. Visualize the results.

You can see the full code [here](Val_crypto_clustering.ipynb).

## Data Pre-Processing
After importing all of the appropriate libraries, we read in the CSV, as we were unable to read in from the API.
Some of the manual adjustments we will make are:
* Keep only cryptocurrencies that are trading 
* Keep only cryptocurrencies with a working algorithm
* Remove rows with at least 1 null value 
* Drop rows where there are 'N/A' text values
* Create an index column which we name "Cointype".

For the algorithms, we need to:
* convert string values into numerical values.   In our case we have two columms "Algorithm" and "Prooftype" that have can have various string values.  In kernel 18, we create a dummy boolean value for each possible string value.   This dramatically expands the number of columns in the DataFrame.
* scale the columns in the X DataFrame to a normalized distribution.   This is kernel 19.

## Using PCA to reduce dimensions

Next we use the pca algorithm to reduce the scaled dataframe into a three "pca dimensions".  This DataFrame is called "pcs_df".  The algorithm uses core (in our case three) dimensions to analyze relationships between the data.   This helps with resource allocation.

## Using K-Means to figure out appropriate clusters

In kernel 23, we plot an elbow curve that plots "inertia" from a range of 1 cluster to 11.   Looking at the elbow curve,![curve](Elbow-Curve.PNG)

the inertia inflects at value 4, so we will use 4 clusters as our parameter. In kernel 24, we run the K-means model and we create the "clustered_df".  Some visual results are seen in kernel 25 (scatter-chart:  vertical axis is Principal Component 1, the flat axes are for Principal Components 2 and 3) and kernel 26 (a partial view of first 11 currencies).   

![scatter-chart](Scatter-Chart.PNG)
![classification-table](Classification-Table.PNG)

The remainder of the code creates a new DataFrame "new-clustered-df" for the purposes of creating new charts.  In order to improve the visual output (particularly along the axes) for the new charts, we scale the two columns "TotalCoinsMined" and "TotalCoinSupply" from "clustered_df". We use the min-max scaler which is different than the standardized scaler.  Once these columns are scaled, we create a "MMS_df" and concatenate it with "clustered_df" which and the concatenated result is new-clustered-df as referenced above.  The new output is in kernels 33 and 34.  The values along the axes are more understandable and does not change any relationships between the data.


