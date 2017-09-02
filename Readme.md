
# Academy of Py


```python
#################################################################################
# 1 Create a high level snapshot (in table form) of the district's key metrics  #
#################################################################################
```


```python
import pandas as pd
import numpy as np

file1 = './Resources/students_complete.csv'
stud_df = pd.read_csv(file1)
stud_df.head()
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
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
file2 = './Resources/schools_complete.csv'
sch_df = pd.read_csv(file2)
sch_df.head()
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
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_cnt=sch_df["School ID"].count()
tot_student=stud_df["Student ID"].count()
tot_budget=sch_df["budget"].sum()
avg_math=stud_df["math_score"].mean()
avg_read=stud_df["reading_score"].mean()


stmathpased_df=stud_df.loc[stud_df["math_score"] >= 70]
pct_math_passed=(stmathpased_df["Student ID"].count()/tot_student)*100

streadpased_df=stud_df.loc[stud_df["reading_score"] >= 70]
streadpased_df
pct_read_passed=(streadpased_df["Student ID"].count()/tot_student)*100
ovall_pass_rt=(pct_math_passed+pct_read_passed)/2

print(school_cnt)
print(tot_student)
print(tot_budget)
print(avg_math)
print(avg_read)
print(stmathpased_df["Student ID"].count())
print(pct_math_passed)
print(streadpased_df["Student ID"].count())
print(pct_read_passed)
print(ovall_pass_rt)

```

    15
    39170
    24649428
    78.98537145774827
    81.87784018381414
    29370
    74.9808526934
    33610
    85.8054633648
    80.3931580291
    


```python

finsum_district_df = pd.DataFrame({"Total Schools": [school_cnt],
                                   "Total Students": [tot_student],
                                   "Total Budget": [tot_budget],
                                   "Average Math Score": [avg_math],
                                   "Average Reading Score": [avg_read],
                                   "% Passing Math":[pct_math_passed],
                                   "% Passing Reading":[pct_read_passed],                                   
                                   "Overall Passing Rate": [ovall_pass_rt]
})
finsum_district_df = finsum_district_df[["Total Schools",
                                   "Total Students",
                                   "Total Budget",
                                   "Average Math Score",
                                   "Average Reading Score",
                                   "% Passing Math",
                                   "% Passing Reading",
                                   "Overall Passing Rate"]]
finsum_district_df = finsum_district_df.round(2)

#################################
##--         OUTPUT         ---##
#################################
finsum_district_df
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
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.99</td>
      <td>81.88</td>
      <td>74.98</td>
      <td>85.81</td>
      <td>80.39</td>
    </tr>
  </tbody>
</table>
</div>




```python
#####################################################################
# 2  Overview table that summarizes key metrics about each school   #
#####################################################################
```


```python
grpbysch1_df=sch_df.groupby(["name"],as_index=False)
grpbysch2_df=stud_df.groupby(["school"],as_index=False)


```


```python
sch_sum1_df=grpbysch1_df.max()
sch_sum1_df.rename(columns={"name":"school","size":"tot_students"},inplace = True)
sch_sum1_df
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
      <th>school</th>
      <th>School ID</th>
      <th>type</th>
      <th>tot_students</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_sum2_df=grpbysch2_df.mean()
sch_sum2_df.rename(columns={"reading_score":"avg_reading_score","math_score":"avg_math_score"},inplace = True)
sch_sum2_df
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
      <th>school</th>
      <th>Student ID</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>9944.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>23060.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>32415.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>23754.5</td>
      <td>84.044699</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>28035.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>6746.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>14871.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>25135.5</td>
      <td>83.955000</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_mrg1_df=pd.merge(sch_sum1_df, sch_sum2_df, on="school")
sch_mrg1_df
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
      <th>school</th>
      <th>School ID</th>
      <th>type</th>
      <th>tot_students</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>9944.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>23060.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>32415.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>23754.5</td>
      <td>84.044699</td>
      <td>83.839917</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>28035.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>6746.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>14871.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>25135.5</td>
      <td>83.955000</td>
      <td>83.682222</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_mrg2_df=pd.merge(stud_df, sch_sum2_df, on="school")
sch_mrg2_df.head()


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
      <th>Student ID_x</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
  </tbody>
</table>
</div>




```python
#schmathpased_df=sch_mrg2_df.loc[sch_mrg2_df["math_score"] >= sch_mrg2_df["avg_math_score"]]
schmathpased_df=sch_mrg2_df.loc[sch_mrg2_df["math_score"] >= 70]
schmathpased_df.head()
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
      <th>Student ID_x</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>94</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>82</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Michael Roth</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>95</td>
      <td>87</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
  </tbody>
</table>
</div>




```python
#schreadpased_df=sch_mrg2_df.loc[sch_mrg2_df["reading_score"] >= sch_mrg2_df["avg_reading_score"]]
schreadpased_df=sch_mrg2_df.loc[sch_mrg2_df["reading_score"] >= 70]
schreadpased_df.head()
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
      <th>Student ID_x</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>94</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>82</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
    </tr>
  </tbody>
</table>
</div>




```python
grpbysch3a_df=schmathpased_df.groupby(["school"],as_index=False)
grpbysch3b_df=schreadpased_df.groupby(["school"],as_index=False)
```


```python
sch_sum3a_df=grpbysch3a_df.count()
sch_sum3a_df.rename(columns={"Student ID_x":"stud_passed_math"},inplace = True)
sch_sum3b_df=grpbysch3b_df.count()
sch_sum3b_df.rename(columns={"Student ID_x":"stud_passed_read"},inplace = True)                             
```


