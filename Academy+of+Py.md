

```python
# Dependencies
import pandas as pd

# Load CSV
csv_path1 = "raw_data/schools_complete.csv"
csv_path2 = "raw_data/students_complete.csv"

# Read school_data with Pandas
school_data_df = pd.read_csv(csv_path1, low_memory = False)
school_data_df.head()

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
# Read student_data with Pandas
student_data_df = pd.read_csv(csv_path2, low_memory = False)
student_data_df.head()
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



# District Summary


```python
#**District Summary**

# Create a high level snapshot (in table form) of the district's key metrics, including:

# Total Schools
total_schools = len(school_data_df)
#print("Total Schools: ", total_schools)

# Total Students
total_students = school_data_df["size"].sum()
#print("Total Students: ", total_students)

# Total Budget
total_budget = school_data_df["budget"].sum()
#print("Total budget: ", total_budget)

# Average Math Score
avg_math_sc = round(student_data_df["math_score"].mean(), 6)
#print("Average Math Score: ", avg_math_sc)

# Average Reading Score
avg_rdg_sc = round(student_data_df["reading_score"].mean(), 6)
#print("Average Reading Score: ", avg_rdg_sc)

# % Passing Math (assuming score > 70 is pass)
pass_math_df = student_data_df.loc[student_data_df["math_score"] > 70 ,:]
pass_math_count = len(pass_math_df)
percent_pass_math = (pass_math_count/total_students) * 100
#print("% Passing Math: ", percent_pass_math)

# % Passing Reading
pass_rdg_df = student_data_df.loc[student_data_df["reading_score"] > 70 ,:]
pass_rdg_count = len(pass_rdg_df)
percent_pass_rdg = (pass_rdg_count/total_students) * 100
#print("% Passing Reading: ", percent_pass_rdg)

# Overall Passing Rate (Average of the above two)
overall_pass_rate = (percent_pass_math + percent_pass_rdg) / 2
#print("Overall Passing Rate", overall_pass_rate)

# Create a high level snapshot (in table form)
print("DISTRICT SUMMARY: ")
dist_summary_df = pd.DataFrame({"Total Schools":[total_schools], "Total Students": [total_students], \
                                "Total Budget": [total_budget], "Average Math Score": [avg_math_sc], \
                               "Average Reading Score": [avg_rdg_sc], "% Passing Math": [percent_pass_math], \
                                "% Passing Reading":[percent_pass_rdg], "% Overall Passing Rate": [overall_pass_rate]}, \
                              columns = ["Total Schools", "Total Students", "Total Budget", "Average Math Score", \
                                        "Average Reading Score", "% Passing Math", "% Passing Reading", "% Overall Passing Rate"])


dist_summary_df


```

    DISTRICT SUMMARY: 
    




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
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39170</td>
      <td>24649428</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>72.392137</td>
      <td>82.971662</td>
      <td>77.681899</td>
    </tr>
  </tbody>
</table>
</div>




```python
school_data_df.set_index("name", inplace=True)
# school_data_df.head()
```


```python
student_data_df.set_index("school", inplace=True)
# student_data_df.head()
```

# School Summary


```python
#**School Summary**
# Create an overview table that summarizes key metrics about each school, including:

# School Type
school_type_df = school_data_df["type"]
#print(school_type_df.head())

# Total Students
# Total School Budget
total_school_budget_df = school_data_df["budget"]
#print(total_school_budget_df.head())

# Per Student Budget
per_student_budget_df = school_data_df["budget"]/school_data_df["size"]
#print(per_student_budget_df.head())

# Average Math Score
avg_math_sc_df = student_data_df.groupby('school')['math_score'].mean()
#print(avg_math_sc_df.head())

# Average Reading Score
avg_rdg_sc_df = student_data_df.groupby('school')['reading_score'].mean()
# print(avg_rdg_sc_df.head())

# % Passing Math
    # total students by school
