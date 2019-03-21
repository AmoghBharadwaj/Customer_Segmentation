
# **Credit Card Customer Segmentation**

# **Business Problem**

**Numbers and Statistics**


*   The credit card industry is big business, and it is dominated by a handful of companies.

* American consumers collectively are flirting with $1 trillion in credit card debt in mid-2017, according to the Federal Reserve consumer credit report.1  The top four issuers provide more than 57 percent of all the cards issued by 5,231 banks. The top 10 issuers issued nearly 90 percent.13

*  There were some 14.5 billion U.S. general purpose credit card transactions in the first six months of 2015, accounting for more than $1.4 trillion in purchase volume.27 General purpose credit card spending has risen as a proportion of gross domestic 
product, rising from 10 percent of GDP in 2000 to 15 percent in 2014.2

*  The total number of credit card transactions in the U.S. was 26.2 billion in 2012, up from 21 billion in 2009,3 according to the 2013 Federal Reserve Payments Study. 

*  At the end of 2014, there were approximately 3.4 billion smart chip cards in circulation around the globe, per EMV Connection.22 Today, U.S. card issuers are in the midst of upgrading approximately 1.2 billion credit and debit cards to smart chip cards.25  Approximately 400 million chip cards were issued in the U.S. by the end of 2015.22

** The Problem **

Anyone searching on a credit card comparison website is already in the market for a new credit card and is actively searching for the best deal. These are either:

* Primary market consumers (first-time credit card applicants, often with no credit history)

* People who are dissatisfied with their current credit card and have made their minds up to switch, or

* People who have identified a strategic reason to add a second or third credit card to their arsenals.

**Market segmentation**

* With different motivations like those above, it's hard to know what consumers are thinking, but it does point to the importance of market segmentation. In other words, know which consumers are interested more in rewards and which are interested more in low prices - and give both segments what they want.

* To a great degree, this is already happening. Marketers are sophisticated enough to know what consumers they want - high-spending ones, of course - and are targeting them with the juiciest offers.

* The number one challenge faced by marketers is to understand who they are selling to. When you know your buyers’ personas you can tailor your targeting and offerings to increase their satisfaction and your revenue as a result. When you already have a pool of customers and enough data, it can be very useful to segment them.

# **Objective**

The data for this analysis was taken from Kaggle
Data Set : https://www.kaggle.com/arjunbhasin2013/ccdata



*   Create customer segmentation to help the credit card companies for Targeted Marketing
*   Come up with recommendations/ strategies to target different segments



# **Obtaining the Data**


```python
#Importing necessary packages to do data manipulation and Exploratory data analysis
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
from google.colab import drive, files
drive.mount('/content/drive/')
path = "/content/drive/My Drive/Customer_segmentation/CC_GENERAL.csv"
```

    Drive already mounted at /content/drive/; to attempt to forcibly remount, call drive.mount("/content/drive/", force_remount=True).
    


```python
df = pd.read_csv(path)
```


```python
df.head(10)
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
      <th>CUST_ID</th>
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C10001</td>
      <td>40.900749</td>
      <td>0.818182</td>
      <td>95.40</td>
      <td>0.00</td>
      <td>95.40</td>
      <td>0.000000</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0</td>
      <td>2</td>
      <td>1000.0</td>
      <td>201.802084</td>
      <td>139.509787</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C10002</td>
      <td>3202.467416</td>
      <td>0.909091</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>6442.945483</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.250000</td>
      <td>4</td>
      <td>0</td>
      <td>7000.0</td>
      <td>4103.032597</td>
      <td>1072.340217</td>
      <td>0.222222</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C10003</td>
      <td>2495.148862</td>
      <td>1.000000</td>
      <td>773.17</td>
      <td>773.17</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>12</td>
      <td>7500.0</td>
      <td>622.066742</td>
      <td>627.284787</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>C10004</td>
      <td>1666.670542</td>
      <td>0.636364</td>
      <td>1499.00</td>
      <td>1499.00</td>
      <td>0.00</td>
      <td>205.788017</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>1</td>
      <td>1</td>
      <td>7500.0</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>C10005</td>
      <td>817.714335</td>
      <td>1.000000</td>
      <td>16.00</td>
      <td>16.00</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>1</td>
      <td>1200.0</td>
      <td>678.334763</td>
      <td>244.791237</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>5</th>
      <td>C10006</td>
      <td>1809.828751</td>
      <td>1.000000</td>
      <td>1333.28</td>
      <td>0.00</td>
      <td>1333.28</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.000000</td>
      <td>0.583333</td>
      <td>0.000000</td>
      <td>0</td>
      <td>8</td>
      <td>1800.0</td>
      <td>1400.057770</td>
      <td>2407.246035</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>6</th>
      <td>C10007</td>
      <td>627.260806</td>
      <td>1.000000</td>
      <td>7091.01</td>
      <td>6402.63</td>
      <td>688.38</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>64</td>
      <td>13500.0</td>
      <td>6354.314328</td>
      <td>198.065894</td>
      <td>1.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>7</th>
      <td>C10008</td>
      <td>1823.652743</td>
      <td>1.000000</td>
      <td>436.20</td>
      <td>0.00</td>
      <td>436.20</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>12</td>
      <td>2300.0</td>
      <td>679.065082</td>
      <td>532.033990</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>8</th>
      <td>C10009</td>
      <td>1014.926473</td>
      <td>1.000000</td>
      <td>861.49</td>
      <td>661.49</td>
      <td>200.00</td>
      <td>0.000000</td>
      <td>0.333333</td>
      <td>0.083333</td>
      <td>0.250000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>5</td>
      <td>7000.0</td>
      <td>688.278568</td>
      <td>311.963409</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>9</th>
      <td>C10010</td>
      <td>152.225975</td>
      <td>0.545455</td>
      <td>1281.60</td>
      <td>1281.60</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.166667</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>3</td>
      <td>11000.0</td>
      <td>1164.770591</td>
      <td>100.302262</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Let us get more info on the columns and the number of entries
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 8950 entries, 0 to 8949
    Data columns (total 18 columns):
    CUST_ID                             8950 non-null object
    BALANCE                             8950 non-null float64
    BALANCE_FREQUENCY                   8950 non-null float64
    PURCHASES                           8950 non-null float64
    ONEOFF_PURCHASES                    8950 non-null float64
    INSTALLMENTS_PURCHASES              8950 non-null float64
    CASH_ADVANCE                        8950 non-null float64
    PURCHASES_FREQUENCY                 8950 non-null float64
    ONEOFF_PURCHASES_FREQUENCY          8950 non-null float64
    PURCHASES_INSTALLMENTS_FREQUENCY    8950 non-null float64
    CASH_ADVANCE_FREQUENCY              8950 non-null float64
    CASH_ADVANCE_TRX                    8950 non-null int64
    PURCHASES_TRX                       8950 non-null int64
    CREDIT_LIMIT                        8949 non-null float64
    PAYMENTS                            8950 non-null float64
    MINIMUM_PAYMENTS                    8637 non-null float64
    PRC_FULL_PAYMENT                    8950 non-null float64
    TENURE                              8950 non-null int64
    dtypes: float64(14), int64(3), object(1)
    memory usage: 1.2+ MB
    

We see that there are 8950 entries, and 18 behavioral variables  in total, in which all are numerical and cust_id indicating the customer id who has owns the card


```python
df.describe()
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8949.000000</td>
      <td>8950.000000</td>
      <td>8637.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1564.474828</td>
      <td>0.877271</td>
      <td>1003.204834</td>
      <td>592.437371</td>
      <td>411.067645</td>
      <td>978.871112</td>
      <td>0.490351</td>
      <td>0.202458</td>
      <td>0.364437</td>
      <td>0.135144</td>
      <td>3.248827</td>
      <td>14.709832</td>
      <td>4494.449450</td>
      <td>1733.143852</td>
      <td>864.206542</td>
      <td>0.153715</td>
      <td>11.517318</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2081.531879</td>
      <td>0.236904</td>
      <td>2136.634782</td>
      <td>1659.887917</td>
      <td>904.338115</td>
      <td>2097.163877</td>
      <td>0.401371</td>
      <td>0.298336</td>
      <td>0.397448</td>
      <td>0.200121</td>
      <td>6.824647</td>
      <td>24.857649</td>
      <td>3638.815725</td>
      <td>2895.063757</td>
      <td>2372.446607</td>
      <td>0.292499</td>
      <td>1.338331</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>50.000000</td>
      <td>0.000000</td>
      <td>0.019163</td>
      <td>0.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>128.281915</td>
      <td>0.888889</td>
      <td>39.635000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1600.000000</td>
      <td>383.276166</td>
      <td>169.123707</td>
      <td>0.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>873.385231</td>
      <td>1.000000</td>
      <td>361.280000</td>
      <td>38.000000</td>
      <td>89.000000</td>
      <td>0.000000</td>
      <td>0.500000</td>
      <td>0.083333</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>3000.000000</td>
      <td>856.901546</td>
      <td>312.343947</td>
      <td>0.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2054.140036</td>
      <td>1.000000</td>
      <td>1110.130000</td>
      <td>577.405000</td>
      <td>468.637500</td>
      <td>1113.821139</td>
      <td>0.916667</td>
      <td>0.300000</td>
      <td>0.750000</td>
      <td>0.222222</td>
      <td>4.000000</td>
      <td>17.000000</td>
      <td>6500.000000</td>
      <td>1901.134317</td>
      <td>825.485459</td>
      <td>0.142857</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>19043.138560</td>
      <td>1.000000</td>
      <td>49039.570000</td>
      <td>40761.250000</td>
      <td>22500.000000</td>
      <td>47137.211760</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.500000</td>
      <td>123.000000</td>
      <td>358.000000</td>
      <td>30000.000000</td>
      <td>50721.483360</td>
      <td>76406.207520</td>
      <td>1.000000</td>
      <td>12.000000</td>
    </tr>
  </tbody>
