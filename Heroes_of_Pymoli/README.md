

```python
import pandas as pd

purchase_df = pd.read_json('purchase_data.json')

purchase_df.head()
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
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>



# Player Count


```python
#count unique SN names
total_players = purchase_df["SN"].nunique()

#create total players dataframe
total_players_df = pd.DataFrame({"Total Players" : [total_players]})

#display dataframe
total_players_df
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)


```python
#variable to hold unique count of Item ID
unique_items = purchase_df["Item ID"].nunique()

#variable to hold mean value of Price
average_price = purchase_df["Price"].mean()

#variable to hold count of Item ID
total_purchases = purchase_df["Item ID"].count()

#variable to hold sum of Price
total_revenue = purchase_df["Price"].sum()

#creates dataframe that combines the above variables 
purchase_analysis_df = pd.DataFrame({"Number of Unique Items" : [unique_items]
                                     ,"Average Price" : [average_price]
                                     ,"Number of Purchases" : [total_purchases]
                                     ,"Total Revenue" : [total_revenue]
                                     })
#format Average Price to currency
purchase_analysis_df["Average Price"] = purchase_analysis_df["Average Price"].map("${:,.2f}".format)

#format Total Revenue to currency
purchase_analysis_df["Total Revenue"] = purchase_analysis_df["Total Revenue"].map("${:,.2f}".format)

#order the columns in the dataframe
purchase_analysis_df = purchase_analysis_df[["Number of Unique Items", "Average Price", "Number of Purchases", "Total Revenue"]]

#display dataframe
purchase_analysis_df

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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>183</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2,286.33</td>
    </tr>
  </tbody>
</table>
</div>



# Gender Demographics


```python
#variable to hold unique count of SN names
gender_count = purchase_df.groupby("Gender")["SN"].nunique()

#variable for the sumtotal of unique count of each gender
gender_sum_cnt = purchase_df.groupby("Gender")["SN"].nunique().sum()

#divide unique count by sumtotal of unique count
gender_pct = (gender_count/gender_sum_cnt)*100

#create dataframe 
gender_demo_df = pd.DataFrame({"Total Count" : gender_count
                                     ,"Percent of Players" : gender_pct
                                     })

#format Percent of Players to round to two decimal places
gender_demo_df["Percent of Players"] = gender_demo_df["Percent of Players"].map("{:,.2f}".format)

#order columns in datafame
gender_demographics = gender_demo_df[["Percent of Players", "Total Count"]]

#display dataframe
gender_demographics
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
      <th>Percent of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



# Purchase Analysis (Gender)


```python
#variables for all calculations (count, average, sum, unique count, normalized total)
gp_count = purchase_df.groupby("Gender")["SN"].count()
gp_avg   = purchase_df.groupby("Gender")["Price"].mean()
gp_total = purchase_df.groupby("Gender")["Price"].sum()
gp_unique = purchase_df.groupby("Gender")["SN"].nunique()
gp_norm  = gp_total/gp_unique

#create datafram
gp_df = pd.DataFrame({"Purchase Count" : gp_count
                     ,"Average Purchase Price" : gp_avg
                     ,"Total Purchase Value" : gp_total
                     ,"Normalized Totals" : gp_norm})

#format Average Purchase Price, Total Purchase Value, and Normalized Totals to currency 
gp_df["Average Purchase Price"] = gp_df["Average Purchase Price"].map("${:,.2f}".format)
gp_df["Total Purchase Value"] = gp_df["Total Purchase Value"].map("${:,.2f}".format)
gp_df["Normalized Totals"] = gp_df["Normalized Totals"].map("${:,.2f}".format)

#order columns in dataframe
purchase_analysis_by_gender = gp_df[["Purchase Count"
                                     , "Average Purchase Price"
                                     , "Total Purchase Value"
                                     , "Normalized Totals"]]
#display dataframe
purchase_analysis_by_gender
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$3.83</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>$2.95</td>
      <td>$1,867.68</td>
      <td>$4.02</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>$4.47</td>
    </tr>
  </tbody>
</table>
</div>



# Age Demographics


```python
#get min age for lower bin limit if > 0, will use 0
min_age = purchase_df["Age"].min()
#get max age for upper bin limit 
max_age = purchase_df["Age"].max()

#create bins
bins = [0, 9, 14, 19, 24, 29, 34, 39, 47]

#create bin labels
group_names = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']

#cut bins to bin labels and assign by age
age_binning = pd.cut(purchase_df["Age"], bins, labels=group_names)

#add age group to purchase df dataframe 
purchase_df['Age Group'] = age_binning


#variable to hold unique count of SN names
age_count = purchase_df.groupby("Age Group")["SN"].nunique()

#variable for the sumtotal of unique count of each age group
age_sum_cnt = purchase_df.groupby("Age Group")["SN"].nunique().sum()

#divide unique count by sumtotal of unique count
age_pct = (age_count/age_sum_cnt)*100

#create dataframe 
age_demo_df = pd.DataFrame({"Total Count" : age_count, "Percentage of Players" : age_pct
                                     })

#format Percent of Players to round to two decimal places
age_demo_df["Percentage of Players"] = age_demo_df["Percentage of Players"].map("{:,.2f}".format)

#order columns in datafame
age_demographics = age_demo_df[["Percentage of Players", "Total Count"]]

#display dataframe
age_demographics

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
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>3.32</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.01</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.20</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>15.18</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.20</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>4.71</td>
      <td>27</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1.92</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



# Purchase Analysis (Age)