student_count_in_school_df = student_data_df.groupby('school')['math_score'].count()
    # all passing math (assuming pass >70)
passing_math_all_df = student_data_df.loc[student_data_df["math_score"] > 70 ,:]
    # grouping and counting all passing math by school
passing_math_byschool_df = passing_math_all_df.groupby('school')["name"].count()
    # calculation %
percent_passing_math_df = (passing_math_byschool_df/student_count_in_school_df)*100
# print(percent_passing_math_df.head())

# % Passing Reading
    # total students by school
student_count_in_school_df = student_data_df.groupby('school')['reading_score'].count()
    # all passing Reading (assuming pass >70)
passing_rdg_all_df = student_data_df.loc[student_data_df["reading_score"] > 70 ,:]
    # grouping and counting all passing reading by school
passing_rdg_byschool_df = passing_rdg_all_df.groupby('school')["name"].count()
    # calculation %
percent_passing_rdg_df = (passing_rdg_byschool_df/student_count_in_school_df)*100
# print(percent_passing_rdg_df.head())

# Overall Passing Rate (Average of the above two)
overall_passing_rate_df = (percent_passing_math_df + percent_passing_rdg_df)/2
#print(overall_passing_rate_df.head())

# Create an overview table that summarizes key metrics about each school
print("SCHOOL SUMMARY: ")
school_summary_df = pd.DataFrame({"School Type":school_type_df, "Total Students": student_count_in_school_df, \
                               "Total School Budget": total_school_budget_df, "Per Student Budget": per_student_budget_df, \
                                "Average Math Score": avg_math_sc_df, "Average Reading Score": avg_rdg_sc_df, \
                                "% Passing Math":percent_passing_math_df, "% Passing Reading": percent_passing_rdg_df, \
                                 "% Overall Passing Rate":overall_passing_rate_df},\
                                 columns = ["School Type", "Total Students", "Total School Budget", "Per Student Budget", \
                                            "Average Math Score", "Average Reading Score", "% Passing Math", \
                                            "% Passing Reading", "% Overall Passing Rate"])

# formatting
# Total Students is not being formatted since cant use it in calculations if we add a ,
# school_summary_df["Total Students"] = school_summary_df["Total Students"].map('{:,}'.format)

school_summary_df["Total School Budget"] = school_summary_df["Total School Budget"].map('{:,}'.format)
school_summary_df["Per Student Budget"] = school_summary_df["Per Student Budget"].map('{:.2f}'.format)

school_summary_df



```

    SCHOOL SUMMARY: 
    




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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>3,124,928</td>
      <td>628.00</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>64.630225</td>
      <td>79.300643</td>
      <td>71.965434</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1,081,356</td>
      <td>582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>89.558665</td>
      <td>93.864370</td>
      <td>91.711518</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1,884,411</td>
      <td>639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>63.750424</td>
      <td>78.433367</td>
      <td>71.091896</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>1,763,916</td>
      <td>644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>65.753925</td>
      <td>77.510040</td>
      <td>71.631982</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>917,500</td>
      <td>625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>89.713896</td>
      <td>93.392371</td>
      <td>91.553134</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3,022,020</td>
      <td>652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>64.746494</td>
      <td>78.187702</td>
      <td>71.467098</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248,087</td>
      <td>581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>90.632319</td>
      <td>92.740047</td>
      <td>91.686183</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1,910,635</td>
      <td>655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>63.318478</td>
      <td>78.813850</td>
      <td>71.066164</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3,094,650</td>
      <td>650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>63.852132</td>
      <td>78.281874</td>
      <td>71.067003</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585,858</td>
      <td>609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>91.683992</td>
      <td>92.203742</td>
      <td>91.943867</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2,547,363</td>
      <td>637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>64.066017</td>
      <td>77.744436</td>
      <td>70.905226</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>1,056,600</td>
      <td>600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>89.892107</td>
      <td>92.617831</td>
      <td>91.254969</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>1,043,130</td>
      <td>638.00</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>90.214067</td>
      <td>92.905199</td>
      <td>91.559633</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1,319,574</td>
      <td>578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>90.932983</td>
      <td>93.254490</td>
      <td>92.093736</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1,049,400</td>
      <td>583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>90.277778</td>
      <td>93.444444</td>
      <td>91.861111</td>
    </tr>
  </tbody>
</table>
</div>



# Top Performing Schools (by Passing Rate)


```python
#**Top Performing Schools (By Passing Rate)**