</table>
</div>



**Some Statistics**

*   We see that the purchases range from 0 dollars to 49000 dollars with mean of 1003 dollars
*   The credit limit ranges from as 50 dollars to a max of 30000 dollars,with a mean of 4494 dollars


*   The cash advance is the cash loan taken from your credit card account using an ATM, bank withdrawal or check from your card issuer. It has a mean of 978$ and max of 47137 dollars
*   the installment purchase amount ranges from 0 dollars to a max of 22500 dollars with a mean of about 411 dollars
*  the installment purchase frequency ranges from 0% to as high as 100% with a mean of about 49%. This implies that on an average users buy 50% of the products on installments and there are users that buy the items on installments 100% of the time
*   The balance ranges from 0 dollars to 19000 dollars with a mean of 1564 dollars.  Balance is the amount of money owed to the credit card company. Users owe 0 dollars to 19000 dollars to the credit card company with the average amount owed being 1564 dollars





```python
df.isnull().sum()
```




    CUST_ID                               0
    BALANCE                               0
    BALANCE_FREQUENCY                     0
    PURCHASES                             0
    ONEOFF_PURCHASES                      0
    INSTALLMENTS_PURCHASES                0
    CASH_ADVANCE                          0
    PURCHASES_FREQUENCY                   0
    ONEOFF_PURCHASES_FREQUENCY            0
    PURCHASES_INSTALLMENTS_FREQUENCY      0
    CASH_ADVANCE_FREQUENCY                0
    CASH_ADVANCE_TRX                      0
    PURCHASES_TRX                         0
    CREDIT_LIMIT                          1
    PAYMENTS                              0
    MINIMUM_PAYMENTS                    313
    PRC_FULL_PAYMENT                      0
    TENURE                                0
    dtype: int64



We see that the credit limit has 1 missing value and the minimum payments has about 313 missing values. Let us fill the missing data with the mean of the respective colums so that the distribution of the data does not change



```python
df['CREDIT_LIMIT'].fillna(df['CREDIT_LIMIT'].mean(),inplace= True)
df['MINIMUM_PAYMENTS'].fillna(df['MINIMUM_PAYMENTS'].mean(),inplace= True)
```


```python
df.isnull().sum()
```




    CUST_ID                             0
    BALANCE                             0
    BALANCE_FREQUENCY                   0
    PURCHASES                           0
    ONEOFF_PURCHASES                    0
    INSTALLMENTS_PURCHASES              0
    CASH_ADVANCE                        0
    PURCHASES_FREQUENCY                 0
    ONEOFF_PURCHASES_FREQUENCY          0
    PURCHASES_INSTALLMENTS_FREQUENCY    0
    CASH_ADVANCE_FREQUENCY              0
    CASH_ADVANCE_TRX                    0
    PURCHASES_TRX                       0
    CREDIT_LIMIT                        0
    PAYMENTS                            0
    MINIMUM_PAYMENTS                    0
    PRC_FULL_PAYMENT                    0
    TENURE                              0
    dtype: int64



**Now that there are no missing values, let us explore the data a bit**

**Let us try to select three samples out of the data set and try to analyse how they belong to different segments**


```python

# TODO: Select three indices of your choice you wish to sample from the dataset
indices = [5,75,342]

# Create a DataFrame of the chosen samples
samples = pd.DataFrame(df.loc[indices], columns = df.keys()).reset_index(drop = True)
print("Chosen samples of credit card customers dataset:")
display(samples)
```

    Chosen samples of credit card customers dataset:
    


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
      <th>CUST_ID</th>
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>C10006</td>
      <td>1809.828751</td>
      <td>1.0</td>
      <td>1333.28</td>
      <td>0.00</td>
      <td>1333.28</td>
      <td>0.000000</td>
      <td>0.666667</td>
      <td>0.000000</td>
      <td>0.583333</td>
      <td>0.000000</td>
      <td>0</td>
      <td>8</td>
      <td>1800.0</td>
      <td>1400.057770</td>
      <td>2407.246035</td>
      <td>0.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>C10079</td>
      <td>5860.433624</td>
      <td>1.0</td>
      <td>561.87</td>
      <td>249.50</td>
      <td>312.37</td>
      <td>0.000000</td>
      <td>0.833333</td>
      <td>0.166667</td>
      <td>0.750000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>14</td>
      <td>6000.0</td>
      <td>1990.044998</td>
      <td>2161.428274</td>
      <td>0.0</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>C10353</td>
      <td>1254.669100</td>
      <td>1.0</td>
      <td>361.73</td>
      <td>361.73</td>
      <td>0.00</td>
      <td>198.686744</td>
      <td>0.166667</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>1</td>
      <td>2</td>
      <td>1500.0</td>
      <td>535.606816</td>
      <td>432.688080</td>
      <td>0.0</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>


The mean values of the predictors are as follows




# **Heat map of the variables **
## let us see if there are any predictors with high correlation




