[![Up to Date](https://github.com/ikatyang/emoji-cheat-sheet/workflows/Up%20to%20Date/badge.svg)](https://github.com/ikatyang/emoji-cheat-sheet/actions?query=workflow%3A%22Up+to+Date%22)

<!-- ![Build Status](https://travis-ci.org/yourusername/yourproject.svg?branch=main) -->

# :bookmark_tabs: PA 4 - Data Wrangling and Data Visualization

> [!NOTE]
> :open_book: *Data Wrangling* (also called ***data munching***) - involves **manipulation** and **transformation** of data frames in preparation for data analytics.

> [!NOTE]
>  :open_book: *Data visualization* - is the *graphical representation* of **any information** or **data**. 
> ###### :heavy_check_mark: Data visualization provides a way of understanding trends, outliers, and patterns in data
> ###### :heavy_check_mark:  Thus, it is a mean of turning numerical data into a “story” that can convey a significant or key message.

## 📖 Intended Learning Outcomes
1. To identify the codes and functions needed in cleaning and visualizing data
2. To be able to apply and use the different codes and functions in creating a Python program that will
be used in data wrangling and data visualization

---

## :bookmark: Python Demonstration 1:
- In this demonstration, we will display how to perform data wrangling operations in corporate with Pandas DataFrane Methods.
> [!NOTE]
> `Pivot Data`: Rotate data from a long format to a wide format, making it easier to analyze and visualize.

### CODE IMPLEMENTATION
##### :keyboard: *Input:* 
```python
# Import related library
import pandas as pd

data = {
    'Country':['Afghanistan', 'Afghanistan', 'Afghanistan', 'Afghanistan', 'Brazil', 'Brazil', 'Brazil', 'Brazil', 'China', 'China', 'China', 'China'],
    'Year': [1999, 1999, 2000, 2000, 1999, 1999, 2000, 2000, 1999, 1999, 2000, 2000],
    'Key': ['Cases', 'Population', 'Cases', 'Population', 'Cases', 'Population', 'Cases', 'Population', 'Cases', 'Population', 'Cases', 'Population'],
    'Value': [745, 19987071, 2666, 20595360, 37737, 172006362, 80488, 174504898, 212258, 1272915272, 213766, 1280428583]
}

messy = pd.DataFrame(data, columns = ['Country', 'Year', 'Key', 'Value'])
messy
```

##### :computer: *Output:*
- **To make this dataset clean**, perform data wrangling operations to convert this dataframe using *tidy dataframe method*.
```python
#To convert rows into columns of data, use pivot_table
tidy = messy.pivot_table(index=['Country', 'Year'], columns = 'Key', values = 'Value').reset_index()
tidy
```

- After converting this messy dataset to **tidy data**, extract the following information using *pandas subsetting operations*:
  
**1.** Number of TB cases in China at year 2000
```python
# Using .loc allows you to select data based on the row and column labels
tidy.loc[5,'Cases']
```

**2.** Rate of infection (cases/population) in Brazil at year 1999
```python
# Using .loc allows you to select data based on the row and column labels
tidy.loc[2,'Cases']/tidy.loc[2,'Population']
```
---

## Python Demonstration 2:
- In this demonstration, we will display how to perform data wrangling operations in corporate with Pandas DataFrane Methods.
> [!NOTE]
> `sort_values` function - it sorts the DataFrame by the values in the specified column(s).
> - `by='Student'`: specifies the column to sort by.
> - The resulting DataFrame will have the rows sorted in ascending order (default) based on the values in the Student column.
>
>   
> `reset_index` function - resets the index of the DataFrame. When you sort a DataFrame, the original index is preserved, which can lead to a non-sequential index. 
> - it reassigns a new sequential index to the DataFrame.
> - `drop=True`: specifies that the original index column should be dropped (not included) in the resulting DataFrame.
>
> 
> `melt` function - it takes a wide-format DataFrame as input and returns a long-format DataFrame. It "melts" the data by:
> - **Unpivoting column**s: Converting columns into rows.
> - **Creating a new variable column**: Adding a new column to store the original column names.

### CODE IMPLEMENTATION
##### :keyboard: *Input:*
```python
import pandas as pd

data = {
    'Student':['Ice Bear', 'Panda', 'Grizzly'],
    '2014': [80, 95, 79],
    '2015': [85, 81, 83]
}

webarebears = pd.DataFrame(data, columns = ['Student', '2014', '2015'])
webarebears
```

#### :mag_right: The dataframe shown is messy data because there are columns that are not actually variables but rather values of observation.

##### :computer: *Output:*
- **To make this dataset clean**, perform data wrangling operations to convert this dataframe using *melt dataframe method*.
```python
# To convert columns into rows, use melt
pd.melt(webarebears, id_vars = ['Student'],
        value_vars = ['2014', '2015'],
        var_name = 'Year', value_name = 'Grades').sort_values(by='Student').reset_index(drop=True)
```

---

## Python Demonstration 3:
- In this demonstration, we will display how to perform data visualization operations in corporate with Pandas DataFrane Methods.
  
> [!IMPORTANT]
> :file_folder: Save this DataFrame to your default user folder by downloading this link folder [board.csv](https://github.com/user-attachments/files/17082430/board.csv)
> - ###### This file folder (***board.csv***) will be used for Python Demo 3.

> [!NOTE]
> `&` operator - ensures that all of these conditions must be _True_ for a _row to be selected_. If any of these conditions are _False_, the entire expression will evaluate to False, and the _row will not be selected_.
>  - often used in conditional statements, such as **_if_** statements and list comprehensions, to filter data or make decisions based on multiple conditions.

### CODE IMPLEMENTATION 
##### :keyboard: *Input:*
```python
# Use pandas to read the CSV file into a DataFrame
df = pd.read_csv('board.csv')
df
```
##### :computer: *Output:*
**1.** Check the data overview
```python
df.describe()
```

**2.** Extract the data of the following:
- Students whose Math grades are above 70
```python
# To select rows from a Pandas DataFrame df where the value in the 'Math' column is greater than 70.
df.loc[(df['Math']>70)]
```

- Students whose grades are above 70 for all subjects.
```python
# To select rows from the DataFrame where the values in multiple columns (all subjects).
df.loc[(df['Math']>70) &
      (df['Electronics']>70) &
      (df['GEAS']>70) &
      (df['Communication']>70)]
```

- Students whose grades are below 70 but greater than 60.
```python
# To efficiently filter out rows from a DataFrame where the values in multiple columns fall within a specific range.
# Use a define function
x = df[(df['Math'] < 70) & (df['Math'] > 60) &
(df['Electronics'] < 70) & (df['Electronics'] > 60) &
(df['GEAS'] < 70) & (df['GEAS'] > 60) &
(df['Communication'] < 70) & (df['Communication'] > 60)]

x

```
---
**4.** Show the data in a graphical format.
##### :keyboard: *Input:*
```python
# To allow for more concise and readable code when creating plots and visualizations
import matplotlib.pyplot as plt
```

##### :computer: *Output:*
- Used **Bar Chart** to present the data.
``` python
plt.figure(figsize=(20, 4))
plt.bar(df['student name'], df['Math'])
```
> [!NOTE]
> `plt.figure(figsize=(20, 4))`: This line creates a new figure for the plot, and sets its size to be _20 inches wide and 4 inches tall_.
> - The figsize parameter is a tuple that specifies the width and height of the figure in inches.
> - By setting the figure size, you can control the overall size of the plot and make it more readable.
>
> 
> `plt.bar(df['student name'], df['Math'])`: This line creates a bar chart using the bar function from matplotlib. The chart is created based on the data in the df DataFrame.
> - The 1st argument df['student name'] specifies the x-axis values, which are the student names in this case.
> - The 2nd argument df['Math'] specifies the heights of the bars, which are the Math scores in this case.

- Used **Histogram** to present the data.
```python
df.plot.hist(x='student name', y=['Math', 'GEAS', 'Electronics', 'Communication'])
```
> [!NOTE]
> `df.plot.hist`: This method creates a histogram plot from the data in the DataFrame.
>
> 
> `x='student name'`: This parameter specifies the column in the DataFrame to use as the x-axis labels.
>
> 
> `y=['Math', 'GEAS', 'Electronics', 'Communication']`: This parameter specifies the columns in the DataFrame to use as the data for the histogram. In this case, it's a list of four columns: 'Math', 'GEAS', 'Electronics', and 'Communication'.

> [!TIP]
> This repository lacks a predefined output, in contrast to the prior PA2, due to its design, which fosters engagement and stimulates interest in Pandas. It would be best to explore it yourself to fully understand its functionalities and applications.

## Author
Julian Bernice Kristoffer Tomenio


## 🔑 Version History
- 1.03
  - Amended and completed the README file.

- 1.02
  - Added the README file.

- 1.01
  - Added the supplemental files

- 1.00 
  - Repository has been established