```python
sch_sum3a_df
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
      <th>school</th>
      <th>stud_passed_math</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
      <td>3318</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
      <td>1749</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
      <td>1946</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
      <td>1871</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
      <td>1371</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
      <td>3094</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
      <td>395</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
      <td>1916</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
      <td>3145</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
      <td>910</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
      <td>2654</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
      <td>1653</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
      <td>1525</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
      <td>2143</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
      <td>1680</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_sum3b_df
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
      <th>school</th>
      <th>stud_passed_read</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
      <td>4077</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
      <td>1803</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
      <td>2381</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
      <td>2172</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
      <td>1426</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
      <td>3748</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
      <td>411</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
      <td>2372</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
      <td>3867</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
      <td>923</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
      <td>3208</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
      <td>1688</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
      <td>1591</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
      <td>2204</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
      <td>1739</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_sum3a_df.drop(['name','gender','grade','reading_score','math_score','Student ID_y','avg_reading_score','avg_math_score'],axis=1,inplace=True)
sch_sum3b_df.drop(['name','gender','grade','reading_score','math_score','Student ID_y','avg_reading_score','avg_math_score'],axis=1,inplace=True)
sch_mrg3_df=pd.merge(sch_mrg1_df, sch_sum3a_df, on="school")
sch_mrg4_df=pd.merge(sch_mrg3_df, sch_sum3b_df, on="school")
sch_mrg4_df.head() 
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
      <th>school</th>
      <th>School ID</th>
      <th>type</th>
      <th>tot_students</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
      <th>stud_passed_math</th>
      <th>stud_passed_read</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>3318</td>
      <td>4077</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>1749</td>
      <td>1803</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1946</td>
      <td>2381</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>1871</td>
      <td>2172</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>1371</td>
      <td>1426</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_sum3a_df
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
      <th>school</th>
      <th>stud_passed_math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>3318</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1749</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>1946</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>1871</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1371</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3094</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>395</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>1916</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>3145</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>910</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>2654</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>1653</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>1525</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>2143</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>1680</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_sum3b_df
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
      <th>school</th>
      <th>stud_passed_read</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>4077</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1803</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>2381</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>2172</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1426</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3748</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>411</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>2372</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>3867</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>923</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>3208</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>1688</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>1591</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>2204</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>1739</td>
    </tr>
  </tbody>
</table>
</div>




```python
sch_mrg4_df["% Passing Math"]=(sch_mrg4_df["stud_passed_math"]/sch_mrg4_df["tot_students"])*100
sch_mrg4_df["% Passing Reading"]=(sch_mrg4_df["stud_passed_read"]/sch_mrg4_df["tot_students"])*100
sch_mrg4_df["Overall Passing Rate"]=(sch_mrg4_df["% Passing Math"]+sch_mrg4_df["% Passing Reading"])/2
sch_mrg4_df["Per Student Budget"]=sch_mrg4_df["budget"]/sch_mrg4_df["tot_students"]
sch_mrg4_df
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
      <th>school</th>
      <th>School ID</th>
      <th>type</th>
      <th>tot_students</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
      <th>stud_passed_math</th>
      <th>stud_passed_read</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>7</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>20358.5</td>
      <td>81.033963</td>
      <td>77.048432</td>
      <td>3318</td>
      <td>4077</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>74.306672</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>6</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>16941.5</td>
      <td>83.975780</td>
      <td>83.061895</td>
      <td>1749</td>
      <td>1803</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>95.586652</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>1</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>4391.0</td>
      <td>81.158020</td>
      <td>76.711767</td>
      <td>1946</td>
      <td>2381</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>73.363852</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>13</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>36165.0</td>
      <td>80.746258</td>
      <td>77.102592</td>
      <td>1871</td>
      <td>2172</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>73.804308</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>4</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>12995.5</td>
      <td>83.816757</td>
      <td>83.351499</td>
      <td>1371</td>
      <td>1426</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>95.265668</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>3</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>9944.0</td>
      <td>80.934412</td>
      <td>77.289752</td>
      <td>3094</td>
      <td>3748</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>73.807983</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>8</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>23060.0</td>
      <td>83.814988</td>
      <td>83.803279</td>
      <td>395</td>
      <td>411</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>94.379391</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>1916</td>
      <td>2372</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>73.500171</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>12</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>32415.0</td>
      <td>80.966394</td>
      <td>77.072464</td>
      <td>3145</td>
      <td>3867</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>73.639992</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>9</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>23754.5</td>
      <td>84.044699</td>
      <td>83.839917</td>
      <td>910</td>
      <td>923</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>95.270270</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>11</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>28035.0</td>
      <td>80.744686</td>
      <td>76.842711</td>
      <td>2654</td>
      <td>3208</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>73.293323</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>2</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>6746.0</td>
      <td>83.725724</td>
      <td>83.359455</td>
      <td>1653</td>
      <td>1688</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>94.860875</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>1525</td>
      <td>1591</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>95.290520</td>
      <td>638.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>5</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>14871.0</td>
      <td>83.989488</td>
      <td>83.274201</td>
      <td>2143</td>
      <td>2204</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>95.203679</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>10</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>25135.5</td>
      <td>83.955000</td>
      <td>83.682222</td>
      <td>1680</td>
      <td>1739</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>94.972222</td>
      <td>583.0</td>
    </tr>
  </tbody>
</table>
</div>




```python

finsum_byschool_df=sch_mrg4_df
finsum_byschool_df.rename(columns={"school":"School Name",
                                   "tot_students":"Total Students",
                                   "budget":"Total School Budget",
                                   "avg_reading_score":"Average Reading Score",
                                   "avg_math_score":"Average Math Score"},inplace = True)
finsum_byschool_df.drop(["School ID","type","Student ID","stud_passed_math","stud_passed_read"],axis=1,inplace=True)
finsum_byschool_df = finsum_byschool_df.round(2)

#################################
##--         OUTPUT         ---##
#################################
finsum_byschool_df
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
      <th>School Name</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>4976</td>
      <td>3124928</td>
      <td>81.03</td>
      <td>77.05</td>
      <td>66.68</td>
      <td>81.93</td>
      <td>74.31</td>
      <td>628.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1858</td>
      <td>1081356</td>
      <td>83.98</td>
      <td>83.06</td>
      <td>94.13</td>
      <td>97.04</td>
      <td>95.59</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>2949</td>
      <td>1884411</td>
      <td>81.16</td>
      <td>76.71</td>
      <td>65.99</td>
      <td>80.74</td>
      <td>73.36</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>2739</td>
      <td>1763916</td>
      <td>80.75</td>
      <td>77.10</td>
      <td>68.31</td>
      <td>79.30</td>
      <td>73.80</td>
      <td>644.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1468</td>
      <td>917500</td>
      <td>83.82</td>
      <td>83.35</td>
      <td>93.39</td>
      <td>97.14</td>
      <td>95.27</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Hernandez High School</td>
      <td>4635</td>
      <td>3022020</td>
      <td>80.93</td>
      <td>77.29</td>
      <td>66.75</td>
      <td>80.86</td>
      <td>73.81</td>
      <td>652.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Holden High School</td>
      <td>427</td>
      <td>248087</td>
      <td>83.81</td>
      <td>83.80</td>
      <td>92.51</td>
      <td>96.25</td>
      <td>94.38</td>
      <td>581.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>2917</td>
      <td>1910635</td>
      <td>81.18</td>
      <td>76.63</td>
      <td>65.68</td>
      <td>81.32</td>
      <td>73.50</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>4761</td>
      <td>3094650</td>
      <td>80.97</td>
      <td>77.07</td>
      <td>66.06</td>
      <td>81.22</td>
      <td>73.64</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>962</td>
      <td>585858</td>
      <td>84.04</td>
      <td>83.84</td>
      <td>94.59</td>
      <td>95.95</td>
      <td>95.27</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>3999</td>
      <td>2547363</td>
      <td>80.74</td>
      <td>76.84</td>
      <td>66.37</td>
      <td>80.22</td>
      <td>73.29</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Shelton High School</td>
      <td>1761</td>
      <td>1056600</td>
      <td>83.73</td>
      <td>83.36</td>
      <td>93.87</td>
      <td>95.85</td>
      <td>94.86</td>
      <td>600.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>1635</td>
      <td>1043130</td>
      <td>83.85</td>
      <td>83.42</td>
      <td>93.27</td>
      <td>97.31</td>
      <td>95.29</td>
      <td>638.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>2283</td>
      <td>1319574</td>
      <td>83.99</td>
      <td>83.27</td>
      <td>93.87</td>
      <td>96.54</td>
      <td>95.20</td>
      <td>578.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wright High School</td>
      <td>1800</td>
      <td>1049400</td>
      <td>83.96</td>
      <td>83.68</td>
      <td>93.33</td>
      <td>96.61</td>
      <td>94.97</td>
      <td>583.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
######################################################
# 3     Top 5 Performing Schools (By Passing Rate)   #
######################################################
```


