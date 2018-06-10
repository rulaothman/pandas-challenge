
Heroes of Pymoli Data Analysis

-Of the 780 total players, the majority of them are male. 
-The most popular items seem to be the cheapest so price may be a factor in popularity.
-Purchase count and purchase value are highest in age range 20-24. Age group 15-19 show the second highest values. As such, we can advise that marketing be targeting these age brackets to yield greater returns. 



```python
import pandas as pd
```


```python
Pymoli="/Users/rulaothman/Desktop/pandas-challenge/HeroesOfPymoli/purchase_data.json"
```


```python
currency= '${0:.2f}'
```


```python
Pymoli_df=pd.read_json(Pymoli)
Pymoli_df.head()
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




```python
#Player Count 
Player_count=Pymoli_df['SN'].value_counts().count()
Player_count
```




    573




```python
#Purchasing Analysis 
unique = Pymoli_df['Item Name'].value_counts().count()
unique
count = Pymoli_df['Price'].count()
average = Pymoli_df['Price'].mean()
total = Pymoli_df['Price'].sum()

Player_data = [{'Number of Unique Items':unique,
                'Number of Purchases':count,
                'Average Purchase Price':average,
                'Total Revenue': total}]
player_analysis = pd.DataFrame(Player_data).style.format({'Percentage': '{:.2%}', 'Average Purchase Price': currency, 'Total Revenue': currency})
player_analysis
```




<style  type="text/css" >
</style>  
<table id="T_312f751e_6c65_11e8_a5a6_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Number of Purchases</th> 
        <th class="col_heading level0 col2" >Number of Unique Items</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_312f751e_6c65_11e8_a5a6_a45e60d6c10flevel0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_312f751e_6c65_11e8_a5a6_a45e60d6c10frow0_col0" class="data row0 col0" >$2.93</td> 
        <td id="T_312f751e_6c65_11e8_a5a6_a45e60d6c10frow0_col1" class="data row0 col1" >780</td> 
        <td id="T_312f751e_6c65_11e8_a5a6_a45e60d6c10frow0_col2" class="data row0 col2" >179</td> 
        <td id="T_312f751e_6c65_11e8_a5a6_a45e60d6c10frow0_col3" class="data row0 col3" >$2286.33</td> 
    </tr></tbody> 
</table> 




```python
#Gender Demographics 
Gender_df = Pymoli_df.groupby(['Gender'])
print(Gender_df)
```

    <pandas.core.groupby.DataFrameGroupBy object at 0x11622a9e8>



```python
count = Pymoli_df.groupby(['Gender']).count()
total = Pymoli_df['Gender'].count()
percentage = count/total
gender_data = {'Percentage': percentage['SN'],
          'Total Players': count['SN']}
gender_analysis = pd.DataFrame(gender_data).style.format({'Percentage': '{:.2%}'})
gender_analysis
```




<style  type="text/css" >
</style>  
<table id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Percentage</th> 
        <th class="col_heading level0 col1" >Total Players</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10flevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10frow0_col0" class="data row0 col0" >17.44%</td> 
        <td id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10frow0_col1" class="data row0 col1" >136</td> 
    </tr>    <tr> 
        <th id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10flevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10frow1_col0" class="data row1 col0" >81.15%</td> 
        <td id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10frow1_col1" class="data row1 col1" >633</td> 
    </tr>    <tr> 
        <th id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10flevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10frow2_col0" class="data row2 col0" >1.41%</td> 
        <td id="T_31a8739c_6c65_11e8_9c4b_a45e60d6c10frow2_col1" class="data row2 col1" >11</td> 
    </tr></tbody> 
</table> 




```python
#Purchase Analysis by gender 
count = Pymoli_df.groupby(['Gender']).count()
average = Pymoli_df.groupby(['Gender']).mean()
total = Pymoli_df.groupby(['Gender']).sum()
normalized_total = total/Pymoli_df['Gender'].count()

genderpurchase_data= {'Purchase Count': count['Price'],
           'Average Purchase Price': average['Price'],
           'Total Purchase Value': total['Price'], 'Normalized Totals': normalized_total['Price']}

purchase_analysis = pd.DataFrame(genderpurchase_data).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency, 'Normalized Totals': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Normalized Totals</th> 
        <th class="col_heading level0 col2" >Purchase Count</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10flevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow0_col0" class="data row0 col0" >$2.82</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow0_col1" class="data row0 col1" >$0.49</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow0_col2" class="data row0 col2" >136</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow0_col3" class="data row0 col3" >$382.91</td> 
    </tr>    <tr> 
        <th id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10flevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow1_col0" class="data row1 col0" >$2.95</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow1_col1" class="data row1 col1" >$2.39</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow1_col2" class="data row1 col2" >633</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow1_col3" class="data row1 col3" >$1867.68</td> 
    </tr>    <tr> 
        <th id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10flevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow2_col0" class="data row2 col0" >$3.25</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow2_col1" class="data row2 col1" >$0.05</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow2_col2" class="data row2 col2" >11</td> 
        <td id="T_31d8608c_6c65_11e8_8e27_a45e60d6c10frow2_col3" class="data row2 col3" >$35.74</td> 
    </tr></tbody> 
