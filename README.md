# Customer-Retention-Strategies

![CLV](https://news.vaimo.com/hubfs/Blog%202018%20/blog_post_imglifetime.jpg)
## INTRODUCTION
The most crucial asset for a retail organization is its customers. In the early times, a more frequent customer was provided better recognition by the staff, but how do we achieve this in the new age of e-commerce. The metrics for a superior customer have changed and so has the context of frequent visits.

The best customer retention tactics enable the seller to create lasting relationships with consumers who will become loyal to their brand. They might even spread the word within their own circles of influence, which could turn them into brand ambassadors.

For every business, to start investing in a unique and different strategy is time-consuming and demands a high amount of resources. So, understanding why CLV is crucial for the survival and growth of the business is really important. 


## PROBLEM STATEMENT
The task at hand is to improvize customer retention strategies using:
1. Customer Lifetime Value - Understand the approximate duration to recoup the Customer Acquisition Cost (CAC)  and also make a decision if the investment will follow through or not 
2. Customer Segmentation - Which segments to target to maximise profitability?

Finally, provide specific strategies based on customer segments and their respective CLV scores.

## APPROACH AND CONCEPTS
* **Data gathering and cleaning** - The dataset contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The dataset contains transaction-level data of customers with 541,909 rows and 8 columns.
This data had a lot of records that did not contain Customer IDs or had negative order quantities and hence data cleaning is required.

  The following steps were performed to clean the data:
    * Records that had negative order quantities and monetary values were filtered out
    * Only records with a Customer ID were kept

  For the probabilistic approach followed, some additional data processing steps have been taken:
    * The orders were grouped by day instead of InvoiceNo because the minimum time unit used by the probabilistic model is a day
    * Only customers who bought something in the past 90 days are considered
    * Only the fields that were useful for the probabilistic model are retained

* **train-test split** - A threshold date needed to be chosen in order to prepare the data for training the model. That date separates the orders into two partitions:
Orders before the threshold date are used to train the model
Orders after the threshold date are used to compute the target value
  
  The threshold date chosen for our analysis is 09/09/2011.

* **Feature Engineering** - After the split of the data into training and target intervals, aggregated data is used to create features and targets for each customer.
The new features are defined as follows:
  * monetary_btyd: The average of all orders' monetary values for each customer during the features period. The probabilistic model assumes that the value of the first order is 0. This has been manually enforced
  * Recency: The time between the first and last orders that were placed by a customer during the features period
  * frequency_btyd: The number of orders placed by a customer during the features period minus the first one
  * frequency_btyd_clipped: Same as frequency_btyd, but clipped by cap outliers
  * monetary_btyd_clipped: Same as monetary_btyd, but clipped by cap outliers
  * target_monetary_clipped: Same as target_monetary, but clipped by cap outliers
  * Target_monetary: The total amount spent by a customer 

## **Modeling** - 
  * CLV: For the model implementation, we have followed a two-step approach. We have started with determining the rate at which customers will make future transactions. Then, we have predicted the rate at which customers will drop out off of the system in the future. To identify these, we have implemented Pareto/NBD or BG/NBD. We have used these results to calculate customers’ monetary value.
  * Segmentation: To achieve segmentation, we perform clustering on all 3 metrics individually - Recency, Frequency, and Monetary value. k-means is used as the model and based on the optimum number of clusters, we perform weighted sum and achieve an overall score. After analyzing the mean Recency, Frequency, and monetary values of these clusters, we can observe three major groups being formed. We will label then Low Value, Mid Value, and High-Value customers

## **Marketing Strategy Recommendations** - 
* Further segregating on bought items analysis - affinity to certain products, affordability, brand-conscious, etc. and sending out advertisements, emails, coupons on this analysis 
* For customers with sporadic buying patterns, offering options of buy now and pay later schemes or pay in installments 
* For customers that are potential brand loyalists, converting them to brand ambassadors would be cost-effective and highly profitable in the long run. This could be achieved through elite memberships, exclusive coupons, special offers
* For customers who haven’t bought lately, sending emails about upcoming sales, offering them exclusive offers for their continuous love towards the brand, and staying in touch through reminders. Continuous emails beyond a certain point might also alienate the customer so the number needs to be set on a combination of surveys, past experiences and domain knowledge


## **Segment Specific Recommendatios** - 
  * For high-value customers, we know that these customers buy less frequency but are high revenue purchasers. They also haven’t bought any products lately. Therefore we need to inquire if they are sleeping or dead customers. They could also be groups that purchase products based on certain period gaps, for instance, customers who shop based on season or customers who shop based on quarterly bonuses
  * For our mid-value customers, they haven’t bought recently but have a considerable range with respect to frequency and revenue. They could be potential brand loyalists. They could also be high revenue generators that either buy large quantities or have an affinity towards expensive items. We need to dig a little deeper into this but overall need to increase their recency. 
  * For our low value, we know that they buy less frequency and have low revenue purchases but they have sporadic buying patterns, which is an attribute the business could leverage and improve

## References
* https://www.shopify.com/encyclopedia/customer-lifetime-value-clv
* https://www.crazyegg.com/blog/customer-lifetime-value/
* https://cran.r-project.org/web/packages/BTYD/vignettes/BTYD-walkthrough.pdf
* https://pypi.org/project/Lifetimes/


## REPOSITORY DETAILS
Access -
1. [Report - Details of Approach and Results](https://github.com/arnavd17/Instacart-Market-Basket-Analysis/blob/master/Instacart%20-%20Customer%20Segmentation%20%26%20Association%20Rule%20Mining.pdf)
2. [Data](https://github.com/arnavd17/Instacart-Market-Basket-Analysis/blob/master/Instacart_EDA.ipynb)
3. [Code](https://github.com/arnavd17/Instacart-Market-Basket-Analysis/blob/master/Association_rule_mining%20-%20Generators.ipynb)