```python

top5_perfschools_df=finsum_byschool_df.sort_values(['Overall Passing Rate'],ascending=False).head(5)
top5_perfschools_df = top5_perfschools_df.round(2)


#################################
##--         OUTPUT         ---##
#################################
top5_perfschools_df
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
      <th>School Name</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1858</td>
      <td>1081356</td>
      <td>83.98</td>
      <td>83.06</td>
      <td>94.13</td>
      <td>97.04</td>
      <td>95.59</td>
      <td>582.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Thomas High School</td>
      <td>1635</td>
      <td>1043130</td>
      <td>83.85</td>
      <td>83.42</td>
      <td>93.27</td>
      <td>97.31</td>
      <td>95.29</td>
      <td>638.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1468</td>
      <td>917500</td>
      <td>83.82</td>
      <td>83.35</td>
      <td>93.39</td>
      <td>97.14</td>
      <td>95.27</td>
      <td>625.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>962</td>
      <td>585858</td>
      <td>84.04</td>
      <td>83.84</td>
      <td>94.59</td>
      <td>95.95</td>
      <td>95.27</td>
      <td>609.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wilson High School</td>
      <td>2283</td>
      <td>1319574</td>
      <td>83.99</td>
      <td>83.27</td>
      <td>93.87</td>
      <td>96.54</td>
      <td>95.20</td>
      <td>578.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
####################################################
# 4  Bottom 5 Performing Schools (By Passing Rate) #
####################################################
```


```python

bott5_perfschools_df=finsum_byschool_df.sort_values(['Overall Passing Rate'],ascending=True).head(5)
bott5_perfschools_df = bott5_perfschools_df.round(2)

#################################
##--         OUTPUT         ---##
#################################
bott5_perfschools_df
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
      <th>School Name</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Average Reading Score</th>
      <th>Average Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
      <th>Per Student Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>Rodriguez High School</td>
      <td>3999</td>
      <td>2547363</td>
      <td>80.74</td>
      <td>76.84</td>
      <td>66.37</td>
      <td>80.22</td>
      <td>73.29</td>
      <td>637.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>2949</td>
      <td>1884411</td>
      <td>81.16</td>
      <td>76.71</td>
      <td>65.99</td>
      <td>80.74</td>
      <td>73.36</td>
      <td>639.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Huang High School</td>
      <td>2917</td>
      <td>1910635</td>
      <td>81.18</td>
      <td>76.63</td>
      <td>65.68</td>
      <td>81.32</td>
      <td>73.50</td>
      <td>655.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Johnson High School</td>
      <td>4761</td>
      <td>3094650</td>
      <td>80.97</td>
      <td>77.07</td>
      <td>66.06</td>
      <td>81.22</td>
      <td>73.64</td>
      <td>650.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>2739</td>
      <td>1763916</td>
      <td>80.75</td>
      <td>77.10</td>
      <td>68.31</td>
      <td>79.30</td>
      <td>73.80</td>
      <td>644.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
###################################
# 5     Math Scores by Grade      #
###################################
```


```python

grpbygrade_df=stud_df.groupby(["school","grade"],as_index=False)
grde_sum_df=grpbygrade_df.mean()
math_grd_sum_df=grde_sum_df[["school","grade","math_score"]]
math_grd_sum_df.rename(columns={"school":"School Name","grade":"Grade","math_score":"Average Math Score"},inplace = True)


#################################
##--         OUTPUT         ---##
#################################
math_grd_sum_df
```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\pandas\core\frame.py:2844: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      **kwargs)
    




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
      <th>School Name</th>
      <th>Grade</th>
      <th>Average Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>10th</td>
      <td>76.996772</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bailey High School</td>
      <td>11th</td>
      <td>77.515588</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bailey High School</td>
      <td>12th</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bailey High School</td>
      <td>9th</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cabrera High School</td>
      <td>10th</td>
      <td>83.154506</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cabrera High School</td>
      <td>11th</td>
      <td>82.765560</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>12th</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Cabrera High School</td>
      <td>9th</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Figueroa High School</td>
      <td>10th</td>
      <td>76.539974</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Figueroa High School</td>
      <td>11th</td>
      <td>76.884344</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Figueroa High School</td>
      <td>12th</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Figueroa High School</td>
      <td>9th</td>
      <td>76.403037</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Ford High School</td>
      <td>10th</td>
      <td>77.672316</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>11th</td>
      <td>76.918058</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Ford High School</td>
      <td>12th</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Ford High School</td>
      <td>9th</td>
      <td>77.361345</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Griffin High School</td>
      <td>10th</td>
      <td>84.229064</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Griffin High School</td>
      <td>11th</td>
      <td>83.842105</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Griffin High School</td>
      <td>12th</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Griffin High School</td>
      <td>9th</td>
      <td>82.044010</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Hernandez High School</td>
      <td>10th</td>
      <td>77.337408</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Hernandez High School</td>
      <td>11th</td>
      <td>77.136029</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Hernandez High School</td>
      <td>12th</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Hernandez High School</td>
      <td>9th</td>
      <td>77.438495</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Holden High School</td>
      <td>10th</td>
      <td>83.429825</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Holden High School</td>
      <td>11th</td>
      <td>85.000000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Holden High School</td>
      <td>12th</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Holden High School</td>
      <td>9th</td>
      <td>83.787402</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Huang High School</td>
      <td>10th</td>
      <td>75.908735</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Huang High School</td>
      <td>11th</td>
      <td>76.446602</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Huang High School</td>
      <td>12th</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Huang High School</td>
      <td>9th</td>
      <td>77.027251</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Johnson High School</td>
      <td>10th</td>
      <td>76.691117</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Johnson High School</td>
      <td>11th</td>
      <td>77.491653</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Johnson High School</td>
      <td>12th</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Johnson High School</td>
      <td>9th</td>
      <td>77.187857</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Pena High School</td>
      <td>10th</td>
      <td>83.372000</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Pena High School</td>
      <td>11th</td>
      <td>84.328125</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Pena High School</td>
      <td>12th</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Pena High School</td>
      <td>9th</td>
      <td>83.625455</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Rodriguez High School</td>
      <td>10th</td>
      <td>76.612500</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Rodriguez High School</td>
      <td>11th</td>
      <td>76.395626</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Rodriguez High School</td>
      <td>12th</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Rodriguez High School</td>
      <td>9th</td>
      <td>76.859966</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Shelton High School</td>
      <td>10th</td>
      <td>82.917411</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Shelton High School</td>
      <td>11th</td>
      <td>83.383495</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Shelton High School</td>
      <td>12th</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Shelton High School</td>
      <td>9th</td>
      <td>83.420755</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Thomas High School</td>
      <td>10th</td>
      <td>83.087886</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Thomas High School</td>
      <td>11th</td>
      <td>83.498795</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Thomas High School</td>
      <td>12th</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Thomas High School</td>
      <td>9th</td>
      <td>83.590022</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Wilson High School</td>
      <td>10th</td>
      <td>83.724422</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Wilson High School</td>
      <td>11th</td>
      <td>83.195326</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Wilson High School</td>
      <td>12th</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Wilson High School</td>
      <td>9th</td>
      <td>83.085578</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Wright High School</td>
      <td>10th</td>
      <td>84.010288</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Wright High School</td>
      <td>11th</td>
      <td>83.836782</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Wright High School</td>
      <td>12th</td>
      <td>83.644986</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Wright High School</td>
      <td>9th</td>
      <td>83.264706</td>
    </tr>
  </tbody>