```python
# Create a correlation matrix. What features correlate the most eachpther? 
corr = df.corr()
fig, ax = plt.subplots(figsize=(30,15))    
sns.heatmap(corr, 
            xticklabels=corr.columns.values,
            yticklabels=corr.columns.values,
            linewidths=.2, 
            ax=ax,
            annot=True, 
            annot_kws={"size": 7})
plt.title('Heatmap of Correlation Matrix')
corr
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BALANCE</th>
      <td>1.000000</td>
      <td>0.322412</td>
      <td>0.181261</td>
      <td>0.164350</td>
      <td>0.126469</td>
      <td>0.496692</td>
      <td>-0.077944</td>
      <td>0.073166</td>
      <td>-0.063186</td>
      <td>0.449218</td>
      <td>0.385152</td>
      <td>0.154338</td>
      <td>0.531267</td>
      <td>0.322802</td>
      <td>0.394282</td>
      <td>-0.318959</td>
      <td>0.072692</td>
    </tr>
    <tr>
      <th>BALANCE_FREQUENCY</th>
      <td>0.322412</td>
      <td>1.000000</td>
      <td>0.133674</td>
      <td>0.104323</td>
      <td>0.124292</td>
      <td>0.099388</td>
      <td>0.229715</td>
      <td>0.202415</td>
      <td>0.176079</td>
      <td>0.191873</td>
      <td>0.141555</td>
      <td>0.189626</td>
      <td>0.095795</td>
      <td>0.065008</td>
      <td>0.114249</td>
      <td>-0.095082</td>
      <td>0.119776</td>
    </tr>
    <tr>
      <th>PURCHASES</th>
      <td>0.181261</td>
      <td>0.133674</td>
      <td>1.000000</td>
      <td>0.916845</td>
      <td>0.679896</td>
      <td>-0.051474</td>
      <td>0.393017</td>
      <td>0.498430</td>
      <td>0.315567</td>
      <td>-0.120143</td>
      <td>-0.067175</td>
      <td>0.689561</td>
      <td>0.356959</td>
      <td>0.603264</td>
      <td>0.093515</td>
      <td>0.180379</td>
      <td>0.086288</td>
    </tr>
    <tr>
      <th>ONEOFF_PURCHASES</th>
      <td>0.164350</td>
      <td>0.104323</td>
      <td>0.916845</td>
      <td>1.000000</td>
      <td>0.330622</td>
      <td>-0.031326</td>
      <td>0.264937</td>
      <td>0.524891</td>
      <td>0.127729</td>
      <td>-0.082628</td>
      <td>-0.046212</td>
      <td>0.545523</td>
      <td>0.319721</td>
      <td>0.567292</td>
      <td>0.048597</td>
      <td>0.132763</td>
      <td>0.064150</td>
    </tr>
    <tr>
      <th>INSTALLMENTS_PURCHASES</th>
      <td>0.126469</td>
      <td>0.124292</td>
      <td>0.679896</td>
      <td>0.330622</td>
      <td>1.000000</td>
      <td>-0.064244</td>
      <td>0.442418</td>
      <td>0.214042</td>
      <td>0.511351</td>
      <td>-0.132318</td>
      <td>-0.073999</td>
      <td>0.628108</td>
      <td>0.256496</td>
      <td>0.384084</td>
      <td>0.131687</td>
      <td>0.182569</td>
      <td>0.086143</td>
    </tr>
    <tr>
      <th>CASH_ADVANCE</th>
      <td>0.496692</td>
      <td>0.099388</td>
      <td>-0.051474</td>
      <td>-0.031326</td>
      <td>-0.064244</td>
      <td>1.000000</td>
      <td>-0.215507</td>
      <td>-0.086754</td>
      <td>-0.177070</td>
      <td>0.628522</td>
      <td>0.656498</td>
      <td>-0.075850</td>
      <td>0.303983</td>
      <td>0.453238</td>
      <td>0.139223</td>
      <td>-0.152935</td>
      <td>-0.068312</td>
    </tr>
    <tr>
      <th>PURCHASES_FREQUENCY</th>
      <td>-0.077944</td>
      <td>0.229715</td>
      <td>0.393017</td>
      <td>0.264937</td>
      <td>0.442418</td>
      <td>-0.215507</td>
      <td>1.000000</td>
      <td>0.501343</td>
      <td>0.862934</td>
      <td>-0.308478</td>
      <td>-0.203478</td>
      <td>0.568430</td>
      <td>0.119778</td>
      <td>0.103464</td>
      <td>0.002976</td>
      <td>0.305802</td>
      <td>0.061506</td>
    </tr>
    <tr>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <td>0.073166</td>
      <td>0.202415</td>
      <td>0.498430</td>
      <td>0.524891</td>
      <td>0.214042</td>
      <td>-0.086754</td>
      <td>0.501343</td>
      <td>1.000000</td>
      <td>0.142329</td>
      <td>-0.111716</td>
      <td>-0.069088</td>
      <td>0.544869</td>
      <td>0.295030</td>
      <td>0.243537</td>
      <td>-0.029963</td>
      <td>0.157531</td>
      <td>0.082466</td>
    </tr>
    <tr>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <td>-0.063186</td>
      <td>0.176079</td>
      <td>0.315567</td>
      <td>0.127729</td>
      <td>0.511351</td>
      <td>-0.177070</td>
      <td>0.862934</td>
      <td>0.142329</td>
      <td>1.000000</td>
      <td>-0.262958</td>
      <td>-0.169207</td>
      <td>0.529975</td>
      <td>0.060752</td>
      <td>0.085551</td>
      <td>0.029590</td>
      <td>0.250087</td>
      <td>0.073275</td>
    </tr>
    <tr>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <td>0.449218</td>
      <td>0.191873</td>
      <td>-0.120143</td>
      <td>-0.082628</td>
      <td>-0.132318</td>
      <td>0.628522</td>
      <td>-0.308478</td>
      <td>-0.111716</td>
      <td>-0.262958</td>
      <td>1.000000</td>
      <td>0.799561</td>
      <td>-0.131168</td>
      <td>0.132616</td>
      <td>0.183192</td>
      <td>0.097898</td>
      <td>-0.249773</td>
      <td>-0.133372</td>
    </tr>
    <tr>
      <th>CASH_ADVANCE_TRX</th>
      <td>0.385152</td>
      <td>0.141555</td>
      <td>-0.067175</td>
      <td>-0.046212</td>
      <td>-0.073999</td>
      <td>0.656498</td>
      <td>-0.203478</td>
      <td>-0.069088</td>
      <td>-0.169207</td>
      <td>0.799561</td>
      <td>1.000000</td>
      <td>-0.066157</td>
      <td>0.149699</td>
      <td>0.255278</td>
      <td>0.109185</td>
      <td>-0.169784</td>
      <td>-0.043421</td>
    </tr>
    <tr>
      <th>PURCHASES_TRX</th>
      <td>0.154338</td>
      <td>0.189626</td>
      <td>0.689561</td>
      <td>0.545523</td>
      <td>0.628108</td>
      <td>-0.075850</td>
      <td>0.568430</td>
      <td>0.544869</td>
      <td>0.529975</td>
      <td>-0.131168</td>
      <td>-0.066157</td>
      <td>1.000000</td>
      <td>0.272877</td>
      <td>0.370832</td>
      <td>0.095858</td>
      <td>0.162066</td>
      <td>0.121874</td>
    </tr>
    <tr>
      <th>CREDIT_LIMIT</th>
      <td>0.531267</td>
      <td>0.095795</td>
      <td>0.356959</td>
      <td>0.319721</td>
      <td>0.256496</td>
      <td>0.303983</td>
      <td>0.119778</td>
      <td>0.295030</td>
      <td>0.060752</td>
      <td>0.132616</td>
      <td>0.149699</td>
      <td>0.272877</td>
      <td>1.000000</td>
      <td>0.421852</td>
      <td>0.125134</td>
      <td>0.055671</td>
      <td>0.139034</td>
    </tr>
    <tr>
      <th>PAYMENTS</th>
      <td>0.322802</td>
      <td>0.065008</td>
      <td>0.603264</td>
      <td>0.567292</td>
      <td>0.384084</td>
      <td>0.453238</td>
      <td>0.103464</td>
      <td>0.243537</td>
      <td>0.085551</td>
      <td>0.183192</td>
      <td>0.255278</td>
      <td>0.370832</td>
      <td>0.421852</td>
      <td>1.000000</td>
      <td>0.125046</td>
      <td>0.112138</td>
      <td>0.106136</td>
    </tr>
    <tr>
      <th>MINIMUM_PAYMENTS</th>
      <td>0.394282</td>
      <td>0.114249</td>
      <td>0.093515</td>
      <td>0.048597</td>
      <td>0.131687</td>
      <td>0.139223</td>
      <td>0.002976</td>
      <td>-0.029963</td>
      <td>0.029590</td>
      <td>0.097898</td>
      <td>0.109185</td>
      <td>0.095858</td>
      <td>0.125134</td>
      <td>0.125046</td>
      <td>1.000000</td>
      <td>-0.139674</td>
      <td>0.057257</td>
    </tr>
    <tr>
      <th>PRC_FULL_PAYMENT</th>
      <td>-0.318959</td>
      <td>-0.095082</td>
      <td>0.180379</td>
      <td>0.132763</td>
      <td>0.182569</td>
      <td>-0.152935</td>
      <td>0.305802</td>
      <td>0.157531</td>
      <td>0.250087</td>
      <td>-0.249773</td>
      <td>-0.169784</td>
      <td>0.162066</td>
      <td>0.055671</td>
      <td>0.112138</td>
      <td>-0.139674</td>
      <td>1.000000</td>
      <td>-0.016486</td>
    </tr>
    <tr>
      <th>TENURE</th>
      <td>0.072692</td>
      <td>0.119776</td>
      <td>0.086288</td>
      <td>0.064150</td>
      <td>0.086143</td>
      <td>-0.068312</td>
      <td>0.061506</td>
      <td>0.082466</td>
      <td>0.073275</td>
      <td>-0.133372</td>
      <td>-0.043421</td>
      <td>0.121874</td>
      <td>0.139034</td>
      <td>0.106136</td>
      <td>0.057257</td>
      <td>-0.016486</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




![png](output_24_1.png)


We see that many variables have high correlation, let us try to get the pairs with high correlation from the below code


```python
def get_pairs(df):
    '''Grabs the combinations of pairs of column names '''
    pairs = set()
    cols = df.columns
    for i in range(0, df.shape[1]):
        for j in range(0, i+1):
            pairs.add((cols[i], cols[j]))
    return pairs