</table> 




```python
Pymoli_df['Age'].max()
```




    45




```python
Pymoli_df['Age'].min()
```




    7




```python
#4-year bins 
bins=([0, 10, 15, 20, 25, 30, 35, 40, 45])
group_names= ["<10","10-14","15-19","20-24","25-29","30-34","35-39","40+"]

df= Pymoli_df.groupby(pd.cut(Pymoli_df["Age"], bins, labels = group_names))
count= Pymoli_df.groupby(pd.cut(Pymoli_df["Age"], bins, labels = group_names)).count()
average= Pymoli_df.groupby(pd.cut(Pymoli_df["Age"], bins, labels = group_names)).mean()
total= Pymoli_df.groupby((pd.cut(Pymoli_df["Age"], bins, labels = group_names))).sum()
normalized_total= total/Pymoli_df['Gender'].count()

agedemo_data= {'Purchase Count': count['Price'],
           'Average Purchase Price': average['Price'],
           'Total Purchase Value': total['Price'], 'Normalized Totals': normalized_total['Price']}
purchase_analysis = pd.DataFrame(agedemo_data).rename(index={'0-10':'<10','10-14':'10-14','15-19':'15-19','20-24':'20-24','25-29':'25-29','30-34':'30-34','35-39':'35-39','40+':'>40'}).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency, 'Normalized Totals': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_32804614_6c65_11e8_ac3a_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Normalized Totals</th> 
        <th class="col_heading level0 col2" >Purchase Count</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Age</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow0_col0" class="data row0 col0" >$3.02</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow0_col1" class="data row0 col1" >$0.12</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow0_col2" class="data row0 col2" >32</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow0_col3" class="data row0 col3" >$96.62</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow1_col0" class="data row1 col0" >$2.87</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow1_col1" class="data row1 col1" >$0.29</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow1_col2" class="data row1 col2" >78</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow1_col3" class="data row1 col3" >$224.15</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow2_col0" class="data row2 col0" >$2.87</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow2_col1" class="data row2 col1" >$0.68</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow2_col2" class="data row2 col2" >184</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow2_col3" class="data row2 col3" >$528.74</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow3_col0" class="data row3 col0" >$2.96</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow3_col1" class="data row3 col1" >$1.16</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow3_col2" class="data row3 col2" >305</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow3_col3" class="data row3 col3" >$902.61</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow4_col0" class="data row4 col0" >$2.89</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow4_col1" class="data row4 col1" >$0.28</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow4_col2" class="data row4 col2" >76</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow4_col3" class="data row4 col3" >$219.82</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow5_col0" class="data row5 col0" >$3.07</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow5_col1" class="data row5 col1" >$0.23</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow5_col2" class="data row5 col2" >58</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow5_col3" class="data row5 col3" >$178.26</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow6_col0" class="data row6 col0" >$2.90</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow6_col1" class="data row6 col1" >$0.16</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow6_col2" class="data row6 col2" >44</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow6_col3" class="data row6 col3" >$127.49</td> 
    </tr>    <tr> 
        <th id="T_32804614_6c65_11e8_ac3a_a45e60d6c10flevel0_row7" class="row_heading level0 row7" >>40</th> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow7_col0" class="data row7 col0" >$2.88</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow7_col1" class="data row7 col1" >$0.01</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow7_col2" class="data row7 col2" >3</td> 
        <td id="T_32804614_6c65_11e8_ac3a_a45e60d6c10frow7_col3" class="data row7 col3" >$8.64</td> 
    </tr></tbody> 
</table> 




```python
#Top 5 Spenders 
count = Pymoli_df.groupby(['SN']).count()
average = Pymoli_df.groupby(['SN']).mean()
total = Pymoli_df.groupby(['SN']).sum()

topspender_data= {'Purchase Count': count['Price'],
           'Average Purchase Price': average['Price'],
           'Total Purchase Value': total['Price']}
purchase_analysis = pd.DataFrame(topspender_data).sort_values('Total Purchase Value', ascending=False).head(5).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis

```




<style  type="text/css" >
</style>  
<table id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >SN</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10flevel0_row0" class="row_heading level0 row0" >Undirrala66</th> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow0_col0" class="data row0 col0" >$3.41</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow0_col1" class="data row0 col1" >5</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow0_col2" class="data row0 col2" >$17.06</td> 
    </tr>    <tr> 
        <th id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10flevel0_row1" class="row_heading level0 row1" >Saedue76</th> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow1_col0" class="data row1 col0" >$3.39</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow1_col1" class="data row1 col1" >4</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow1_col2" class="data row1 col2" >$13.56</td> 
    </tr>    <tr> 
        <th id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10flevel0_row2" class="row_heading level0 row2" >Mindimnya67</th> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow2_col0" class="data row2 col0" >$3.18</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow2_col1" class="data row2 col1" >4</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow2_col2" class="data row2 col2" >$12.74</td> 
    </tr>    <tr> 
        <th id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10flevel0_row3" class="row_heading level0 row3" >Haellysu29</th> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow3_col0" class="data row3 col0" >$4.24</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow3_col1" class="data row3 col1" >3</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow3_col2" class="data row3 col2" >$12.73</td> 
    </tr>    <tr> 
        <th id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10flevel0_row4" class="row_heading level0 row4" >Eoda93</th> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow4_col0" class="data row4 col0" >$3.86</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow4_col1" class="data row4 col1" >3</td> 
        <td id="T_32a026d2_6c65_11e8_ba7b_a45e60d6c10frow4_col2" class="data row4 col2" >$11.58</td> 
    </tr></tbody> 
</table> 




```python
#Most Popular Item
count = Pymoli_df.groupby(['Item ID','Item Name']).count()
average = Pymoli_df.groupby(['Item ID','Item Name']).mean()
total = Pymoli_df.groupby(['Item ID','Item Name']).sum()