</table>
</div>




```python
##################################
# 6  Reading Scores by Grade     #
##################################
```


```python

read_grd_sum_df=grde_sum_df[["school","grade","reading_score"]]
read_grd_sum_df.rename(columns={"school":"School Name","grade":"Grade","reading_score":"Average Reading Score"},inplace = True)


#################################
##--         OUTPUT         ---##
#################################
read_grd_sum_df
```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\pandas\core\frame.py:2844: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      **kwargs)
    




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
      <th>School Name</th>
      <th>Grade</th>
      <th>Average Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>10th</td>
      <td>80.907183</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bailey High School</td>
      <td>11th</td>
      <td>80.945643</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bailey High School</td>
      <td>12th</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bailey High School</td>
      <td>9th</td>
      <td>81.303155</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cabrera High School</td>
      <td>10th</td>
      <td>84.253219</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cabrera High School</td>
      <td>11th</td>
      <td>83.788382</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>12th</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Cabrera High School</td>
      <td>9th</td>
      <td>83.676136</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Figueroa High School</td>
      <td>10th</td>
      <td>81.408912</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Figueroa High School</td>
      <td>11th</td>
      <td>80.640339</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Figueroa High School</td>
      <td>12th</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Figueroa High School</td>
      <td>9th</td>
      <td>81.198598</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Ford High School</td>
      <td>10th</td>
      <td>81.262712</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>11th</td>
      <td>80.403642</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Ford High School</td>
      <td>12th</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Ford High School</td>
      <td>9th</td>
      <td>80.632653</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Griffin High School</td>
      <td>10th</td>
      <td>83.706897</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Griffin High School</td>
      <td>11th</td>
      <td>84.288089</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Griffin High School</td>
      <td>12th</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Griffin High School</td>
      <td>9th</td>
      <td>83.369193</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Hernandez High School</td>
      <td>10th</td>
      <td>80.660147</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Hernandez High School</td>
      <td>11th</td>
      <td>81.396140</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Hernandez High School</td>
      <td>12th</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Hernandez High School</td>
      <td>9th</td>
      <td>80.866860</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Holden High School</td>
      <td>10th</td>
      <td>83.324561</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Holden High School</td>
      <td>11th</td>
      <td>83.815534</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Holden High School</td>
      <td>12th</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Holden High School</td>
      <td>9th</td>
      <td>83.677165</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Huang High School</td>
      <td>10th</td>
      <td>81.512386</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Huang High School</td>
      <td>11th</td>
      <td>81.417476</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Huang High School</td>
      <td>12th</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Huang High School</td>
      <td>9th</td>
      <td>81.290284</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Johnson High School</td>
      <td>10th</td>
      <td>80.773431</td>
    </tr>
    <tr>
      <th>33</th>
      <td>Johnson High School</td>
      <td>11th</td>
      <td>80.616027</td>
    </tr>
    <tr>
      <th>34</th>
      <td>Johnson High School</td>
      <td>12th</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Johnson High School</td>
      <td>9th</td>
      <td>81.260714</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Pena High School</td>
      <td>10th</td>
      <td>83.612000</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Pena High School</td>
      <td>11th</td>
      <td>84.335938</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Pena High School</td>
      <td>12th</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Pena High School</td>
      <td>9th</td>
      <td>83.807273</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Rodriguez High School</td>
      <td>10th</td>
      <td>80.629808</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Rodriguez High School</td>
      <td>11th</td>
      <td>80.864811</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Rodriguez High School</td>
      <td>12th</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Rodriguez High School</td>
      <td>9th</td>
      <td>80.993127</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Shelton High School</td>
      <td>10th</td>
      <td>83.441964</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Shelton High School</td>
      <td>11th</td>
      <td>84.373786</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Shelton High School</td>
      <td>12th</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Shelton High School</td>
      <td>9th</td>
      <td>84.122642</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Thomas High School</td>
      <td>10th</td>
      <td>84.254157</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Thomas High School</td>
      <td>11th</td>
      <td>83.585542</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Thomas High School</td>
      <td>12th</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Thomas High School</td>
      <td>9th</td>
      <td>83.728850</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Wilson High School</td>
      <td>10th</td>
      <td>84.021452</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Wilson High School</td>
      <td>11th</td>
      <td>83.764608</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Wilson High School</td>
      <td>12th</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Wilson High School</td>
      <td>9th</td>
      <td>83.939778</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Wright High School</td>
      <td>10th</td>
      <td>83.812757</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Wright High School</td>
      <td>11th</td>
      <td>84.156322</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Wright High School</td>
      <td>12th</td>
      <td>84.073171</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Wright High School</td>
      <td>9th</td>
      <td>83.833333</td>
    </tr>
  </tbody>
</table>
</div>




```python
##################################
# 7  Scores by School Spending   #
##################################
```


```python
schspend_df=sch_df
schspend_df["Avg Spending Range"]=""
schspend_df["Avg Spending Range"][(schspend_df["budget"]/schspend_df["size"]>=0) & (schspend_df["budget"]/schspend_df["size"]<=585)]="0-585"
schspend_df["Avg Spending Range"][(schspend_df["budget"]/schspend_df["size"]>585) & (schspend_df["budget"]/schspend_df["size"]<=615)]="585-615"
schspend_df["Avg Spending Range"][(schspend_df["budget"]/schspend_df["size"]>615) & (schspend_df["budget"]/schspend_df["size"]<=645)]="615-645"
schspend_df["Avg Spending Range"][(schspend_df["budget"]/schspend_df["size"]>645)]="645+"
schspend_df.rename(columns={"name":"school"},inplace=True)


```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    


```python
grpbyspend0_df=schspend_df.groupby(["Avg Spending Range"],as_index=False)
grpbyspend0_sum_df=grpbyspend0_df.sum()
grpbyspend0_sum_df.drop(["School ID","budget"],axis=1,inplace=True)
grpbyspend0_sum_df
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
      <th>Avg Spending Range</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-585</td>
      <td>6368</td>
    </tr>
    <tr>
      <th>1</th>
      <td>585-615</td>
      <td>2723</td>
    </tr>
    <tr>
      <th>2</th>
      <td>615-645</td>
      <td>17766</td>
    </tr>
    <tr>
      <th>3</th>
      <td>645+</td>
      <td>12313</td>
    </tr>
  </tbody>
</table>
</div>




```python
schspend_mrg_df=pd.merge(sch_mrg2_df, schspend_df, on="school")
schspend_mrg_df["MathPassed"]=0
schspend_mrg_df["MathPassed"][(schspend_mrg_df["math_score"])>=70]=1
schspend_mrg_df["ReadPassed"]=0
schspend_mrg_df["ReadPassed"][(schspend_mrg_df["reading_score"])>=70]=1
schspend_mrg_df

