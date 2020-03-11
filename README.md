# UTexas-Week2


6. Business understanding of the model
We can divide the customers into different income groups depending on the constraints of sales resources in the Bank. As shown in figure below, the bank is able to offer personal loan products to customers with income exceeding 110K. However, it failed to capture significant percentage of customers who earn less than 110K.

It is recommended that the bank starts to look at

In [146]:
bins = [0,60,80,90,100,110,300]
groups = bank_data.groupby(['Personal Loan', pd.cut(bank_data['Income'], bins)])
groups.size().unstack()
Out[146]:
Income	(0, 60]	(60, 80]	(80, 90]	(90, 100]	(100, 110]	(110, 300]
Personal Loan						
0	2331	790	429	196	124	650
1	1	6	15	20	27	411
6.1 Customers earning exceeding 100K and below 100K
For the figure below that less than 20% of customers with income between 100K to 110K have a personal loan. We could learn from the high precision model with more than 0.8 of recall and precision values to identify customers who would sign up personal loan. Using the print(pd.DataFrame(model.coef_)), we could identify the coefficient of the attributes and identify customers who are within the attribute values but have not signup a personal loan.

In [148]:
bank_data_exceed_hundred_k = bank_data[(bank_data.Income>100) & (bank_data.Income<110)] 
generate_percentage_count = lambda x : pd.Series.value_counts(x)
generate_categorical_values(bank_data_exceed_hundred_k, ["Personal Loan", "Securities Account", "CD Account", "Online", "CreditCard"]).apply(generate_percentage_count)
C:\Anaconda3\lib\site-packages\ipykernel_launcher.py:4: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
  after removing the cwd from sys.path.
Out[148]:
Personal Loan	Securities Account	CD Account	Online	CreditCard
0	108	115	122	59	98
1	24	17	10	73	34
6.2 Customers earning below 100K
For the figure below, we could learn from the model with 0.04 precision and 0.88 recall to identify customers who would sign up personal loan. Using the print(pd.DataFrame(model.coef_)), we could identify the coefficient of the attributes and identify customers who are within the attribute values but have not signed up a personal loan.

However, it is important for the bank to offer personal loan to some customers of this group and also collect data to further improve the model. The potential for customers without personal loans are high in this group because only slightly more than 1% of them own a personal loan.

In [131]:
bank_data_exceed_hundred_k = bank_data[bank_data.Income<100] 
generate_percentage_count = lambda x : pd.Series.value_counts(x)
generate_categorical_values(bank_data_exceed_hundred_k, ["Personal Loan", "Securities Account", "CD Account", "Online", "CreditCard"]).apply(generate_percentage_count)
C:\Anaconda3\lib\site-packages\ipykernel_launcher.py:4: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
  after removing the cwd from sys.path.
Out[131]:
Personal Loan	Securities Account	CD Account	Online	CreditCard
0	3737	3383	3635	1525	2667
1	41	395	143	2253	1111
