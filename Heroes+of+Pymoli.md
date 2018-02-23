

```python
# Dependencies
import pandas as pd
import json

# Load json
# Read data with Pandas
json_path = "purchase_data.json"

game_data_df = pd.read_json(json_path, orient = "records")

game_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
# **Player Count**
# Total Number of Players
players_unique_df = game_data_df.loc[:,["Age", "Gender", "SN"]]
players_unique_df = players_unique_df.drop_duplicates()
#print(players_unique_df)
player_count = len(players_unique_df)
player_count_df = pd.DataFrame({"Total Players":[player_count]})

player_count_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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



#  Purchasing Analysis (Total)


```python
# **Purchasing Analysis (Total)**

# Number of Unique Items
unique_items = len(game_data_df["Item ID"].unique())

# Average Purchase Price
avg_purchase_price = game_data_df["Price"].mean()

# Total Number of Purchases
total_purchases = game_data_df["Price"].count()

# Total Revenue
total_revenue = game_data_df["Price"].sum()

purchasing_analysis_df = pd.DataFrame({"Number of Unique Items":[unique_items], "Average Purchase Price": [avg_purchase_price], \
                               "Total Number of Purchases": [total_purchases], "Total Revenue": [total_revenue]},\
                                 columns = ["Number of Unique Items", "Average Purchase Price", "Total Number of Purchases", \
                                            "Total Revenue"])
purchasing_analysis_df["Average Purchase Price"] = purchasing_analysis_df["Average Purchase Price"].map('${:.2f}'.format)
purchasing_analysis_df["Total Revenue"] = purchasing_analysis_df["Total Revenue"].map('${:,.2f}'.format)

print("PURCHASING ANALYSIS:")
purchasing_analysis_df


```

    PURCHASING ANALYSIS:
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Purchase Price</th>
      <th>Total Number of Purchases</th>
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
# **Gender Demographics**
# use the filtered non-duplicate data for age related calculations and summaries.
# Percentage and Count of Male Players
# Percentage and Count of Female Players
# Percentage and Count of Other / Non-Disclosed

players_unique_gender = players_unique_df["Gender"].value_counts()
percent_players = (players_unique_gender/player_count) * 100

gender_demographics_df = pd.DataFrame({"Total Count": players_unique_gender, "Percentage of Players": percent_players})

gender_demographics_df["Percentage of Players"] = gender_demographics_df["Percentage of Players"].map('{:,.2f}'.format)

print("GENDER DEMOGRAPHICS:")
gender_demographics_df


```

    GENDER DEMOGRAPHICS:
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.40</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Gender)


```python
#**Purchasing Analysis (Gender)** 
# use the original game data for price related calculations and summaries.
# The below each broken by gender

# Purchase Count
purchase_count = game_data_df.groupby("Gender")["Price"].count()

# Average Purchase Price
avg_purchase_price = game_data_df.groupby("Gender")["Price"].mean()

# Total Purchase Value
total_purchase_value = game_data_df.groupby("Gender")["Price"].sum()

# Normalized Totals
normalized_totals = total_purchase_value / gender_demographics_df["Total Count"]

gender_analysis_df = pd.DataFrame({"Purchase Count": purchase_count, "Average Purchase Price": avg_purchase_price, \
                                   "Total Purchase Value": total_purchase_value,"Normalized Totals": normalized_totals}, \
                                  columns = ["Purchase Count", "Average Purchase Price", "Total Purchase Value",\
                                             "Normalized Totals"])

gender_analysis_df["Average Purchase Price"] =gender_analysis_df["Average Purchase Price"].map('${:,.2f}'.format)
gender_analysis_df["Total Purchase Value"] =gender_analysis_df["Total Purchase Value"].map('${:,.2f}'.format)
gender_analysis_df["Normalized Totals"] =gender_analysis_df["Normalized Totals"].map('${:,.2f}'.format)

print("PURCHASING ANALYSIS (Gender):")
gender_analysis_df

```

    PURCHASING ANALYSIS (Gender):
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
#**Age Demographics**
# group the non-duplicate data by bins. Use this data for age related calculations and summaries.
# The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
bins_age = [0, 9.5, 14.5, 19.5, 24.5, 29.5, 34.5, 39.5, 100]
group_names_age = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]
players_unique_df["Age Ranges"] = pd.cut(players_unique_df["Age"], bins_age, labels=group_names_age)

#print("NON-DUPLICATE GAME DATA WITH AGE RANGES:")
#players_unique_df.head()

```


```python
# Percentage of players and Total Count Players in each bin
total_count_age = players_unique_df["Age Ranges"].value_counts()
percent_players_age = total_count_age / player_count * 100
age_demographics_df = pd.DataFrame({"Percentage of players": percent_players_age, "Total Count": total_count_age})

age_demographics_df["Percentage of players"] =age_demographics_df["Percentage of players"].map('{:,.2f}'.format)
age_demographics_df.sort_index()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of players</th>
      <th>Total Count</th>
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



# Purchasing Analysis (Age)


```python
# group the original game data by bins. Use this data for purchase/price related calculations. 
game_data_df["Age Ranges"] = pd.cut(game_data_df["Age"], bins_age, labels=group_names_age)

#Sprint("ORIGINAL GAME DATA WITH AGE RANGES:")
#game_data_df.head()

```