def top_abs_corrs(df, n=.5):
    '''Returns the variables with absolute value of correlation >= n'''
    corrs = df.corr().abs().unstack()
    pairs = get_pairs(df)
    top_corrs = corrs.drop(labels=pairs).sort_values(ascending=False)
    top_corrs = top_corrs.to_dict()
    d= {k: v for k, v in top_corrs.items() if  v >= n}
#     return top_corrs[0:n]
    return d

# return pairs from the correlation matrix with correlation >= .85
top_corrs = top_abs_corrs(corr,.85)
top_corrs
```




    {('CASH_ADVANCE', 'CASH_ADVANCE_FREQUENCY'): 0.9118370648288009,
     ('CASH_ADVANCE', 'CASH_ADVANCE_TRX'): 0.9170453786323367,
     ('CASH_ADVANCE_FREQUENCY', 'CASH_ADVANCE_TRX'): 0.9769561655289744,
     ('INSTALLMENTS_PURCHASES', 'PURCHASES_TRX'): 0.8603490822035166,
     ('PURCHASES', 'ONEOFF_PURCHASES'): 0.9535932980644026,
     ('PURCHASES', 'PURCHASES_TRX'): 0.8643451146665079,
     ('PURCHASES_FREQUENCY',
      'PURCHASES_INSTALLMENTS_FREQUENCY'): 0.9533728151834796}



We see the following


*   we see that Cash_Advance has high correlation of about 91% with cash_advance_frequency, cash_advance_trx...so it is safe to drop these two columns 
*   purchases has high correlation of 95% with oneoff_purchases, so it is good to drop oneoff_purchases

*   Purchase_frequence has high correlation of 95% with purchases_installments_frequency, so we are good to drop purchases_installments_frequency



*  PURCHASES_TRX has about 86% correlation with Purchasesm so lets go ahead and drop that as well







# **Outlier Detection using Isolation Forest**

**Return the anomaly score of each sample using the IsolationForest algorithm**

**The IsolationForest ‘isolates’ observations by randomly selecting a feature and then randomly selecting a split value between the maximum and minimum values of the selected feature.**

**Since recursive partitioning can be represented by a tree structure, the number of splittings required to isolate a sample is equivalent to the path length from the root node to the terminating node.**

**This path length, averaged over a forest of such random trees, is a measure of normality and our decision function.**

**Random partitioning produces noticeably shorter paths for anomalies. Hence, when a forest of random trees collectively produce shorter path lengths for particular samples, they are highly likely to be anomalies.**

**It gives a score of -1 for anomalies**


```python
df_temp = df.drop('CUST_ID',axis=1)

#Let us see the how the data of each variable looks like using describe()
df_temp.describe()
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
      <td>8950.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1564.474828</td>
      <td>0.877271</td>
      <td>1003.204834</td>
      <td>592.437371</td>
      <td>411.067645</td>
      <td>978.871112</td>
      <td>0.490351</td>
      <td>0.202458</td>
      <td>0.364437</td>
      <td>0.135144</td>
      <td>3.248827</td>
      <td>14.709832</td>
      <td>4494.449450</td>
      <td>1733.143852</td>
      <td>864.206542</td>
      <td>0.153715</td>
      <td>11.517318</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2081.531879</td>
      <td>0.236904</td>
      <td>2136.634782</td>
      <td>1659.887917</td>
      <td>904.338115</td>
      <td>2097.163877</td>
      <td>0.401371</td>
      <td>0.298336</td>
      <td>0.397448</td>
      <td>0.200121</td>
      <td>6.824647</td>
      <td>24.857649</td>
      <td>3638.612411</td>
      <td>2895.063757</td>
      <td>2330.588021</td>
      <td>0.292499</td>
      <td>1.338331</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>50.000000</td>
      <td>0.000000</td>
      <td>0.019163</td>
      <td>0.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>128.281915</td>
      <td>0.888889</td>
      <td>39.635000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1600.000000</td>
      <td>383.276166</td>
      <td>170.857654</td>
      <td>0.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>873.385231</td>
      <td>1.000000</td>
      <td>361.280000</td>
      <td>38.000000</td>
      <td>89.000000</td>
      <td>0.000000</td>
      <td>0.500000</td>
      <td>0.083333</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>7.000000</td>
      <td>3000.000000</td>
      <td>856.901546</td>
      <td>335.628312</td>
      <td>0.000000</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2054.140036</td>
      <td>1.000000</td>
      <td>1110.130000</td>
      <td>577.405000</td>
      <td>468.637500</td>
      <td>1113.821139</td>
      <td>0.916667</td>
      <td>0.300000</td>
      <td>0.750000</td>
      <td>0.222222</td>
      <td>4.000000</td>
      <td>17.000000</td>
      <td>6500.000000</td>
      <td>1901.134317</td>
      <td>864.206542</td>
      <td>0.142857</td>
      <td>12.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>19043.138560</td>
      <td>1.000000</td>
      <td>49039.570000</td>
      <td>40761.250000</td>
      <td>22500.000000</td>
      <td>47137.211760</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.500000</td>
      <td>123.000000</td>
      <td>358.000000</td>
      <td>30000.000000</td>
      <td>50721.483360</td>
      <td>76406.207520</td>
      <td>1.000000</td>
      <td>12.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.ensemble import IsolationForest


