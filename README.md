# Customer_Segmentation

## Project Excesive Summary
This project aims to establish a customers segmentation for telecom consumption. The
target is to divide them into 3 stages of different “maintaining value”, high-value
customers, medium-value customers and lower-value customers with the
RMF(Recency, Monetary and frequency) evaluation. Based on the "maintaining value", analysis on clusters is applied to profile high value customers in order to establish consumption attracting business methods.

## Data Description

There are 5000 rows and 59 columns in the customer dataframe. Because the number of features is large, Pandas_Profiling is introduced to plot the description about all features. The columns include a unique id 'CustomerID' and no target feature. 41 features of type "Object". Therefore we are going to build an **unsupervised clustering model**.

![image](https://user-images.githubusercontent.com/38795845/130334895-cb360f56-5667-408b-90ce-a3b36e52abb3.png)


- Duplicates Check:

Check is held towards the unique id, there is no duplicates in this dataset.
- Null Check:

There are nulls in columns 'Gender' of 33 nulls, 'JobCategory' of 15 nulls, 'HouseholdSize' of 8, 'NumberPets' of 6, 'NumberCats' of 7, 'NumberDogs' of 8, 'NumberBirds' of 34, 'HomeOwner' of 13. The counts of nulls are small compared to the total 5000 cases. And for building clusters through RMF model, we are not using these features. So nulls are not going to be dropped in this project. 


## Methodology

1. RMF evaluation
2. K-mean Clusters.
The RFM model is mostly used in known target data sets and it has certain
limitations. This project will use a widely applicable K-Means clustering, which
belongs to unsupervised machine learning.
The main process is to generate R-M-F variables with existing variables in the dataset.

Recency, frequency, monetary value is a marketing analysis tool used to identify a
company's or an organization's best customers by using certain measures. The RFM
model is based on three quantitative factors:

1. Recency: How recently a customer has made a purchase, and how much the
purchase is
2. Frequency: How often a customer makes a purchase
3. Monetary Value: How much money a customer spends on purchases

To prepare for the evaluation, it’s necessary to generate these information from
existing variables.
From observation, following features are recording customers’ monetary activities:

![image](https://user-images.githubusercontent.com/38795845/130334855-4d9ed13b-f30a-446e-a47e-1babf67aa431.png)

However, most of these variables are recorded in currency format. It’s necessary to
transfer them into float type, which is named ‘~_Coded’ after transfer.
- For R, the recency value, I add three telecom related variables of
‘~LastMonth’ into one ‘TotalLastMonth’ to record the total spend in the last
month on telecom services. And it’s used to evaluate the most recent spending
on telecom service.
- For M, the monetary value, I add three telecom related variables of
‘~OverTenure’ into one ‘TotalTenure’ to record the total spend over tenure on
telecom services.
- For F, the frequency value, I choose the ‘CardItemsMonthly’ as an average
value of willing to consume for the samples.


## Kth Nearest Neighbor Output

The RFM model is mostly used in known target data sets and it has certain
limitations. This project will use a widely applicable K-Means clustering, which
belongs to unsupervised machine learning.
Because the K-Means algorithm is very simple and could be well generated with the
RMF model. For a given sample set, divide the sample set into K clusters according
to the distance between the samples, so that the points in the clusters are connected as
closely as possible, and the distance between the clusters is as large as possible.
Also, our main variables are all numerical, and we have an expected judgment on the
number of classifications K. At this time, K-means clustering can be used. The system
will divide all points into K categories according to the distance from these
classification points. And our data objects include both observations and targets. The
target is to divide customers into different priority stages:
1. High-value customers: who are highly willing to buy. They are the most
important to maintain.
2. Medium-value customers: who are at average spending stage.They are the
majority and still important to maintain, with less priority.
3. Low-value customers: who consume less service. They could be maintained
with least focus, because the revenue of maintaining is relatively low.

### Data preprocessing for KNN

![image](https://user-images.githubusercontent.com/38795845/130334926-1347305e-1b81-4bec-8b5c-d4e49d6554c4.png)![image](https://user-images.githubusercontent.com/38795845/130334943-0bf18d44-444a-4f15-94aa-bf921b0b2cb0.png)


Scaled:

![image](https://user-images.githubusercontent.com/38795845/130334949-3fca5bf0-843a-40c2-8222-510e81444aef.png)

### Search for the best # of Clusters of the KNN model throguh Silhouette Score

![image](https://user-images.githubusercontent.com/38795845/130334956-bcd6cf29-5140-4cf4-af55-34a05b5203cf.png)

A model with **3 clusters** will be the best for KNN model.

### 3 cluster KNN result

Append cluster # to every instance:

![image](https://user-images.githubusercontent.com/38795845/130334972-e1cd0926-f88f-42f3-b1df-156558ef205c.png)

IQR Binning Values:
Q1, medium, Q3

![image](https://user-images.githubusercontent.com/38795845/130334988-688316bb-1746-4c33-891b-c175eaafa9c8.png)

- R: 'TotalLastMonth' Distribution among clusters:


![image](https://user-images.githubusercontent.com/38795845/130334994-7771ad8a-3d25-4690-a38a-84d741f606b1.png)

- M: 'TotalTenure' Distribution among clusters:


![image](https://user-images.githubusercontent.com/38795845/130335001-750f8449-dc70-4ed7-82aa-0f9982aca429.png)

- F: 'CardItemsMonthly' Distribution among clusters:

![image](https://user-images.githubusercontent.com/38795845/130335004-82b3a6c3-f924-4bce-9acf-8bb9356fc6ec.png)

### Cluster Output

- Cluster 1:

is the cluster occupying 47.3% (about a half) of total customers, with the largest crowd paying less than $87.3 for Total Last Month Service, and total consumption less than 2088 over whole tenure. Moreover, cluster 1 people do not buy more than 10 items monthly. These customers have the least willing to buy new products.

- Cluster 2:

17% (less than a quater) of all cases. It is the cluster for customers with the highest consumption amount. Cluster 2 cases occupy 67.49% of consumption over $87.3 the last month and 67.5% of payment larger than 2088 over total tenure. This cluster is the one for the most valuable customers to retain.

- Cluster 3:

35.7% of all cases. Customers in this cluster tend to buy more items than others. However, their spent is close to cluster 1. Cluster 2 occupy 81.8% of cases buying more than 12 itmes monthly and 76.7% of cases buying more than 10 items monthly. Meanwhile people in cluster 2 has less cases consuming larger > $87.3 than cluster 1 and less cases totally paying >2088 than cluster 1.

### To encourage consumption

Cluster 2 is the most important cluster to analyze and then cluster 3. Cluster 1 should be put in the retention analysis.

### Clusters Description

Plot the boxplots of features of three clusters to see if there are important triggers for high consuming crowd. Outliers are not displayed because we are focusing on the general difference.


![image](https://user-images.githubusercontent.com/38795845/130335442-09a703bf-6812-4b82-b9a1-816c105375be.png)

## Analysis

- From the boxplots above, following features do not distinct between 3 clusters:
Region, TownSize, Gender, UnionMember, Retired, DebtToIncomeRatio, MaritalStatus, HouseholdSize, NumberPets, NumberCats, NumberBirds, HomeOwner, CarsOwned, CommuteTime, PoliticalPartyMem, Votes, ActiveLifestyle, EquipmentRental, CallerID, CallWait, CallForward, ThreeWayCalling, EBilling, TVWatchingHours, OwnsMobileDevice, OwnsGameSystem.

- Following are features significantly differring:
   
   Cluster 2 have more and cluster 1&3 have none or less: OwnsFax, NewsSubscriber, OwnsPC, Pager, VM, Multiline, WirelessData, CallingCard, EquipmentLastMonth, VoiceLastMonth, PhoneCoTenure, CarValue, NumberDogs, CreditDebt, OtherDebit, HHIncome, EmploymentLength, EducationYears, Age.

   Cluster 2 have less than other clusters: HouseholdSize

- Significant Difference between Cluster 1&3:
Cluster 1 has True LoanDefault while cluster 3 does not has.

- Category features analysis:
All JobCategory and CarOwnership and CarBrand features have similar distribution among three clusters. Despite the 'JobCategory_Sales', cluster 2 has most False value, while other 2 clusters has more cases with a sales job.

![image](https://user-images.githubusercontent.com/38795845/130335454-df24cb96-6471-4b83-8315-a637b3f1b748.png)

## Conclusion & Business Suggestion

From the cluster description analysis, it is clear that customers with more added service than calling are the ones willing to spend. They tend to use wireless data, buy more expensive cars, have more dogs. They generally have higher household income as well as get educated for more years (which means normally higher education) and tend to held debit. Cluster 2 customers are older in Age and stay with the the telecom company for the longest. 

For cluster 2, the company could develop and marketing more new services to them. 

For cluster 3, the company could offer them discounts to attract them to add new services like wireless data. Through the trial, they are possibly going to stay with new services. 

For cluster 1, due to they are facing pressure of Loan. They are the least possible to add services to monthly plans. They should be put at the retention group with no further aggressive marketing. 