```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    




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
      <th>Student ID_x</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Avg Spending Range</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>94</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>82</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Nicole Baker</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>69</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Michael Roth</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>95</td>
      <td>87</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Matthew Greene</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Andrew Alexander</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>70</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Daniel Cooper</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>78</td>
      <td>77</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Brittney Walker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>William Long</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>71</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Tammy Hebert</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>67</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Dr. Jordan Carson</td>
      <td>M</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>88</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Donald Zamora</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>88</td>
      <td>55</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Kimberly Santiago</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>74</td>
      <td>75</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Kevin Stevens</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>69</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Brandi Lyons</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>89</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Lisa Davis</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>91</td>
      <td>89</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Kristen Lopez</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>77</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Kimberly Stewart</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>99</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Christopher Parker</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>81</td>
      <td>68</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Chelsea Griffith</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>73</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Cesar Morris</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>92</td>
      <td>70</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Melanie Decker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>63</td>
      <td>85</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Tracey Oconnor</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>80</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Kelly James</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>73</td>
      <td>55</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Nicole Brown</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>88</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39140</th>
      <td>39140</td>
      <td>Cheyenne Hernandez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>76</td>
      <td>99</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39141</th>
      <td>39141</td>
      <td>Jonathan Sullivan</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>86</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39142</th>
      <td>39142</td>
      <td>Deborah Higgins DDS</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>96</td>
      <td>83</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39143</th>
      <td>39143</td>
      <td>Steven Jackson</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>71</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39144</th>
      <td>39144</td>
      <td>Cristian Webster</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>77</td>
      <td>87</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39145</th>
      <td>39145</td>
      <td>Audrey Fry</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>74</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39146</th>
      <td>39146</td>
      <td>Michael Carroll</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>69</td>
      <td>95</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>39147</th>
      <td>39147</td>
      <td>Raymond Hawkins</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>88</td>
      <td>81</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39148</th>
      <td>39148</td>
      <td>Christopher Wilson</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>89</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39149</th>
      <td>39149</td>
      <td>Glenda Fletcher</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>82</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39150</th>
      <td>39150</td>
      <td>Jennifer Hamilton</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39151</th>
      <td>39151</td>
      <td>Shannon Williams</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>84</td>
      <td>73</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39152</th>
      <td>39152</td>
      <td>Lori Moore</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>98</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>39153</td>
      <td>William Hubbard</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39154</th>
      <td>39154</td>
      <td>Bradley Johnson</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>91</td>
      <td>71</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39155</th>
      <td>39155</td>
      <td>John Brooks</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>92</td>
      <td>98</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39156</th>
      <td>39156</td>
      <td>Stephanie Contreras</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>95</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39157</th>
      <td>39157</td>
      <td>Kristen Gonzalez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>94</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39158</th>
      <td>39158</td>
      <td>Kari Holloway</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>87</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39159</th>
      <td>39159</td>
      <td>Kimberly Cabrera</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>85</td>
      <td>72</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39160</th>
      <td>39160</td>
      <td>Katie Weaver</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>86</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39161</th>
      <td>39161</td>
      <td>April Reyes</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>70</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39162</th>
      <td>39162</td>
      <td>Derek Weeks</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>77</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39163</th>
      <td>39163</td>
      <td>John Reese</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>90</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39164</th>
      <td>39164</td>
      <td>Joseph Anthony</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>97</td>
      <td>76</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39165</th>
      <td>39165</td>
      <td>Donna Howard</td>
      <td>F</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39166</th>
      <td>39166</td>
      <td>Dawn Bell</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>70</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39167</th>
      <td>39167</td>
      <td>Rebecca Tanner</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>73</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39168</th>
      <td>39168</td>
      <td>Desiree Kidd</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>39169</td>
      <td>Carolyn Jackson</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>39170 rows × 17 columns</p>
</div>




```python
grpbyspend1_df=schspend_mrg_df.groupby(["Avg Spending Range"],as_index=False)
grpbyspend1_mean_df=grpbyspend1_df.mean()

grpbyspend1_mean_df.drop(["Student ID_x",
"Student ID_y",
"avg_reading_score",
"avg_math_score",
"School ID",
"size",
"budget",
"MathPassed",
"ReadPassed"],axis=1,inplace=True)
grpbyspend1_mean_df.rename(columns={"reading_score":"Avg Reading Score","math_score":"Avg Math Score"},inplace=True)

grpbyspend1_mean_df

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
      <th>Avg Spending Range</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-585</td>
      <td>83.964039</td>
      <td>83.363065</td>
    </tr>
    <tr>
      <th>1</th>
      <td>585-615</td>
      <td>83.838414</td>
      <td>83.529196</td>
    </tr>
    <tr>
      <th>2</th>
      <td>615-645</td>
      <td>81.434088</td>
      <td>78.061635</td>
    </tr>
    <tr>
      <th>3</th>
      <td>645+</td>
      <td>81.005604</td>
      <td>77.049297</td>
    </tr>
  </tbody>
</table>
</div>




```python
grpbyspend1_sum_df=grpbyspend1_df.sum()
grpbyspend1_sum_df.drop(["Student ID_x",
"reading_score",
"math_score",
"Student ID_y",
"avg_reading_score",
"avg_math_score",
"School ID",
"size",
"budget"],axis=1,inplace=True)

grpbyspend1_sum_df

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
      <th>Avg Spending Range</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-585</td>
      <td>5967</td>
      <td>6157</td>
    </tr>
    <tr>
      <th>1</th>
      <td>585-615</td>
      <td>2563</td>
      <td>2611</td>
    </tr>
    <tr>
      <th>2</th>
      <td>615-645</td>
      <td>12685</td>
      <td>14855</td>
    </tr>
    <tr>
      <th>3</th>
      <td>645+</td>
      <td>8155</td>
      <td>9987</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
spendmrg1_df=pd.merge(grpbyspend0_sum_df, grpbyspend1_mean_df, on="Avg Spending Range")
spendmrg1_df
spendmrg2_df=pd.merge(spendmrg1_df, grpbyspend1_sum_df, on="Avg Spending Range")
spendmrg2_df
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
      <th>Avg Spending Range</th>
      <th>size</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-585</td>
      <td>6368</td>
      <td>83.964039</td>
      <td>83.363065</td>
      <td>5967</td>
      <td>6157</td>
    </tr>
    <tr>
      <th>1</th>
      <td>585-615</td>
      <td>2723</td>
      <td>83.838414</td>
      <td>83.529196</td>
      <td>2563</td>
      <td>2611</td>
    </tr>
    <tr>
      <th>2</th>
      <td>615-645</td>
      <td>17766</td>
      <td>81.434088</td>
      <td>78.061635</td>
      <td>12685</td>
      <td>14855</td>
    </tr>
    <tr>
      <th>3</th>
      <td>645+</td>
      <td>12313</td>
      <td>81.005604</td>
      <td>77.049297</td>
      <td>8155</td>
      <td>9987</td>
    </tr>
  </tbody>
</table>
</div>




```python

