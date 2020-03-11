# UTexas-Week2


# Thera Bank Personal Loan Campaign

# Objective
The file Bank.xls contains data on 5000 customers. The data include customer demographic information (age, income, etc.), the customer's relationship with the bank (mortgage, securities account, etc.), and the customer response to the last personal loan campaign (Personal Loan). Among these 5000 customers, only 480 (= 9.6%) accepted the personal loan that was offered to them in the earlier campaign.

This case is about a bank (Thera Bank) whose management wants to explore ways of converting its liability customers to personal loan customers (while retaining them as depositors). A campaign that the bank ran last year for liability customers showed a healthy conversion rate of over 9% success. This has encouraged the retail marketing department to devise campaigns with better target marketing to increase the success ratio with a minimal budget.

# Business understanding of the model

We can divide the customers into different income groups depending on the constraints of sales resources in the Bank. As shown in figure below, the bank is successful to offer personal loan products to customers with income exceeding 110K. However, it failed to capture significant percentage of customers who earn less than 110K.

It is recommended that the bank starts to focus on customers with income below 100K and offers competitive personal loan products to attract them.

For visit this web page for detailed analytics of the project.
https://github.com/koksoon100/UTexas-Week2/blob/master/week_2_assignment.ipynb


```python
bins = [0,60,80,90,100,110,300]
groups = bank_data.groupby(['Personal Loan', pd.cut(bank_data['Income'], bins)])
groups.size().unstack()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Income</th>
      <th>(0, 60]</th>
      <th>(60, 80]</th>
      <th>(80, 90]</th>
      <th>(90, 100]</th>
      <th>(100, 110]</th>
      <th>(110, 300]</th>
    </tr>
    <tr>
      <th>Personal Loan</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2331</td>
      <td>790</td>
      <td>429</td>
      <td>196</td>
      <td>124</td>
      <td>650</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>6</td>
      <td>15</td>
      <td>20</td>
      <td>27</td>
      <td>411</td>
    </tr>
  </tbody>
</table>
</div>



## 1 Customers earning exceeding 100K and below 100K

For the figure below that less than 20% of customers with income between 100K to 110K have a personal loan. We could learn from the high precision model with more than 0.8 of recall and precision values to identify customers who would sign up personal loan. Using the print(pd.DataFrame(model.coef_)), we could identify the coefficient of the attributes and identify customers who are within the attribute values but have not signup a personal loan.


```python
bank_data_exceed_hundred_k = bank_data[(bank_data.Income>100) & (bank_data.Income<110)] 
generate_percentage_count = lambda x : pd.Series.value_counts(x)
generate_categorical_values(bank_data_exceed_hundred_k, ["Personal Loan", "Securities Account", "CD Account", "Online", "CreditCard"]).apply(generate_percentage_count)
```



<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Personal Loan</th>
      <th>Securities Account</th>
      <th>CD Account</th>
      <th>Online</th>
      <th>CreditCard</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>108</td>
      <td>115</td>
      <td>122</td>
      <td>59</td>
      <td>98</td>
    </tr>
    <tr>
      <th>1</th>
      <td>24</td>
      <td>17</td>
      <td>10</td>
      <td>73</td>
      <td>34</td>
    </tr>
  </tbody>
</table>
</div>



## 2 Customers earning below 100K

For the figure below, we could learn from the model with 0.04 precision and 0.88 recall to identify customers who would sign up personal loan. Using the print(pd.DataFrame(model.coef_)), we could identify the coefficient of the attributes and identify customers who are within the attribute values but have not signed up a personal loan.

However, it is important for the bank to offer personal loan to some customers of this group and also collect data to further improve the model. The potential for customers without personal loans are high in this group because only slightly more than 1% of them own a personal loan.


```python
bank_data_exceed_hundred_k = bank_data[bank_data.Income<100] 
generate_percentage_count = lambda x : pd.Series.value_counts(x)
generate_categorical_values(bank_data_exceed_hundred_k, ["Personal Loan", "Securities Account", "CD Account", "Online", "CreditCard"]).apply(generate_percentage_count)
```
 




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Personal Loan</th>
      <th>Securities Account</th>
      <th>CD Account</th>
      <th>Online</th>
      <th>CreditCard</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3737</td>
      <td>3383</td>
      <td>3635</td>
      <td>1525</td>
      <td>2667</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41</td>
      <td>395</td>
      <td>143</td>
      <td>2253</td>
      <td>1111</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