#Create a table that highlights the top 5 performing schools based on Overall Passing Rate. Include:
# School Name
# School Type
# Total Students
# Total School Budget
# Per Student Budget
# Average Math Score
# Average Reading Score
# % Passing Math
# % Passing Reading
# Overall Passing Rate (Average of the above two)
print("Top 5 Performing Schools (By Passing Rate): ")
top_performing_schools_df = school_summary_df.sort_values('% Overall Passing Rate', ascending = False)
top5_performing_schools_df = top_performing_schools_df.head(5)
top5_performing_schools_df

```

    Top 5 Performing Schools (By Passing Rate): 
    




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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>1,319,574</td>
      <td>578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>90.932983</td>
      <td>93.254490</td>
      <td>92.093736</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>585,858</td>
      <td>609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>91.683992</td>
      <td>92.203742</td>
      <td>91.943867</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>1,049,400</td>
      <td>583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>90.277778</td>
      <td>93.444444</td>
      <td>91.861111</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>1,081,356</td>
      <td>582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>89.558665</td>
      <td>93.864370</td>
      <td>91.711518</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>248,087</td>
      <td>581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>90.632319</td>
      <td>92.740047</td>
      <td>91.686183</td>
    </tr>
  </tbody>
</table>
</div>



# Bottom 5 Performing Schools (By Passing Rate)


```python
# Create a table that highlights the bottom 5 performing schools based on Overall Passing Rate. 
# Include all of the same metrics as above.
print("Bottom 5 Performing Schools (By Passing Rate): ")
bottom_performing_schools_df = school_summary_df.sort_values('% Overall Passing Rate')
bottom5_performing_schools_df = bottom_performing_schools_df.head(5)
bottom5_performing_schools_df
```

    Bottom 5 Performing Schools (By Passing Rate): 
    




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
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>2,547,363</td>
      <td>637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>64.066017</td>
      <td>77.744436</td>
      <td>70.905226</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>1,910,635</td>
      <td>655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>63.318478</td>
      <td>78.813850</td>
      <td>71.066164</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>3,094,650</td>
      <td>650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>63.852132</td>
      <td>78.281874</td>
      <td>71.067003</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>1,884,411</td>
      <td>639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>63.750424</td>
      <td>78.433367</td>
      <td>71.091896</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>3,022,020</td>
      <td>652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>64.746494</td>
      <td>78.187702</td>
      <td>71.467098</td>
    </tr>
  </tbody>
</table>
</div>




```python
#student_data_df.head()

```

# Math Scores by Grade


```python
# **Math Scores by Grade**
# Create a table that lists the average Math Score for students of each grade level (9th, 10th, 11th, 12th) at each school.
math_score_by_school = student_data_df.groupby('school')["math_score"].mean()

stu_9th_grade_df = student_data_df.loc[student_data_df["grade"] == "9th",:]
math_score_9th_df = stu_9th_grade_df.groupby('school')["math_score"].mean()

stu_10th_grade_df = student_data_df.loc[student_data_df["grade"] == "10th",:]
math_score_10th_df = stu_10th_grade_df.groupby('school')["math_score"].mean()

stu_11th_grade_df = student_data_df.loc[student_data_df["grade"] == "11th",:]
math_score_11th_df = stu_11th_grade_df.groupby('school')["math_score"].mean()