# clf = IsolationForest(n_jobs=6,n_estimators=500, max_samples=256, random_state=23)
# fit the model
clf = IsolationForest(max_samples=100)
clf.fit(df_temp)
y_pred_train = clf.predict(df_temp)

```

    /usr/local/lib/python3.6/dist-packages/sklearn/ensemble/iforest.py:213: FutureWarning: default contamination parameter 0.1 will change in version 0.22 to "auto". This will change the predict method behavior.
      FutureWarning)
    /usr/local/lib/python3.6/dist-packages/sklearn/ensemble/iforest.py:223: FutureWarning: behaviour="old" is deprecated and will be removed in version 0.22. Please use behaviour="new", which makes the decision_function change to match other anomaly detection algorithm API.
      FutureWarning)
    /usr/local/lib/python3.6/dist-packages/sklearn/ensemble/iforest.py:417: DeprecationWarning: threshold_ attribute is deprecated in 0.20 and will be removed in 0.22.
      " be removed in 0.22.", DeprecationWarning)
    


```python
df_temp['not outlier'] = y_pred_train
df_temp.head()
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
      <th>not outlier</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>40.900749</td>
      <td>0.818182</td>
      <td>95.40</td>
      <td>0.00</td>
      <td>95.4</td>
      <td>0.000000</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0</td>
      <td>2</td>
      <td>1000.0</td>
      <td>201.802084</td>
      <td>139.509787</td>
      <td>0.000000</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3202.467416</td>
      <td>0.909091</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>6442.945483</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.250000</td>
      <td>4</td>
      <td>0</td>
      <td>7000.0</td>
      <td>4103.032597</td>
      <td>1072.340217</td>
      <td>0.222222</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2495.148862</td>
      <td>1.000000</td>
      <td>773.17</td>
      <td>773.17</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>12</td>
      <td>7500.0</td>
      <td>622.066742</td>
      <td>627.284787</td>
      <td>0.000000</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1666.670542</td>
      <td>0.636364</td>
      <td>1499.00</td>
      <td>1499.00</td>
      <td>0.0</td>
      <td>205.788017</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>1</td>
      <td>1</td>
      <td>7500.0</td>
      <td>0.000000</td>
      <td>864.206542</td>
      <td>0.000000</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>817.714335</td>
      <td>1.000000</td>
      <td>16.00</td>
      <td>16.00</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>1</td>
      <td>1200.0</td>
      <td>678.334763</td>
      <td>244.791237</td>
      <td>0.000000</td>
      <td>12</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_clean = df_temp.drop(df_temp[df_temp['not outlier']==-1].index)
df_clean.drop('not outlier',axis=1, inplace= True)
```


```python
df_clean.head()
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>40.900749</td>
      <td>0.818182</td>
      <td>95.40</td>
      <td>0.00</td>
      <td>95.4</td>
      <td>0.000000</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0</td>
      <td>2</td>
      <td>1000.0</td>
      <td>201.802084</td>
      <td>139.509787</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3202.467416</td>
      <td>0.909091</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>6442.945483</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.250000</td>
      <td>4</td>
      <td>0</td>
      <td>7000.0</td>
      <td>4103.032597</td>
      <td>1072.340217</td>
      <td>0.222222</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2495.148862</td>
      <td>1.000000</td>
      <td>773.17</td>
      <td>773.17</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>12</td>
      <td>7500.0</td>
      <td>622.066742</td>
      <td>627.284787</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1666.670542</td>
      <td>0.636364</td>
      <td>1499.00</td>
      <td>1499.00</td>
      <td>0.0</td>
      <td>205.788017</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>1</td>
      <td>1</td>
      <td>7500.0</td>
      <td>0.000000</td>
      <td>864.206542</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>817.714335</td>
      <td>1.000000</td>
      <td>16.00</td>
      <td>16.00</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>1</td>
      <td>1200.0</td>
      <td>678.334763</td>
      <td>244.791237</td>
      <td>0.000000</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#df_clean has no outliers and its length is 8055 with 895 entries being removed from the original data set
len(df_clean)

```




    8055



# **Visualising the Data Distribution**


```python
#Univariate Analysis
df_clean.plot(kind='density', subplots=True, layout=(5,4), sharex=False)
plt.show()

```


![png](output_36_0.png)


**We see that most of the data are skewed**

# **Feature Transformation**

**In this section you will use principal component analysis (PCA) to draw conclusions about the underlying structure of the wholesale customer data. Since using PCA on a dataset calculates the dimensions which best maximize variance, we will find which compound combinations of features best describe customers.**

## Pre-Req: Standardize the Dataset
### First, lets rescale our feature vectors


```python
from sklearn.preprocessing import StandardScaler
scaled_df = StandardScaler().fit_transform(df_clean)
df_processed = pd.DataFrame(scaled_df,columns = df_clean.columns)
```

    /usr/local/lib/python3.6/dist-packages/sklearn/preprocessing/data.py:645: DataConversionWarning: Data with input dtype int64, float64 were all converted to float64 by StandardScaler.
      return self.partial_fit(X, y)
    /usr/local/lib/python3.6/dist-packages/sklearn/base.py:464: DataConversionWarning: Data with input dtype int64, float64 were all converted to float64 by StandardScaler.
      return self.fit(X, **fit_params).transform(X)
    

## Choosing the Right Number of Dimensions

### The goal is to choose the right number of dimensions that captures the most variance. 


```python
#Fitting the PCA algorithm with our Data
from sklearn.decomposition import PCA
pca = PCA().fit(df_processed)

#Plotting the Cumulative Summation of the Explained Variance
plt.figure()
plt.plot(np.cumsum(pca.explained_variance_ratio_))
plt.xlabel('Number of Components')
plt.ylabel('Variance (%)') #for each component
plt.title('Credit card Dataset Explained Variance')
plt.show()
```


![png](output_43_0.png)


we see that at components=7 we can explain about 85% of the variance.Let us chose the number of components as 7


```python
# TODO: Apply PCA by fitting the good data with the same number of dimensions as features
pca = PCA(n_components=8)
pcomponents = pca.fit_transform(scaled_df)
df_pca = pd.DataFrame(data = pcomponents, columns = ['PC1', 'PC2','PC3', 'PC4','PC5', 'PC6','PC7','PC8'])