```python
# Purchase Count
purchase_count_age = game_data_df.groupby("Age Ranges")["Price"].count()

# Average Purchase Price
avg_purchase_price_age = game_data_df.groupby("Age Ranges")["Price"].mean()

# Total Purchase Value
total_purchase_value_age = game_data_df.groupby("Age Ranges")["Price"].sum()

# Normalized Totals
normalized_totals_age = Total_purchase_value_age / age_demographics_df["Total Count"]

age_analysis_df = pd.DataFrame({"Purchase Count": purchase_count_age, "Average Purchase Price": avg_purchase_price_age, \
                                   "Total Purchase Value": total_purchase_value_age,"Normalized Totals": normalized_totals_age}, \
                                  columns = ["Purchase Count", "Average Purchase Price", "Total Purchase Value",\
                                             "Normalized Totals"])

age_analysis_df["Average Purchase Price"] = age_analysis_df["Average Purchase Price"].map('${:,.2f}'.format)
age_analysis_df["Total Purchase Value"] = age_analysis_df["Total Purchase Value"].map('${:,.2f}'.format)
age_analysis_df["Normalized Totals"] = age_analysis_df["Normalized Totals"].map('${:,.2f}'.format)

print("PURCHASING ANALYSIS (Age):")
age_analysis_df
```

    PURCHASING ANALYSIS (Age):
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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




```python
#game_data_df.head()
```

# Top Spenders


```python
# **Top Spenders**
# Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
# SN
# Purchase Count
# Average Purchase Price
# Total Purchase Value

player_purchase_count = game_data_df.groupby("SN")["Price"].count()
player_avg_price = game_data_df.groupby("SN")["Price"].mean()
player_total_price = game_data_df.groupby("SN")["Price"].sum()

top_spenders_df = pd.DataFrame({"Purchase Count": player_purchase_count, "Average Purchase Price": player_avg_price, \
                               "Total Purchase Value": player_total_price}, \
                               columns = ["Purchase Count", "Average Purchase Price", "Total Purchase Value"])

top_spenders_df["Average Purchase Price"] = top_spenders_df["Average Purchase Price"].map('${:.2f}'.format)
top_spenders_df["Total Purchase Value"] = top_spenders_df["Total Purchase Value"].map('${:.2f}'.format)

#top_spenders_df.sort_values("Total Purchase Value")
top_spenders_df = top_spenders_df.sort_values("Total Purchase Value", ascending=False)

print("TOP 5 SPENDERS IN THE GAME:")
top_spenders_df.head()


```

    TOP 5 SPENDERS IN THE GAME:
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <th>Qarwen67</th>
      <td>4</td>
      <td>$2.49</td>
      <td>$9.97</td>
    </tr>
    <tr>
      <th>Sondim43</th>
      <td>3</td>
      <td>$3.13</td>
      <td>$9.38</td>
    </tr>
    <tr>
      <th>Tillyrin30</th>
      <td>3</td>
      <td>$3.06</td>
      <td>$9.19</td>
    </tr>
    <tr>
      <th>Lisistaya47</th>
      <td>3</td>
      <td>$3.06</td>
      <td>$9.19</td>
    </tr>
    <tr>
      <th>Tyisriphos58</th>
      <td>2</td>
      <td>$4.59</td>
      <td>$9.18</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
# **Most Popular Items**
# Identify the 5 most popular items by purchase count, then list (in a table):
# Item ID
# Item Name
# Purchase Count
# Item Price
# Total Purchase Value

# SINCE SOME OF THE ITEMS HAVE DIFFERENT ITEM IDs FOR THE SAME ITEM NAME, I'LL BE GROUPING BY ITEM ITEM IDS/ITEM NAME
# SOME ITEMS LIKE FINAL CRITIC HAVE 14 ITEM NAMES BUT 2 DIFFERENT IDS (92 and 101)

most_popular_count = game_data_df.groupby(["Item ID", "Item Name"])["Price"].count()
most_popular_price = game_data_df.groupby(["Item ID", "Item Name"])["Price"].mean()
most_popular_total_pvalue = game_data_df.groupby(["Item ID", "Item Name"])["Price"].sum()
most_popular_name = game_data_df.groupby("Item ID")["Item Name"]

most_popular_df = pd.DataFrame({"Purchase Count": most_popular_count, "Item Price": most_popular_price, \
                                "Total Purchase Value": most_popular_total_pvalue}, \
                               columns = ["Purchase Count", "Item Price", "Total Purchase Value"])

most_popular_df = most_popular_df.sort_values("Purchase Count", ascending=False)

print("TOP 5 MOST POPULAR ITEMS:")
most_popular_df.head()


```

    TOP 5 MOST POPULAR ITEMS:
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>2.35</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>2.23</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>2.07</td>
      <td>18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>1.24</td>
      <td>11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>1.49</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>



# Most Profitable Items


```python
# **Most Profitable Items**
# Identify the 5 most profitable items by total purchase value, then list (in a table):
# Item ID
# Item Name
# Purchase Count
# Item Price
# Total Purchase Value

most_profitable_df = pd.DataFrame({"Purchase Count": most_popular_count, "Item Price": most_popular_price, \
                                "Total Purchase Value": most_popular_total_pvalue}, \
                               columns = ["Purchase Count", "Item Price", "Total Purchase Value"])

most_profitable_df = most_popular_df.sort_values("Total Purchase Value", ascending=False)

print("TOP 5 MOST PROFITABLE ITEMS: ")
most_profitable_df.head()


```

    TOP 5 MOST PROFITABLE ITEMS: 
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
      <td>4.14</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>4.25</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>4.95</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>4.87</td>
      <td>29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>3.61</td>
      <td>28.88</td>
    </tr>
  </tbody>
</table>
</div>