topitem_data= {'Purchase Count': count['Price'],
           'Average Purchase Price': average['Price'],
           'Total Purchase Value': total['Price']}

purchase_analysis = pd.DataFrame(topitem_data).sort_values('Purchase Count', ascending=False).head(5).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel0_row0" class="row_heading level0 row0" >39</th> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel1_row0" class="row_heading level1 row0" >Betrayal, Whisper of Grieving Widows</th> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow0_col0" class="data row0 col0" >$2.35</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow0_col1" class="data row0 col1" >11</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow0_col2" class="data row0 col2" >$25.85</td> 
    </tr>    <tr> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel0_row1" class="row_heading level0 row1" >84</th> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel1_row1" class="row_heading level1 row1" >Arcane Gem</th> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow1_col0" class="data row1 col0" >$2.23</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow1_col1" class="data row1 col1" >11</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow1_col2" class="data row1 col2" >$24.53</td> 
    </tr>    <tr> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel0_row2" class="row_heading level0 row2" >31</th> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel1_row2" class="row_heading level1 row2" >Trickster</th> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow2_col0" class="data row2 col0" >$2.07</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow2_col1" class="data row2 col1" >9</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow2_col2" class="data row2 col2" >$18.63</td> 
    </tr>    <tr> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel0_row3" class="row_heading level0 row3" >175</th> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel1_row3" class="row_heading level1 row3" >Woeful Adamantite Claymore</th> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow3_col0" class="data row3 col0" >$1.24</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow3_col1" class="data row3 col1" >9</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow3_col2" class="data row3 col2" >$11.16</td> 
    </tr>    <tr> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel0_row4" class="row_heading level0 row4" >13</th> 
        <th id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10flevel1_row4" class="row_heading level1 row4" >Serenity</th> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow4_col0" class="data row4 col0" >$1.49</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow4_col1" class="data row4 col1" >9</td> 
        <td id="T_32c90a5c_6c65_11e8_95da_a45e60d6c10frow4_col2" class="data row4 col2" >$13.41</td> 
    </tr></tbody> 
</table> 




```python
#Most Profitable Item
purchase_analysis = pd.DataFrame(topitem_data).sort_values('Total Purchase Value', ascending=False).head(5).style.format({'Average Purchase Price': currency, 'Total Purchase Value': currency})
purchase_analysis
```




<style  type="text/css" >
</style>  
<table id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10f" > 
<thead>    <tr> 
        <th class="blank" ></th> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Purchase Count</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Item ID</th> 
        <th class="index_name level1" >Item Name</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel0_row0" class="row_heading level0 row0" >34</th> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel1_row0" class="row_heading level1 row0" >Retribution Axe</th> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow0_col0" class="data row0 col0" >$4.14</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow0_col1" class="data row0 col1" >9</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow0_col2" class="data row0 col2" >$37.26</td> 
    </tr>    <tr> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel0_row1" class="row_heading level0 row1" >115</th> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel1_row1" class="row_heading level1 row1" >Spectral Diamond Doomblade</th> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow1_col0" class="data row1 col0" >$4.25</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow1_col1" class="data row1 col1" >7</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow1_col2" class="data row1 col2" >$29.75</td> 
    </tr>    <tr> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel0_row2" class="row_heading level0 row2" >32</th> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel1_row2" class="row_heading level1 row2" >Orenmir</th> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow2_col0" class="data row2 col0" >$4.95</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow2_col1" class="data row2 col1" >6</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow2_col2" class="data row2 col2" >$29.70</td> 
    </tr>    <tr> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel0_row3" class="row_heading level0 row3" >103</th> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel1_row3" class="row_heading level1 row3" >Singed Scalpel</th> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow3_col0" class="data row3 col0" >$4.87</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow3_col1" class="data row3 col1" >6</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow3_col2" class="data row3 col2" >$29.22</td> 
    </tr>    <tr> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel0_row4" class="row_heading level0 row4" >107</th> 
        <th id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10flevel1_row4" class="row_heading level1 row4" >Splitter, Foe Of Subtlety</th> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow4_col0" class="data row4 col0" >$3.61</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow4_col1" class="data row4 col1" >8</td> 
        <td id="T_32fba9b4_6c65_11e8_814f_a45e60d6c10frow4_col2" class="data row4 col2" >$28.88</td> 
    </tr></tbody> 
</table> 