```


```python
df_pca.head()
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
      <th>PC1</th>
      <th>PC2</th>
      <th>PC3</th>
      <th>PC4</th>
      <th>PC5</th>
      <th>PC6</th>
      <th>PC7</th>
      <th>PC8</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.903492</td>
      <td>-1.945454</td>
      <td>0.372983</td>
      <td>0.665525</td>
      <td>0.095946</td>
      <td>-0.579439</td>
      <td>0.505254</td>
      <td>-0.180630</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3.062577</td>
      <td>2.545186</td>
      <td>-0.105984</td>
      <td>-1.677381</td>
      <td>1.518020</td>
      <td>0.090528</td>
      <td>-0.248566</td>
      <td>0.022647</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.399894</td>
      <td>1.110397</td>
      <td>2.121895</td>
      <td>1.477419</td>
      <td>-0.326238</td>
      <td>-0.118130</td>
      <td>-1.594226</td>
      <td>0.008607</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.240699</td>
      <td>0.202767</td>
      <td>2.235551</td>
      <td>0.490837</td>
      <td>0.543420</td>
      <td>0.350769</td>
      <td>0.094360</td>
      <td>-0.623622</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.119585</td>
      <td>-1.404661</td>
      <td>0.545559</td>
      <td>1.037591</td>
      <td>0.062857</td>
      <td>-0.684356</td>
      <td>0.161928</td>
      <td>-0.006236</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Let us see how much of the total variance is explained by these 7 compoents
sum(pca.explained_variance_ratio_)
```




    0.8465543992318026



**The variance explained is close to 85% from 7 components from the initial 18 variables we had**

## Interpreting Principle Components


```python
pd.DataFrame(pca.components_, columns=list(df_clean.columns), index=('PC1', 'PC2','PC3', 'PC4','PC5', 'PC6','PC7','PC8'))
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>PC1</th>
      <td>0.153874</td>
      <td>-0.051649</td>
      <td>-0.364726</td>
      <td>-0.248159</td>
      <td>-0.313113</td>
      <td>0.244348</td>
      <td>-0.383408</td>
      <td>-0.248250</td>
      <td>-0.327234</td>
      <td>0.277209</td>
      <td>0.247980</td>
      <td>-0.356268</td>
      <td>-0.033817</td>
      <td>-0.026533</td>
      <td>0.053078</td>
      <td>-0.176973</td>
      <td>-0.065876</td>
    </tr>
    <tr>
      <th>PC2</th>
      <td>0.413577</td>
      <td>0.268823</td>
      <td>0.236209</td>
      <td>0.245333</td>
      <td>0.091570</td>
      <td>0.341756</td>
      <td>0.036565</td>
      <td>0.209617</td>
      <td>-0.014449</td>
      <td>0.308664</td>
      <td>0.309308</td>
      <td>0.172436</td>
      <td>0.311660</td>
      <td>0.319766</td>
      <td>0.147768</td>
      <td>-0.122460</td>
      <td>0.114653</td>
    </tr>
    <tr>
      <th>PC3</th>
      <td>-0.091192</td>
      <td>-0.220348</td>
      <td>0.143905</td>
      <td>0.462845</td>
      <td>-0.355488</td>
      <td>-0.110478</td>
      <td>-0.243455</td>
      <td>0.400475</td>
      <td>-0.470929</td>
      <td>-0.162815</td>
      <td>-0.175573</td>
      <td>-0.110250</td>
      <td>0.147939</td>
      <td>0.089403</td>
      <td>-0.158155</td>
      <td>-0.034890</td>
      <td>0.050949</td>
    </tr>
    <tr>
      <th>PC4</th>
      <td>0.251626</td>
      <td>0.382869</td>
      <td>-0.048331</td>
      <td>0.043531</td>
      <td>-0.141721</td>
      <td>-0.272241</td>
      <td>0.006897</td>
      <td>0.091280</td>
      <td>-0.042371</td>
      <td>-0.150015</td>
      <td>-0.189889</td>
      <td>0.028502</td>
      <td>-0.139919</td>
      <td>-0.384253</td>
      <td>0.431593</td>
      <td>-0.470075</td>
      <td>0.218276</td>
    </tr>
    <tr>
      <th>PC5</th>
      <td>0.160949</td>
      <td>-0.238541</td>
      <td>-0.080585</td>
      <td>-0.188407</td>
      <td>0.106098</td>
      <td>0.008244</td>
      <td>-0.104886</td>
      <td>-0.250102</td>
      <td>0.010570</td>
      <td>-0.319121</td>
      <td>-0.289164</td>
      <td>-0.106373</td>
      <td>0.431542</td>
      <td>0.300881</td>
      <td>0.289886</td>
      <td>0.116217</td>
      <td>0.468131</td>
    </tr>
    <tr>
      <th>PC6</th>
      <td>0.127266</td>
      <td>-0.267633</td>
      <td>0.079084</td>
      <td>0.079426</td>
      <td>0.034240</td>
      <td>0.057839</td>
      <td>0.011576</td>
      <td>-0.001989</td>
      <td>-0.000221</td>
      <td>-0.088628</td>
      <td>-0.141636</td>
      <td>-0.009159</td>
      <td>0.070876</td>
      <td>0.036608</td>
      <td>0.565572</td>
      <td>0.017187</td>
      <td>-0.735137</td>
    </tr>
    <tr>
      <th>PC7</th>
      <td>-0.220014</td>
      <td>-0.332992</td>
      <td>0.215761</td>
      <td>0.137729</td>
      <td>0.197277</td>
      <td>-0.003728</td>
      <td>-0.146206</td>
      <td>-0.149966</td>
      <td>-0.022822</td>
      <td>0.068766</td>
      <td>0.124361</td>
      <td>0.082405</td>
      <td>-0.557246</td>
      <td>0.350193</td>
      <td>0.224918</td>
      <td>-0.362356</td>
      <td>0.223241</td>
    </tr>
    <tr>
      <th>PC8</th>
      <td>-0.169544</td>
      <td>0.166352</td>
      <td>-0.065560</td>
      <td>0.047732</td>
      <td>-0.177762</td>
      <td>-0.049859</td>
      <td>0.027279</td>
      <td>0.172354</td>
      <td>-0.100603</td>
      <td>0.105316</td>
      <td>0.193100</td>
      <td>-0.062565</td>
      <td>-0.252765</td>
      <td>0.020527</td>
      <td>0.491208</td>
      <td>0.676218</td>
      <td>0.217230</td>
    </tr>
  </tbody>
</table>
</div>





*   **The first component gives most weightage to the purchases made and least weightage to the balance. And some good weightage to Installment Purchases,One off purchases . This component keeps track of all the different types of purchases**
*   **The second component gives highest weightage to the balance followed by minimum payments, cash_advance, and PRC_full payment. So this component is dealing with plus and minus of the amount.cash flow that is happening in the customers credit card**

**So The Principal component can be used to express latent features in the data set**



# **Clustering**

# **K Means Clustering**


```python
#Now that we have standardised and applied Principal Components, We shall cluster the data using Kmeans Clustering
import pylab as pl
from sklearn.cluster import KMeans
```

# **How many Clusters?**

### Let us use elbow method to decide upon the number of clusters


```python
# Create K Clusters of 15
k = range(1,15)

# Instantiate and Fit KMeans of Clusters 1-15
kmeans = [KMeans(n_clusters=i) for i in k]
score = [kmeans[i].fit(df_pca).score(df_pca) for i in range(len(kmeans))]

# Plot the Elbow Method
pl.plot(k,score)
pl.xlabel('Number of Clusters')
pl.ylabel('Score')
pl.title('Elbow Curve')
pl.show()
```