spendmrg2_df["% Passing Math"]=(spendmrg2_df["MathPassed"]/spendmrg2_df["size"])*100
spendmrg2_df["% Passing Reading"]=(spendmrg2_df["ReadPassed"]/spendmrg2_df["size"])*100
spendmrg2_df["Overall Passing Rate"]=(spendmrg2_df["% Passing Math"]+spendmrg2_df["% Passing Reading"])/2
spendmrg2_df.rename(columns={"size":"Total Students"},inplace=True)
score_by_spend_df=spendmrg2_df
score_by_spend_df.drop(["Total Students","MathPassed","ReadPassed"],axis=1,inplace=True)


#################################
##--         OUTPUT         ---##
#################################
score_by_spend_df
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
      <th>Avg Spending Range</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0-585</td>
      <td>83.964039</td>
      <td>83.363065</td>
      <td>93.702889</td>
      <td>96.686558</td>
      <td>95.194724</td>
    </tr>
    <tr>
      <th>1</th>
      <td>585-615</td>
      <td>83.838414</td>
      <td>83.529196</td>
      <td>94.124128</td>
      <td>95.886889</td>
      <td>95.005509</td>
    </tr>
    <tr>
      <th>2</th>
      <td>615-645</td>
      <td>81.434088</td>
      <td>78.061635</td>
      <td>71.400428</td>
      <td>83.614770</td>
      <td>77.507599</td>
    </tr>
    <tr>
      <th>3</th>
      <td>645+</td>
      <td>81.005604</td>
      <td>77.049297</td>
      <td>66.230813</td>
      <td>81.109397</td>
      <td>73.670105</td>
    </tr>
  </tbody>
</table>
</div>




```python
#########################################
# 8   Scores by School Size             #
#########################################
```


```python
schsize_df=sch_df
schsize_df["School Size"]=""
schsize_df["School Size"][(schsize_df["size"]>=0) & (schsize_df["size"]<=1000)]="Small(<1000)"
schsize_df["School Size"][(schsize_df["size"]>=1000) & (schsize_df["size"]<=2000)]="Medium(1000-2000)"
schsize_df["School Size"][(schsize_df["size"]>=2000) & (schsize_df["size"]<=5000)]="Large(2000-5000)"
schsize_df.rename(columns={"name":"school"},inplace=True)
schsize_df
```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    




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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Avg Spending Range</th>
      <th>School Size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>585-615</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>0-585</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>0-585</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>0-585</td>
      <td>Small(&lt;1000)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>585-615</td>
      <td>Small(&lt;1000)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>0-585</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
    </tr>
  </tbody>
</table>
</div>




```python
grpbysize0_df=schsize_df.groupby(["School Size"],as_index=False)
grpbysize0_sum_df=grpbysize0_df.sum()
grpbysize0_sum_df.drop(["School ID","budget"],axis=1,inplace=True)
grpbysize0_sum_df
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
      <th>School Size</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large(2000-5000)</td>
      <td>29259</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium(1000-2000)</td>
      <td>8522</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Small(&lt;1000)</td>
      <td>1389</td>
    </tr>
  </tbody>
</table>
</div>




```python
schsize_mrg_df=pd.merge(sch_mrg2_df, schsize_df, on="school")
schsize_mrg_df["MathPassed"]=0
schsize_mrg_df["MathPassed"][(schsize_mrg_df["math_score"])>=70]=1
schsize_mrg_df["ReadPassed"]=0
schsize_mrg_df["ReadPassed"][(schsize_mrg_df["reading_score"])>=70]=1
schsize_mrg_df
```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    




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
      <th>Student ID_x</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Avg Spending Range</th>
      <th>School Size</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>94</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>82</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Nicole Baker</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>69</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Michael Roth</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>95</td>
      <td>87</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Matthew Greene</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Andrew Alexander</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>70</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Daniel Cooper</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>78</td>
      <td>77</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Brittney Walker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>William Long</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>71</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Tammy Hebert</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>67</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Dr. Jordan Carson</td>
      <td>M</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>88</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Donald Zamora</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>88</td>
      <td>55</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Kimberly Santiago</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>74</td>
      <td>75</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Kevin Stevens</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>69</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Brandi Lyons</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>89</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Lisa Davis</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>91</td>
      <td>89</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Kristen Lopez</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>77</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Kimberly Stewart</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>99</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Christopher Parker</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>81</td>
      <td>68</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Chelsea Griffith</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>73</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Cesar Morris</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>92</td>
      <td>70</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Melanie Decker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>63</td>
      <td>85</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Tracey Oconnor</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>80</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Kelly James</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>73</td>
      <td>55</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Nicole Brown</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>88</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39140</th>
      <td>39140</td>
      <td>Cheyenne Hernandez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>76</td>
      <td>99</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39141</th>
      <td>39141</td>
      <td>Jonathan Sullivan</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>86</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39142</th>
      <td>39142</td>
      <td>Deborah Higgins DDS</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>96</td>
      <td>83</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39143</th>
      <td>39143</td>
      <td>Steven Jackson</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>71</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39144</th>
      <td>39144</td>
      <td>Cristian Webster</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>77</td>
      <td>87</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39145</th>
      <td>39145</td>
      <td>Audrey Fry</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>74</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39146</th>
      <td>39146</td>
      <td>Michael Carroll</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>69</td>
      <td>95</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>39147</th>
      <td>39147</td>
      <td>Raymond Hawkins</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>88</td>
      <td>81</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39148</th>
      <td>39148</td>
      <td>Christopher Wilson</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>89</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39149</th>
      <td>39149</td>
      <td>Glenda Fletcher</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>82</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39150</th>
      <td>39150</td>
      <td>Jennifer Hamilton</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39151</th>
      <td>39151</td>
      <td>Shannon Williams</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>84</td>
      <td>73</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39152</th>
      <td>39152</td>
      <td>Lori Moore</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>98</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>39153</td>
      <td>William Hubbard</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39154</th>
      <td>39154</td>
      <td>Bradley Johnson</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>91</td>
      <td>71</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39155</th>
      <td>39155</td>
      <td>John Brooks</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>92</td>
      <td>98</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39156</th>
      <td>39156</td>
      <td>Stephanie Contreras</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>95</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39157</th>
      <td>39157</td>
      <td>Kristen Gonzalez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>94</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39158</th>
      <td>39158</td>
      <td>Kari Holloway</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>87</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39159</th>
      <td>39159</td>
      <td>Kimberly Cabrera</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>85</td>
      <td>72</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39160</th>
      <td>39160</td>
      <td>Katie Weaver</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>86</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39161</th>
      <td>39161</td>
      <td>April Reyes</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>70</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39162</th>
      <td>39162</td>
      <td>Derek Weeks</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>77</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39163</th>
      <td>39163</td>
      <td>John Reese</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>90</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39164</th>
      <td>39164</td>
      <td>Joseph Anthony</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>97</td>
      <td>76</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39165</th>
      <td>39165</td>
      <td>Donna Howard</td>
      <td>F</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39166</th>
      <td>39166</td>
      <td>Dawn Bell</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>70</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39167</th>
      <td>39167</td>
      <td>Rebecca Tanner</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>73</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39168</th>
      <td>39168</td>
      <td>Desiree Kidd</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>39169</td>
      <td>Carolyn Jackson</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>39170 rows × 18 columns</p>
</div>




```python
grpbysize1_df=schsize_mrg_df.groupby(["School Size"],as_index=False)
grpbysize1_mean_df=grpbysize1_df.mean()