stu_12th_grade_df = student_data_df.loc[student_data_df["grade"] == "12th",:]
math_score_12th_df = stu_12th_grade_df.groupby('school')["math_score"].mean()

math_scores_bygrade_df = pd.DataFrame({"9th Grade":math_score_9th_df, "10th Grade": math_score_10th_df, \
                               "11th Grade": math_score_11th_df, "12th Grade": math_score_12th_df},\
                                 columns = ["9th Grade", "10th Grade", "11th Grade", "12th Grade"])

print("Math Scores by Grade: ")
math_scores_bygrade_df


```

    Math Scores by Grade: 
    




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
      <th>9th Grade</th>
      <th>10th Grade</th>
      <th>11th Grade</th>
      <th>12th Grade</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>



# Reading Scores by Grade


```python
# **Reading Scores by Grade**
# Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.
rdg_score_by_school = student_data_df.groupby('school')["reading_score"].mean()

stu_9th_grade_df = student_data_df.loc[student_data_df["grade"] == "9th",:]
rdg_score_9th_df = stu_9th_grade_df.groupby('school')["reading_score"].mean()

stu_10th_grade_df = student_data_df.loc[student_data_df["grade"] == "10th",:]
rdg_score_10th_df = stu_10th_grade_df.groupby('school')["reading_score"].mean()

stu_11th_grade_df = student_data_df.loc[student_data_df["grade"] == "11th",:]
rdg_score_11th_df = stu_11th_grade_df.groupby('school')["reading_score"].mean()

stu_12th_grade_df = student_data_df.loc[student_data_df["grade"] == "12th",:]
rdg_score_12th_df = stu_12th_grade_df.groupby('school')["reading_score"].mean()

rdg_scores_bygrade_df = pd.DataFrame({"9th Grade":rdg_score_9th_df, "10th Grade": rdg_score_10th_df, \
                               "11th Grade": rdg_score_11th_df, "12th Grade": rdg_score_12th_df},\
                                 columns = ["9th Grade", "10th Grade", "11th Grade", "12th Grade"])

print("Reading Scores by Grade: ")
rdg_scores_bygrade_df

```

    Reading Scores by Grade: 
    




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
      <th>9th Grade</th>
      <th>10th Grade</th>
      <th>11th Grade</th>
      <th>12th Grade</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.303155</td>
      <td>80.907183</td>
      <td>80.945643</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.676136</td>
      <td>84.253219</td>
      <td>83.788382</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.198598</td>
      <td>81.408912</td>
      <td>80.640339</td>
      <td>81.384863</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.632653</td>
      <td>81.262712</td>
      <td>80.403642</td>
      <td>80.662338</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.369193</td>
      <td>83.706897</td>
      <td>84.288089</td>
      <td>84.013699</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.866860</td>
      <td>80.660147</td>
      <td>81.396140</td>
      <td>80.857143</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.677165</td>
      <td>83.324561</td>
      <td>83.815534</td>
      <td>84.698795</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.290284</td>
      <td>81.512386</td>
      <td>81.417476</td>
      <td>80.305983</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.260714</td>
      <td>80.773431</td>
      <td>80.616027</td>
      <td>81.227564</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.807273</td>
      <td>83.612000</td>
      <td>84.335938</td>
      <td>84.591160</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>80.993127</td>
      <td>80.629808</td>
      <td>80.864811</td>
      <td>80.376426</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.122642</td>
      <td>83.441964</td>
      <td>84.373786</td>
      <td>82.781671</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.728850</td>
      <td>84.254157</td>
      <td>83.585542</td>
      <td>83.831361</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.939778</td>
      <td>84.021452</td>
      <td>83.764608</td>
      <td>84.317673</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.833333</td>
      <td>83.812757</td>
      <td>84.156322</td>
      <td>84.073171</td>
    </tr>
  </tbody>
</table>
</div>




```python
#school_summary_df. For some reason Per student Budget, Total Students seems to be an object datatype. Convering it to float.
school_summary_df['Per Student Budget'] = school_summary_df['Per Student Budget'].convert_objects(convert_numeric=True)
school_summary_df['Total Students'] = school_summary_df['Total Students'].convert_objects(convert_numeric=True)
# school_summary_df['Total Students'] = school_summary_df['Total Students'].astype(str).astype(int)
print(school_summary_df.dtypes)
```

    School Type                object
    Total Students              int64
    Total School Budget        object
    Per Student Budget        float64
    Average Math Score        float64
    Average Reading Score     float64
    % Passing Math            float64
    % Passing Reading         float64
    % Overall Passing Rate    float64
    dtype: object
    

    C:\Users\Samsung\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:2: FutureWarning: convert_objects is deprecated.  Use the data-type specific converters pd.to_datetime, pd.to_timedelta and pd.to_numeric.
      from ipykernel import kernelapp as app
    C:\Users\Samsung\Anaconda3\envs\PythonData\lib\site-packages\ipykernel\__main__.py:3: FutureWarning: convert_objects is deprecated.  Use the data-type specific converters pd.to_datetime, pd.to_timedelta and pd.to_numeric.
      app.launch_new_instance()
    

# Scores by School Spending


```python
# **Scores by School Spending**
# Create a table that breaks down school performances based on average Spending Ranges (Per Student). 
# Use 4 reasonable bins to group school spending. Include in the table each of the following:
# Average Math Score
# Average Reading Score
# % Passing Math
# % Passing Reading
# Overall Passing Rate (Average of the above two)
# Create the names for the four bins
# group_names = ['Low', 'Okay', 'Good', 'Great']