```python
#variables for all calculations (count, average, sum, unique count, normalized total)
ap_count = purchase_df.groupby("Age Group")["SN"].count()
ap_avg   = purchase_df.groupby("Age Group")["Price"].mean()
ap_total = purchase_df.groupby("Age Group")["Price"].sum()
ap_unique = purchase_df.groupby("Age Group")["SN"].nunique()
ap_norm  = ap_total/ap_unique

#create dataframe
ap_df = pd.DataFrame({"Purchase Count" : ap_count
                     ,"Average Purchase Price" : ap_avg
                     ,"Total Purchase Value" : ap_total
                     ,"Normalized Totals" : ap_norm})

#format Average Purchase Price, Total Purchase Value, and Normalized Totals to currency 
ap_df["Average Purchase Price"] = ap_df["Average Purchase Price"].map("${:,.2f}".format)
ap_df["Total Purchase Value"] = ap_df["Total Purchase Value"].map("${:,.2f}".format)
ap_df["Normalized Totals"] = ap_df["Normalized Totals"].map("${:,.2f}".format)

#order columns in dataframe
purchase_analysis_by_age_group = ap_df[["Purchase Count"
                                     , "Average Purchase Price"
                                     , "Total Purchase Value"
                                     , "Normalized Totals"]]
#display dataframe
purchase_analysis_by_age_group
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>28</td>
      <td>$2.98</td>
      <td>$83.46</td>
      <td>$4.39</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>35</td>
      <td>$2.77</td>
      <td>$96.95</td>
      <td>$4.22</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>133</td>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>336</td>
      <td>$2.91</td>
      <td>$978.77</td>
      <td>$3.78</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>125</td>
      <td>$2.96</td>
      <td>$370.33</td>
      <td>$4.26</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>64</td>
      <td>$3.08</td>
      <td>$197.25</td>
      <td>$4.20</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>42</td>
      <td>$2.84</td>
      <td>$119.40</td>
      <td>$4.42</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>17</td>
      <td>$3.16</td>
      <td>$53.75</td>
      <td>$4.89</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
#variables for all calculations (count, average, sum)
item_count = purchase_df.groupby('SN')['SN'].count()
total_value = purchase_df.groupby('SN')['Price'].sum()
avg_price = purchase_df.groupby('SN')['Price'].mean()

#create dataframe to combine variables
spender_combine = pd.DataFrame({"Purchase Count" : item_count
                              ,"Average Purchase Price": avg_price
                              ,"Total Purchase Value": total_value})

#sort dataframe rows by Total Purchase Value Highest to Lowest
spender_sort = spender_combine.sort_values("Total Purchase Value", ascending=False)

#format sorted dataframe for currency values
spender_sort["Average Purchase Price"] = spender_sort["Average Purchase Price"].map("${:,.2f}".format)
spender_sort["Total Purchase Value"] = spender_sort["Total Purchase Value"].map("${:,.2f}".format)

#show only first five rows
spender_5_df = spender_sort.iloc[0:5]

#order columns in dataframe
spender_5_df_final = spender_5_df[["Purchase Count", "Average Purchase Price" , "Total Purchase Value"]]

#display dataframe
spender_5_df_final

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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
#variables for all calculations (count, max, sum)
p_count = purchase_df.groupby(["Item ID", "Item Name"])["Item ID"].count()
p_value = purchase_df.groupby(["Item ID", "Item Name"])["Price"].sum()
p_price = purchase_df.groupby(["Item ID", "Item Name"])['Price'].max()

#create dataframe to combine variables
popular_combine = pd.DataFrame({"Purchase Count" : p_count
                              ,"Total Purchase Value": p_value
                              ,"Item Price": p_price})

#sort dataframe rows by Purchase Count Highest to Lowest
popular_sort = popular_combine.sort_values("Purchase Count", ascending=False)

#format sorted dataframe for currency values
popular_sort["Total Purchase Value"] = popular_sort["Total Purchase Value"].map("${:,.2f}".format)
popular_sort["Item Price"] = popular_sort["Item Price"].map("${:,.2f}".format)

#show only first five rows
popular_5_df = popular_sort.iloc[0:5]

#order columns in dataframe
popular_5_df_final = popular_5_df[["Purchase Count", "Item Price" , "Total Purchase Value"]]

#display dataframe
popular_5_df_final
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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>



# Most Profitable Items


```python
#variables for all calculations (count, average, sum)
item_count = purchase_df.groupby(["Item ID", "Item Name"])["Item ID"].count()
item_price = purchase_df.groupby(["Item ID", "Item Name"])["Price"].max()
total_value = purchase_df.groupby(["Item ID", "Item Name"])["Price"].sum()

#create dataframe to combine variables
item_by_profit_combine = pd.DataFrame({"Purchase Count" : item_count
                              , "Item Price": item_price
                              ,"Total Purchase Value": total_value})

#sort dataframe rows by Purchase Count Highest to Lowest
profit_sort = item_by_profit_combine.sort_values("Total Purchase Value", ascending=False)

#format sorted dataframe for currency values
profit_sort["Item Price"] = profit_sort["Item Price"].map("${:,.2f}".format)
profit_sort["Total Purchase Value"] = profit_sort["Total Purchase Value"].map("${:,.2f}".format)

#show only first five rows
profit_5_df = profit_sort.iloc[0:5]

#show only first five rows
profit_5_df_final = profit_5_df[["Purchase Count", "Item Price" , "Total Purchase Value"]]

#display dataframe
profit_5_df_final

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
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