grpbysize1_mean_df.drop(["Student ID_x",
"Student ID_y",
"avg_reading_score",
"avg_math_score",
"School ID",
"size",
"budget",
"MathPassed",
"ReadPassed"],axis=1,inplace=True)
grpbysize1_mean_df.rename(columns={"reading_score":"Avg Reading Score","math_score":"Avg Math Score"},inplace=True)

grpbysize1_mean_df
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
      <th>School Size</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large(2000-5000)</td>
      <td>81.198674</td>
      <td>77.477597</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium(1000-2000)</td>
      <td>83.867989</td>
      <td>83.372682</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Small(&lt;1000)</td>
      <td>83.974082</td>
      <td>83.828654</td>
    </tr>
  </tbody>
</table>
</div>




```python
grpbysize1_sum_df=grpbysize1_df.sum()
grpbysize1_sum_df.drop(["Student ID_x",
"reading_score",
"math_score",
"Student ID_y",
"avg_reading_score",
"avg_math_score",
"School ID",
"size",
"budget"],axis=1,inplace=True)

grpbysize1_sum_df

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
      <th>School Size</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large(2000-5000)</td>
      <td>20087</td>
      <td>24029</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium(1000-2000)</td>
      <td>7978</td>
      <td>8247</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Small(&lt;1000)</td>
      <td>1305</td>
      <td>1334</td>
    </tr>
  </tbody>
</table>
</div>




```python
sizemrg1_df=pd.merge(grpbysize0_sum_df, grpbysize1_mean_df, on="School Size")
sizemrg1_df
sizemrg2_df=pd.merge(sizemrg1_df, grpbysize1_sum_df, on="School Size")
sizemrg2_df
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
      <th>School Size</th>
      <th>size</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large(2000-5000)</td>
      <td>29259</td>
      <td>81.198674</td>
      <td>77.477597</td>
      <td>20087</td>
      <td>24029</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium(1000-2000)</td>
      <td>8522</td>
      <td>83.867989</td>
      <td>83.372682</td>
      <td>7978</td>
      <td>8247</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Small(&lt;1000)</td>
      <td>1389</td>
      <td>83.974082</td>
      <td>83.828654</td>
      <td>1305</td>
      <td>1334</td>
    </tr>
  </tbody>
</table>
</div>




```python

sizemrg2_df["% Passing Math"]=(sizemrg2_df["MathPassed"]/sizemrg2_df["size"])*100
sizemrg2_df["% Passing Reading"]=(sizemrg2_df["ReadPassed"]/sizemrg2_df["size"])*100
sizemrg2_df["Overall Passing Rate"]=(sizemrg2_df["% Passing Math"]+sizemrg2_df["% Passing Reading"])/2
sizemrg2_df.rename(columns={"size":"Total Students"},inplace=True)
score_by_size_df=sizemrg2_df
score_by_size_df.drop(["Total Students","MathPassed","ReadPassed"],axis=1,inplace=True)


#################################
##--         OUTPUT         ---##
#################################
score_by_size_df
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
      <th>School Size</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Large(2000-5000)</td>
      <td>81.198674</td>
      <td>77.477597</td>
      <td>68.652380</td>
      <td>82.125158</td>
      <td>75.388769</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Medium(1000-2000)</td>
      <td>83.867989</td>
      <td>83.372682</td>
      <td>93.616522</td>
      <td>96.773058</td>
      <td>95.194790</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Small(&lt;1000)</td>
      <td>83.974082</td>
      <td>83.828654</td>
      <td>93.952484</td>
      <td>96.040317</td>
      <td>94.996400</td>
    </tr>
  </tbody>
</table>
</div>




```python
############################
# 9  Scores by School Type #
############################
```


```python
schtype_df=sch_df
schtype_df.rename(columns={"name":"school"},inplace=True)
schtype_df
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
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Avg Spending Range</th>
      <th>School Size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>585-615</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>1319574</td>
      <td>0-585</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>1081356</td>
      <td>0-585</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>3124928</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>248087</td>
      <td>0-585</td>
      <td>Small(&lt;1000)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>585858</td>
      <td>585-615</td>
      <td>Small(&lt;1000)</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>1049400</td>
      <td>0-585</td>
      <td>Medium(1000-2000)</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>2547363</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>3094650</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>1763916</td>
      <td>615-645</td>
      <td>Large(2000-5000)</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
    </tr>
  </tbody>
</table>
</div>