#print max and min per student budget
#print(school_summary_df["Per Student Budget"].max())
#print(school_summary_df["Per Student Budget"].min())

# Bins are 'Low ($585)', 'Okay ($585-$615)', 'Good ($615-$645)', 'Great ($645-$675)'
bins_spending = [0, 585, 615, 645, 675]
group_names_spending = ["Low <$585", "Okay $585-615", "Good $615-645", "Great $645-675"]
school_summary_df["Spending Ranges (Per Student)"] = pd.cut(school_summary_df["Per Student Budget"], bins_spending, \
                                                            labels=group_names_spending)
spending_summary_df = school_summary_df.groupby("Spending Ranges (Per Student)")
spending_summary_math_df = spending_summary_df["Average Math Score"].mean()
spending_summary_rdg_df = spending_summary_df["Average Reading Score"].mean()
spending_summary_permath_df = spending_summary_df["% Passing Math"].mean()
spending_summary_perrdg_df = spending_summary_df["% Passing Reading"].mean()
spending_summary_overall_df = (spending_summary_permath_df + spending_summary_perrdg_df)/2

spending_summary_table_df = pd.DataFrame({"Average Math Score":spending_summary_math_df, \
                                          "Average Reading Score": spending_summary_rdg_df , \
                                          "% Passing Math": spending_summary_permath_df, \
                                          "% Passing Reading": spending_summary_perrdg_df, \
                                          "% Overall Passing Rate": spending_summary_overall_df},
                                 columns = ["Average Math Score", "Average Reading Score", "% Passing Math", \
                                            "% Passing Reading", "% Overall Passing Rate"])

print("Scores by School Spending:")
spending_summary_table_df


```

    Scores by School Spending:
    




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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Low &lt;$585</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>90.350436</td>
      <td>93.325838</td>
      <td>91.838137</td>
    </tr>
    <tr>
      <th>Okay $585-615</th>
      <td>83.599686</td>
      <td>83.885211</td>
      <td>90.788049</td>
      <td>92.410786</td>
      <td>91.599418</td>
    </tr>
    <tr>
      <th>Good $615-645</th>
      <td>79.079225</td>
      <td>81.891436</td>
      <td>73.021426</td>
      <td>83.214343</td>
      <td>78.117884</td>
    </tr>
    <tr>
      <th>Great $645-675</th>
      <td>76.997210</td>
      <td>81.027843</td>
      <td>63.972368</td>
      <td>78.427809</td>
      <td>71.200088</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Size


```python
# **Scores by School Size**
# * Repeat the above breakdown, but this time group schools based on a reasonable approximation of 
# school size (Small, Medium, Large).