![png](output_56_0.png)


**It is not so clear from the elbow curve, let us check the average Silhouette Scores**

## Silhouette Score

### The main goal of clustering is to minimise the intra cluster distance or make the points inside a cluster as dense as possible and intercluster distance or the distance between any two clusters as maximum as possible

### Silhouette analysis can be used to study the separation distance between the resulting clusters. The silhouette plot displays a measure of how close each point in one cluster is to points in the neighboring clusters and thus provides a way to assess parameters like number of clusters visually. This measure has a range of [-1, 1].

### Silhouette coefficients (as these values are referred to as) near +1 indicate that the sample is far away from the neighboring clusters. A value of 0 indicates that the sample is on or very close to the decision boundary between two neighboring clusters and negative values indicate that those samples might have been assigned to the wrong cluster.


```python
from __future__ import print_function

from sklearn.datasets import make_blobs
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_samples, silhouette_score

import matplotlib.pyplot as plt
import matplotlib.cm as cm
import numpy as np

print(__doc__)

# Generating the sample data from make_blobs
# This particular setting has one distinct cluster and 3 clusters placed close
# together.


range_n_clusters = [2, 3, 4, 5, 6,7]

for n_clusters in range_n_clusters:
    # Create a subplot with 1 row and 2 columns
    fig, ax1 = plt.subplots(1, 1)
    fig.set_size_inches(18, 7)

    # The 1st subplot is the silhouette plot
    # The silhouette coefficient can range from -1, 1 but in this example all
    # lie within [-0.1, 1]
    ax1.set_xlim([-0.1, 1])
    # The (n_clusters+1)*10 is for inserting blank space between silhouette
    # plots of individual clusters, to demarcate them clearly.
    ax1.set_ylim([0, len(df_clean) + (n_clusters + 1) * 10])

    # Initialize the clusterer with n_clusters value and a random generator
    # seed of 10 for reproducibility.
    clusterer = KMeans(n_clusters=n_clusters, random_state=10)
    cluster_labels = clusterer.fit_predict(df_clean)

    # The silhouette_score gives the average value for all the samples.
    # This gives a perspective into the density and separation of the formed
    # clusters
    silhouette_avg = silhouette_score(df_clean, cluster_labels)
    print("For n_clusters =", n_clusters,
          "The average silhouette_score is :", silhouette_avg)

    # Compute the silhouette scores for each sample
    sample_silhouette_values = silhouette_samples(df_clean, cluster_labels)

    y_lower = 10
    for i in range(n_clusters):
        # Aggregate the silhouette scores for samples belonging to
        # cluster i, and sort them
        ith_cluster_silhouette_values = \
            sample_silhouette_values[cluster_labels == i]

        ith_cluster_silhouette_values.sort()

        size_cluster_i = ith_cluster_silhouette_values.shape[0]
        y_upper = y_lower + size_cluster_i

        color = cm.nipy_spectral(float(i) / n_clusters)
        ax1.fill_betweenx(np.arange(y_lower, y_upper),
                          0, ith_cluster_silhouette_values,
                          facecolor=color, edgecolor=color, alpha=0.7)

        # Label the silhouette plots with their cluster numbers at the middle
        ax1.text(-0.05, y_lower + 0.5 * size_cluster_i, str(i))

        # Compute the new y_lower for next plot
        y_lower = y_upper + 10  # 10 for the 0 samples

    ax1.set_title("The silhouette plot for the various clusters.")
    ax1.set_xlabel("The silhouette coefficient values")
    ax1.set_ylabel("Cluster label")

    # The vertical line for average silhouette score of all the values
    ax1.axvline(x=silhouette_avg, color="red", linestyle="--")

    ax1.set_yticks([])  # Clear the yaxis labels / ticks
    ax1.set_xticks([-0.1, 0, 0.2, 0.4, 0.6, 0.8, 1])


plt.show()
```

    Automatically created module for IPython interactive environment
    For n_clusters = 2 The average silhouette_score is : 0.4552974848861243
    For n_clusters = 3 The average silhouette_score is : 0.4360205646798433
    For n_clusters = 4 The average silhouette_score is : 0.4462519515674172
    For n_clusters = 5 The average silhouette_score is : 0.39575367914797144
    For n_clusters = 6 The average silhouette_score is : 0.38810914832006244
    For n_clusters = 7 The average silhouette_score is : 0.33375342067170327
    


![png](output_59_1.png)



![png](output_59_2.png)



![png](output_59_3.png)



![png](output_59_4.png)



![png](output_59_5.png)



![png](output_59_6.png)


**We see that clusters 2 and 4 have the best Silhouette scores of around 0.45, let us chose cluster size as 4 because we will get more segments and we can target them better. In the real world Scenario, the number of clusters depends totally on the domain we are dealing with and the Business Objective of the company**


```python
# Choose Cluster Size of 3
cluster = KMeans(n_clusters = 4) 

df_clean['cluster'] = cluster.fit_predict(df_pca)
```


```python
#Let us see the samples
df_clean.head()
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
      <th>BALANCE</th>
      <th>BALANCE_FREQUENCY</th>
      <th>PURCHASES</th>
      <th>ONEOFF_PURCHASES</th>
      <th>INSTALLMENTS_PURCHASES</th>
      <th>CASH_ADVANCE</th>
      <th>PURCHASES_FREQUENCY</th>
      <th>ONEOFF_PURCHASES_FREQUENCY</th>
      <th>PURCHASES_INSTALLMENTS_FREQUENCY</th>
      <th>CASH_ADVANCE_FREQUENCY</th>
      <th>CASH_ADVANCE_TRX</th>
      <th>PURCHASES_TRX</th>
      <th>CREDIT_LIMIT</th>
      <th>PAYMENTS</th>
      <th>MINIMUM_PAYMENTS</th>
      <th>PRC_FULL_PAYMENT</th>
      <th>TENURE</th>
      <th>cluster</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>40.900749</td>
      <td>0.818182</td>
      <td>95.40</td>
      <td>0.00</td>
      <td>95.4</td>
      <td>0.000000</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0</td>
      <td>2</td>
      <td>1000.0</td>
      <td>201.802084</td>
      <td>139.509787</td>
      <td>0.000000</td>
      <td>12</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3202.467416</td>
      <td>0.909091</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>6442.945483</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.250000</td>
      <td>4</td>
      <td>0</td>
      <td>7000.0</td>
      <td>4103.032597</td>
      <td>1072.340217</td>
      <td>0.222222</td>
      <td>12</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2495.148862</td>
      <td>1.000000</td>
      <td>773.17</td>
      <td>773.17</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>12</td>
      <td>7500.0</td>
      <td>622.066742</td>
      <td>627.284787</td>
      <td>0.000000</td>
      <td>12</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1666.670542</td>
      <td>0.636364</td>
      <td>1499.00</td>
      <td>1499.00</td>
      <td>0.0</td>
      <td>205.788017</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>1</td>
      <td>1</td>
      <td>7500.0</td>
      <td>0.000000</td>
      <td>864.206542</td>
      <td>0.000000</td>
      <td>12</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>817.714335</td>
      <td>1.000000</td>
      <td>16.00</td>
      <td>16.00</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0</td>
      <td>1</td>
      <td>1200.0</td>
      <td>678.334763</td>
      <td>244.791237</td>
      <td>0.000000</td>
      <td>12</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Let us see how many entries are there in each cluster
df_clean['cluster'].value_counts().sort_index()
```




    0    3406
    1    1210
    2    2126
    3    1313
    Name: cluster, dtype: int64