```python
grpbytype0_df=schtype_df.groupby(["type"],as_index=False)
grpbytype0_sum_df=grpbytype0_df.sum()
grpbytype0_sum_df.drop(["School ID","budget"],axis=1,inplace=True)
grpbytype0_sum_df
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
      <th>type</th>
      <th>size</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Charter</td>
      <td>12194</td>
    </tr>
    <tr>
      <th>1</th>
      <td>District</td>
      <td>26976</td>
    </tr>
  </tbody>
</table>
</div>




```python
schtype_mrg_df=pd.merge(sch_mrg2_df, schtype_df, on="school")
schtype_mrg_df["MathPassed"]=0
schtype_mrg_df["MathPassed"][(schtype_mrg_df["math_score"])>=70]=1
schtype_mrg_df["ReadPassed"]=0
schtype_mrg_df["ReadPassed"][(schtype_mrg_df["reading_score"])>=70]=1
schtype_mrg_df
```

    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      app.launch_new_instance()
    C:\Users\fervi\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:5: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    




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
      <th>Student ID_x</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>Student ID_y</th>
      <th>avg_reading_score</th>
      <th>avg_math_score</th>
      <th>School ID</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Avg Spending Range</th>
      <th>School Size</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>94</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>82</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Nicole Baker</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>69</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Michael Roth</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>95</td>
      <td>87</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Matthew Greene</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>96</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>Andrew Alexander</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>70</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>Daniel Cooper</td>
      <td>M</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>78</td>
      <td>77</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>Brittney Walker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>William Long</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>71</td>
      <td>79</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>Tammy Hebert</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>67</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>Dr. Jordan Carson</td>
      <td>M</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>88</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>Donald Zamora</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>88</td>
      <td>55</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>Kimberly Santiago</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>74</td>
      <td>75</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>Kevin Stevens</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>64</td>
      <td>69</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>Brandi Lyons</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>89</td>
      <td>80</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>Lisa Davis</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>91</td>
      <td>89</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>Kristen Lopez</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>77</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>Kimberly Stewart</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>99</td>
      <td>84</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>Christopher Parker</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>81</td>
      <td>68</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>Chelsea Griffith</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>85</td>
      <td>73</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>25</td>
      <td>Cesar Morris</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>92</td>
      <td>70</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>26</td>
      <td>Melanie Decker</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>63</td>
      <td>85</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>27</td>
      <td>Tracey Oconnor</td>
      <td>F</td>
      <td>10th</td>
      <td>Huang High School</td>
      <td>80</td>
      <td>58</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>28</th>
      <td>28</td>
      <td>Kelly James</td>
      <td>F</td>
      <td>11th</td>
      <td>Huang High School</td>
      <td>73</td>
      <td>55</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>29</th>
      <td>29</td>
      <td>Nicole Brown</td>
      <td>F</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>88</td>
      <td>1458.0</td>
      <td>81.182722</td>
      <td>76.629414</td>
      <td>0</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>645+</td>
      <td>Large(2000-5000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>39140</th>
      <td>39140</td>
      <td>Cheyenne Hernandez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>76</td>
      <td>99</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39141</th>
      <td>39141</td>
      <td>Jonathan Sullivan</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>86</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39142</th>
      <td>39142</td>
      <td>Deborah Higgins DDS</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>96</td>
      <td>83</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39143</th>
      <td>39143</td>
      <td>Steven Jackson</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>71</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39144</th>
      <td>39144</td>
      <td>Cristian Webster</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>77</td>
      <td>87</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39145</th>
      <td>39145</td>
      <td>Audrey Fry</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>74</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39146</th>
      <td>39146</td>
      <td>Michael Carroll</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>69</td>
      <td>95</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>39147</th>
      <td>39147</td>
      <td>Raymond Hawkins</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>88</td>
      <td>81</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39148</th>
      <td>39148</td>
      <td>Christopher Wilson</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>89</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39149</th>
      <td>39149</td>
      <td>Glenda Fletcher</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>82</td>
      <td>93</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39150</th>
      <td>39150</td>
      <td>Jennifer Hamilton</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39151</th>
      <td>39151</td>
      <td>Shannon Williams</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>84</td>
      <td>73</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39152</th>
      <td>39152</td>
      <td>Lori Moore</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>98</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39153</th>
      <td>39153</td>
      <td>William Hubbard</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>80</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39154</th>
      <td>39154</td>
      <td>Bradley Johnson</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>91</td>
      <td>71</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39155</th>
      <td>39155</td>
      <td>John Brooks</td>
      <td>M</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>92</td>
      <td>98</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39156</th>
      <td>39156</td>
      <td>Stephanie Contreras</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>95</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39157</th>
      <td>39157</td>
      <td>Kristen Gonzalez</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>79</td>
      <td>94</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39158</th>
      <td>39158</td>
      <td>Kari Holloway</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>87</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39159</th>
      <td>39159</td>
      <td>Kimberly Cabrera</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>85</td>
      <td>72</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39160</th>
      <td>39160</td>
      <td>Katie Weaver</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>89</td>
      <td>86</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39161</th>
      <td>39161</td>
      <td>April Reyes</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>70</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39162</th>
      <td>39162</td>
      <td>Derek Weeks</td>
      <td>M</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>94</td>
      <td>77</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39163</th>
      <td>39163</td>
      <td>John Reese</td>
      <td>M</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>90</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39164</th>
      <td>39164</td>
      <td>Joseph Anthony</td>
      <td>M</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>97</td>
      <td>76</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39165</th>
      <td>39165</td>
      <td>Donna Howard</td>
      <td>F</td>
      <td>12th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39166</th>
      <td>39166</td>
      <td>Dawn Bell</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>70</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39167</th>
      <td>39167</td>
      <td>Rebecca Tanner</td>
      <td>F</td>
      <td>9th</td>
      <td>Thomas High School</td>
      <td>73</td>
      <td>84</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39168</th>
      <td>39168</td>
      <td>Desiree Kidd</td>
      <td>F</td>
      <td>10th</td>
      <td>Thomas High School</td>
      <td>99</td>
      <td>90</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>39169</th>
      <td>39169</td>
      <td>Carolyn Jackson</td>
      <td>F</td>
      <td>11th</td>
      <td>Thomas High School</td>
      <td>95</td>
      <td>75</td>
      <td>38352.0</td>
      <td>83.848930</td>
      <td>83.418349</td>
      <td>14</td>
      <td>Charter</td>
      <td>1635</td>
      <td>1043130</td>
      <td>615-645</td>
      <td>Medium(1000-2000)</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>39170 rows × 18 columns</p>
</div>




```python
grpbytype1_df=schtype_mrg_df.groupby(["type"],as_index=False)
grpbytype1_mean_df=grpbytype1_df.mean()

grpbytype1_mean_df.drop(["Student ID_x",
"Student ID_y",
"avg_reading_score",
"avg_math_score",
"School ID",
"size",
"budget",
"MathPassed",
"ReadPassed"],axis=1,inplace=True)
grpbytype1_mean_df.rename(columns={"reading_score":"Avg Reading Score","math_score":"Avg Math Score"},inplace=True)

grpbytype1_mean_df
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
      <th>type</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Charter</td>
      <td>83.902821</td>
      <td>83.406183</td>
    </tr>
    <tr>
      <th>1</th>
      <td>District</td>
      <td>80.962485</td>
      <td>76.987026</td>
    </tr>
  </tbody>
</table>
</div>




```python
grpbytype1_sum_df=grpbytype1_df.sum()
grpbytype1_sum_df.drop(["Student ID_x",
"reading_score",
"math_score",
"Student ID_y",
"avg_reading_score",
"avg_math_score",
"School ID",
"size",
"budget"],axis=1,inplace=True)

grpbytype1_sum_df
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
      <th>type</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Charter</td>
      <td>11426</td>
      <td>11785</td>
    </tr>
    <tr>
      <th>1</th>
      <td>District</td>
      <td>17944</td>
      <td>21825</td>
    </tr>
  </tbody>
</table>
</div>




```python

typemrg1_df=pd.merge(grpbytype0_sum_df, grpbytype1_mean_df, on="type")
typemrg1_df
typemrg2_df=pd.merge(typemrg1_df, grpbytype1_sum_df, on="type")
typemrg2_df

typemrg2_df["% Passing Math"]=(typemrg2_df["MathPassed"]/typemrg2_df["size"])*100
typemrg2_df["% Passing Reading"]=(typemrg2_df["ReadPassed"]/typemrg2_df["size"])*100
typemrg2_df["Overall Passing Rate"]=(typemrg2_df["% Passing Math"]+typemrg2_df["% Passing Reading"])/2
typemrg2_df.rename(columns={"size":"Total Students"},inplace=True)
score_by_type_df=typemrg2_df

#################################
##--         OUTPUT         ---##
#################################
score_by_type_df
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
      <th>type</th>
      <th>Total Students</th>
      <th>Avg Reading Score</th>
      <th>Avg Math Score</th>
      <th>MathPassed</th>
      <th>ReadPassed</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Charter</td>
      <td>12194</td>
      <td>83.902821</td>
      <td>83.406183</td>
      <td>11426</td>
      <td>11785</td>
      <td>93.701821</td>
      <td>96.645891</td>
      <td>95.173856</td>
    </tr>
    <tr>
      <th>1</th>
      <td>District</td>
      <td>26976</td>
      <td>80.962485</td>
      <td>76.987026</td>
      <td>17944</td>
      <td>21825</td>
      <td>66.518387</td>
      <td>80.905249</td>
      <td>73.711818</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