bins_school_size = [0, 1000, 2000, 5000]
group_names_school_size = ["Small <1000", "Medium 1000-2000", "Large 2000-5000"]
school_summary_df["School Size"] = pd.cut(school_summary_df["Total Students"], bins_school_size, \
                                          labels = group_names_school_size)
school_size_summary_df = school_summary_df.groupby("School Size")
school_size_summary_math_df = school_size_summary_df["Average Math Score"].mean()
school_size_summary_rdg_df = school_size_summary_df["Average Reading Score"].mean()
school_size_summary_permath_df = school_size_summary_df["% Passing Math"].mean()
school_size_summary_perrdg_df = school_size_summary_df["% Passing Reading"].mean()
school_size_summary_overall_df = (school_size_summary_permath_df + school_size_summary_perrdg_df)/2

school_size_summary_table_df = pd.DataFrame({"Average Math Score":school_size_summary_math_df, \
                                          "Average Reading Score": school_size_summary_rdg_df , \
                                          "% Passing Math": school_size_summary_permath_df, \
                                          "% Passing Reading": school_size_summary_perrdg_df, \
                                          "% Overall Passing rate": school_size_summary_overall_df},
                                 columns = ["Average Math Score", "Average Reading Score", "% Passing Math", \
                                           "% Passing Reading", "% Overall Passing rate"])

print("Scores by school Size:")
school_size_summary_table_df

```

    Scores by school Size:
    




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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small &lt;1000</th>
      <td>83.821598</td>
      <td>83.929843</td>
      <td>91.158155</td>
      <td>92.471895</td>
      <td>91.815025</td>
    </tr>
    <tr>
      <th>Medium 1000-2000</th>
      <td>83.374684</td>
      <td>83.864438</td>
      <td>89.931303</td>
      <td>93.244843</td>
      <td>91.588073</td>
    </tr>
    <tr>
      <th>Large 2000-5000</th>
      <td>77.746417</td>
      <td>81.344493</td>
      <td>67.631335</td>
      <td>80.190800</td>
      <td>73.911067</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Type


```python
# **Scores by School Type**
# Repeat the above breakdown, but this time group schools based on school type (Charter vs. District).

school_type_summary_df = school_summary_df.groupby("School Type")
school_type_summary_math_df = school_type_summary_df["Average Math Score"].mean()
school_type_summary_rdg_df = school_type_summary_df["Average Reading Score"].mean()
school_type_summary_permath_df = school_type_summary_df["% Passing Math"].mean()
school_type_summary_perrdg_df = school_type_summary_df["% Passing Reading"].mean()
school_type_summary_overall_df = (school_type_summary_permath_df + school_type_summary_perrdg_df)/2

school_type_summary_table_df = pd.DataFrame({"Average Math Score":school_type_summary_math_df, \
                                          "Average Reading Score": school_type_summary_rdg_df , \
                                          "% Passing Math": school_type_summary_permath_df, \
                                          "% Passing Reading": school_type_summary_perrdg_df, \
                                          "% Overall Passing rate": school_type_summary_overall_df},
                                 columns = ["Average Math Score", "Average Reading Score", "% Passing Math", \
                                           "% Passing Reading", "% Overall Passing rate"])

print("Scores by School Type:")
school_type_summary_table_df
```

    Scores by School Type:
    




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
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>90.363226</td>
      <td>93.052812</td>
      <td>91.708019</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>64.302528</td>
      <td>78.324559</td>
      <td>71.313543</td>
    </tr>
  </tbody>
</table>
</div>


