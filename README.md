# School District Analysis - <i>PyCitySchools</i>

## Project Overview
The School Board wanted summary data reported for their district and provided school and student data for analysis.<br>
We have provided the analysis of the data to their specifications.<br><br>
Subsequently, they have discovered that the 9th grade scores for one school, Thomas High School, are suspect.<br>
The School Board wants to have the analysis redone, excluding these scores. <br>
Additionally, they want to know how the overall analysis is affected by omitting the dubious scores.<br><br>

### The analysis of the School District Data included these elements:
- A District Summary
- Key metrics for each school
- Average math and reading scores by students in each grade level at each school
- Passing percentage for math and reading
- Overall passing percentage (both math and reading)
- Top 5 and bottom 5 schools based on overall passing rate
- School performance by budget per student
- School performance based on school size
- School performance based on the type of school (District or Charter)

## Effect of Data Exclusion
### District Summary Report
<b>District Summary Report Before:</b><br>
  <img src=/Resources/District_Summary_Before.png></img><br>
<b>District Summary Report After:</b><br>
  <img src=/Resources/District_Summary_After.png></img><br>

The District Summary Report showed a lower average math score (78.9 vs 79.0) after the change in the data.<br>

### School Summary Report
<b>School Summary Report Before:</b><br>
  <img src=/Resources/School_Summary_Before.png></img><br>
<b>School Summary Report After:</b><br>
  <img src=/Resources/School_Summary_After.png></img><br>

The School Summary Report showed a lower average math score, higher average reading score, lower passing math percentage, lower passing reading percentage, and lower overall passing percentage after the change in the data.

### Top 5 Schools
<b>Top 5 Schools Before:</b><br>
<img src=/Resources/Top_Schools_Before.png></img><br>
<b>Top 5 Schools After:</b><br>
<img src=/Resources/Top_Schools_After.png></img><br>

Thomas High School's overall passing percentage has decreeased, but it retains the #2 position on the Top Five list.

### Scores by Grade
<b>Math Scores by Grade Before:<b><br>
  <img src=/Resources/Math_Scores_by_Grade_Before.png></img><br>
<b>Math Scores by Grade After:<b><br>
  <img src=/Resources/Math_Scores_by_Grade_After.png></img><br>
<b>Reading Scores by Grade Before:<b><br>
  <img src=/Resources/Reading_Scores_by_Grade_Before.png></img><br>
  <img src=/Resources/Reading_Scores_by_Grade_After.png></img><br>

As expected, there are no 9th grade scores for Thomas High School in the changed data.

### Scores by Spending Per Student
<b>Spending Summary Before:<b><br>
  <img src=/Resources/Spending_Summary_Before.png></img><br>
<b>Spending Summary After:<b><br>
  <img src=/Resources/Spending_Summary_After.png>/<img><br>
The scores and percentages, except for reading average, are slightly lower after the data change for the $630-$644 range.
  
### Scores by Spending by School Size
<b>Size Summary Before:<b><br>
  <img src=/Resources/Size_Summary_Before.png></img><br>
<b>Size Summary After:<b><br>
  <img src=/Resources/Size_Summary_After.png>/<img><br>
The scores and percentages, except for reading average, are slightly lower after the data change for the Medium (1000-2000) range.
  
### Scores by School Type
<b>Size Summary Before:<b><br>
  <img src=/Resources/Type_Summary_Before.png></img><br>
<b>Size Summary After:<b><br>
  <img src=/Resources/Type_Summary_After.png>/<img><br>
The scores and percentages, except for reading average, are slightly lower after the data change for the Charter School Type.

### Methodology
Two files were received, schools_complete.csv and students_complete.csv and imported into Panda DataFrames.<br>
```
# File to Load
school_data_to_load = "Resources/schools_complete.csv"
student_data_to_load = "Resources/students_complete.csv"

# Read the School Data and Student Data and store into a Pandas DataFrame
school_data_df = pd.read_csv(school_data_to_load)
student_data_df = pd.read_csv(student_data_to_load)``
```
The student names were cleaned up to remove extraneous prefixes and suffixes
```
# Cleaning Student Names and Replacing Substrings in a Python String
# Add each prefix and suffix to remove to a list.
prefixes_suffixes = ["Dr. ", "Mr. ","Ms. ", "Mrs. ", "Miss ", " MD", " DDS", " DVM", " PhD"]

# Iterate through the words in the "prefixes_suffixes" list and replace them with an empty space, "".
for word in prefixes_suffixes:
    student_data_df["student_name"] = student_data_df["student_name"].str.replace(word,"")``
```
The 9th grade scores from Thomas High School were changed to NaN (Not a Number) using the Numpy library so that they will be ignored.
```
import numpy as np
student_data_df.loc[(student_data_df.grade == "9th") & (student_data_df.school_name == "Thomas High School"),["reading_score"]] = np.nan
student_data_df.loc[(student_data_df.grade == "9th") & (student_data_df.school_name == "Thomas High School"),["math_score"]] = np.nan``
```
The DataFrames containg the data from the two files were combined to facilitate the rest of the analysis
```
# Combine the data into a single dataset
school_data_complete_df = pd.merge(student_data_df, school_data_df, how="left", on=["school_name", "school_name"])
```
<b>Note: Complete confidentiality of the studens' data was maintained in accordance with FERPA (Family Educational Rights and Privacy Act).</b>

### Conclusions<br>
After the omission of the 9th grade data from Thomas High School, the following was noted across all observations:
- The Average Math Score was lower
- The Passing Math Percentage was lower
- The Passing Reading Percentage was lower
- The Overall Passing Percentage was lower<br>

Since it is unlikely that this one class would normally have grades high enough to skew the grades so consistently, the School Board is encuraged to not include these grades in their official report