**we see that the cluster 1 has the highest records with 3406 and cluster 1 with 1210 entries**

## Cluster Centroids


```python
# centers = np.array(kmeans_model.cluster_centers_)
pd.DataFrame(data = cluster.cluster_centers_ , columns= ['PC1', 'PC2','PC3', 'PC4','PC5', 'PC6','PC7','PC8'] )
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
      <th>PC1</th>
      <th>PC2</th>
      <th>PC3</th>
      <th>PC4</th>
      <th>PC5</th>
      <th>PC6</th>
      <th>PC7</th>
      <th>PC8</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.020891</td>
      <td>-0.946809</td>
      <td>0.570970</td>
      <td>0.212233</td>
      <td>0.076916</td>
      <td>-0.043158</td>
      <td>0.135124</td>
      <td>-0.092590</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-3.144079</td>
      <td>1.590373</td>
      <td>1.191085</td>
      <td>0.112592</td>
      <td>-0.423983</td>
      <td>0.048169</td>
      <td>-0.039383</td>
      <td>0.120625</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.492746</td>
      <td>-0.769038</td>
      <td>-1.303861</td>
      <td>-0.138100</td>
      <td>0.106170</td>
      <td>0.011953</td>
      <td>-0.143068</td>
      <td>0.002838</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.668142</td>
      <td>2.235551</td>
      <td>-0.466150</td>
      <td>-0.430428</td>
      <td>0.019266</td>
      <td>0.048168</td>
      <td>-0.082359</td>
      <td>0.124352</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_clean[df_clean['cluster']==0].mean()
```




    BALANCE                              864.441743
    BALANCE_FREQUENCY                      0.780236
    PURCHASES                            230.595211
    ONEOFF_PURCHASES                     180.418097
    INSTALLMENTS_PURCHASES                50.321970
    CASH_ADVANCE                         417.336844
    PURCHASES_FREQUENCY                    0.182059
    ONEOFF_PURCHASES_FREQUENCY             0.096404
    PURCHASES_INSTALLMENTS_FREQUENCY       0.083846
    CASH_ADVANCE_FREQUENCY                 0.090498
    CASH_ADVANCE_TRX                       1.558133
    PURCHASES_TRX                          2.982090
    CREDIT_LIMIT                        3092.762121
    PAYMENTS                             767.839433
    MINIMUM_PAYMENTS                     519.322287
    PRC_FULL_PAYMENT                       0.072217
    TENURE                                11.476218
    cluster                                0.000000
    dtype: float64



## Cluster 0 Characteristics
**The cluster 0 people  have the purchase frequency of 18%, their balance is also quite low which is 864 dollars. They spend very less on installment purchases of about 50 dollars. Their purchase is also quite low of about 230 dollars. They dont borrow much cash from the card either, with just 9% frequency. They are probably fairly new customers who have a low balance and cash advance. The credit card provider might encourage them to increase their activity by offering cash backs, promotions, free Uber rides etc**


```python
df_clean[df_clean['cluster']==1].mean()
```




    BALANCE                             1307.714292
    BALANCE_FREQUENCY                      0.969304
    PURCHASES                           2046.647380
    ONEOFF_PURCHASES                    1449.238702
    INSTALLMENTS_PURCHASES               597.449174
    CASH_ADVANCE                         209.247750
    PURCHASES_FREQUENCY                    0.865467
    ONEOFF_PURCHASES_FREQUENCY             0.659424
    PURCHASES_INSTALLMENTS_FREQUENCY       0.510869
    CASH_ADVANCE_FREQUENCY                 0.042692
    CASH_ADVANCE_TRX                       0.776860
    PURCHASES_TRX                         30.733884
    CREDIT_LIMIT                        5805.751315
    PAYMENTS                            1988.937350
    MINIMUM_PAYMENTS                     523.839005
    PRC_FULL_PAYMENT                       0.231732
    TENURE                                11.904959
    cluster                                1.000000
    dtype: float64



## Cluster 1 Characteristics
**The cluster 1 people have a very good credit limit on an average of about 5800 dollars. They have a high purchase frequency of 86.5%. They have fairly high full payment percentage of 23%. They have less cash advance frequency of just 4% and the average cash advance amount is 200 dollars. The average payment made is around 1988dollars. These indicates this cluster belongs to people who are frequent credit card users with high transactions, the credit card company can target them to increase their spending by giving more attractive offers and by increasing their credit limit to encourage them to spend more.**


```python
df_clean[df_clean['cluster']==2].mean()
```




    BALANCE                              592.984174
    BALANCE_FREQUENCY                      0.900413
    PURCHASES                            742.647286
    ONEOFF_PURCHASES                      95.858537
    INSTALLMENTS_PURCHASES               647.456943
    CASH_ADVANCE                         157.697299
    PURCHASES_FREQUENCY                    0.866308
    ONEOFF_PURCHASES_FREQUENCY             0.064034
    PURCHASES_INSTALLMENTS_FREQUENCY       0.812392
    CASH_ADVANCE_FREQUENCY                 0.033621
    CASH_ADVANCE_TRX                       0.622766
    PURCHASES_TRX                         16.529163
    CREDIT_LIMIT                        3209.850029
    PAYMENTS                             889.552907
    MINIMUM_PAYMENTS                     641.460119
    PRC_FULL_PAYMENT                       0.288365
    TENURE                                11.445908
    cluster                                2.000000
    dtype: float64



## Cluster 2 Characteristics
**The cluster 2 people have very less cash advance among the clusters that is on an average of 157dollars. Their purchase frequency is high with about 86.6%. They take the cash advance very less frequently of about just 3.3%, they have very good full payment percentage rate of about 28.8%. These people are called transactors because they pay very less in interest.**


```python
df_clean[df_clean['cluster']==3].mean()
```




    BALANCE                             3380.880304
    BALANCE_FREQUENCY                      0.952370
    PURCHASES                            184.058378
    ONEOFF_PURCHASES                     122.608751
    INSTALLMENTS_PURCHASES                61.492826
    CASH_ADVANCE                        2976.624321
    PURCHASES_FREQUENCY                    0.154328
    ONEOFF_PURCHASES_FREQUENCY             0.067987
    PURCHASES_INSTALLMENTS_FREQUENCY       0.089614
    CASH_ADVANCE_FREQUENCY                 0.395214
    CASH_ADVANCE_TRX                       9.799695
    PURCHASES_TRX                          2.954303
    CREDIT_LIMIT                        5900.320801
    PAYMENTS                            2330.921739
    MINIMUM_PAYMENTS                    1559.221438
    PRC_FULL_PAYMENT                       0.031114
    TENURE                                11.511043
    cluster                                3.000000
    dtype: float64



## Cluster 3 characteristics
**These are the customers with very high credit limit of about 5900 dollars on an average. They have high credit advance frequency of 39 percent and the lowest full payment of about 3.1%. They also have the least purchase frequency among the clusters with 15.4 percent. Also they have the highest balance of about 3380 dollars. These are the people who are called as revolvers who might be using their credit card’s as a loan.**

**We were able to successfully segment the customers into clusters and this gives the credit card company a better way to target the customers than targeting them the same way. In this manner, the credit card company can make more business by getting their customers to use more.**

**Thank you for the read.**
