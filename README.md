# Pandas In python

This is a simple quick guide on working with files in pandas. We will be working with the following types of files and learn how to read and write using the pandas library.

<p align="center">
 <img src="https://img.shields.io/static/v1?label=language&message=python&color=green"/>
<img src="https://img.shields.io/static/v1?label=liked-most&message=jupyter-notebook&color=brightgreen"/>
<img src="https://img.shields.io/static/v1?label=liked-most&message=pandas&color=red"/>
</p>
<p align="center">
    <img src="https://github.com/CrispenGari/Pandas/blob/main/1200px-Pandas_logo.svg.png"/>
</p>

- CSV
- TXT
- Excel

## Installation

To install pandas run the following command

```shell
$ pip install pandas
```

## Importing library dependencies

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

### 1. Reading CSV files

The following lines of code will read the CSV files and display the data in jupyter Notebook.

```python
df = pd.read_csv("files/airquality.csv")
df
```

### 2. Reading TXT files

The following lines of code will read the TXT files and display the data in jupyter Notebook.

```python
df = pd.read_csv("files/airquality.txt", delimiter="\t")
df
```

### 3. Reading EXCEL files `xlsx`

The following lines of code will read the `xlsx` files and display the data in jupyter Notebook.

```python
df = pd.read_excel("files/cars.xlsx")
df
```

### Reading the first and last columns of the files

Pandas has a function called `head(n)` and `tail(n)` these functions returns the first n `rows` and last n `rows` of the file. If n is not specified the default number n is 5. Let's say we want to read the first 10 and the last 10 rows of the file `airquality.csv`. We can do it using the head and the tail functions respectively.

```python
df = pd.read_csv("files/airquality.csv")
```

##### `head(n)`

```python
df.head(10)
```

##### `tail(n)`

```python
df.tail(10)
```

> You will notice that the index of the tail data has an index that starts from 143. So there's a function called `reset_index()` that resets the index to start at 0. The usage is as follows

```python
df.tail(10).reset_index()
```

## Filtering data

#### Reading certain columns in a data frame

Firstly, we want to read the `Temp` column only in our data frame of the file `airquality.csv` and secondly we will read Ozone, Wind,Temp,Month,Day from this data frame. This can be done as follows:

```python
# reading one column

df["Temp"].head(10)
```

```python
# reading Ozone, Wind,Temp,Month,Day

df[["Ozone", "Wind", "Temp", "Month", "Day"]].head(10)
```

#### Getting the Headings

```python
cls = df.columns
print(cls)

# using numpy indexing to get the colums we are intrested in from Ozone upwards

print(df.columns[1:])
```

### Getting rows from the data DataFrame

We can use the `iloc` or the `loc` primarily label based to index specific rows. Let's say we want to get the row at index 1 we can index it as follows:

- [Read More](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)

###### a. Getting a single row from the DataFrame

```python
df.loc[1]
# or
df.iloc[1]
```

##### b. Getting more than one row from the DataFrame

> We can use numpy indexing to get multiple rows from a data frame. Example:

```python
df.loc[2: 5]
```

## Creating a column based on the available data from the data frame

We want to create a new column called `Temp x2` which we will be obtain by multplying the Temp by 2

```python
df["Temp x2"] = df["Temp"] * 2
df
```

### Creating numpy arrays from the columns.

Let's say we want are interested in getting the temperature and the wind from our data frame. Suppose we want to draw some plots based on this data using pyplot from matplotlib. Looking at it this way we need to create two array the one for temperature and the other for wind. We will use these two numpy arrays to come up with some plots.

> Getting the temperature and wind

```python
wind = np.array(df['Wind'])
print(wind)
temp = np.array(df.Temp)
temp
```

> Plotting the data

#### scatter plot

```python
# we want to plot a scatter plot, regression line

from numpy.polynomial.polynomial import polyfit
constant, gradient = polyfit(wind, temp, 1)

plt.plot(wind, gradient* wind + constant, '-g', linewidth=2)
plt.title("THE TEMPERATURE WIND", fontsize=20, fontfamily='Arial', fontweight="bold")
plt.xticks([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15])
plt.yticks([0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100])
plt.scatter(wind, temp, label="Scatter", marker="o", color='r', edgecolor='blue')
plt.xlabel("Wind", fontsize=15, fontfamily='Arial', fontweight="bold")
plt.ylabel("Temp", fontsize=15, fontfamily='Arial', fontweight="bold")
plt.legend()
plt.rcParams["figure.figsize"] = (10, 6)
plt.rcParams["figure.facecolor"] ='lightgray'
plt.show()
```

#### line plot

```python
# we want to plot line graph

plt.title("THE TEMPERATURE WIND", fontsize=20, fontfamily='Arial', fontweight="bold")
plt.xticks([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15])
plt.yticks([0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100])
plt.plot(wind, temp, '-or', markeredgecolor="b", label="Line Plot")
plt.xlabel("Wind", fontsize=15, fontfamily='Arial', fontweight="bold")
plt.ylabel("Temp", fontsize=15, fontfamily='Arial', fontweight="bold")
plt.legend()
plt.rcParams["figure.figsize"] = (10, 6)
plt.rcParams["figure.facecolor"] ='lightgray'
plt.show()

```

## Attributes

###### df.at[row, column]

Used to access a certain values using the row by column index. For example let's say we want to access the temperature in our data frame that is at index 0.

```python
df.at[0, 'Temp']
```

##### 2. df.attrs

Returns dictionary of global attributes of this dataset.

> example:

```python
df.attrs
```

##### 3. df.axes

Return a list representing the axes of the DataFrame.

> example:

```python
df.axes
```

###### 4. df.columns

The column labels of the DataFrame.

> Example

```python
df.columns
```

###### 5. df.dtypes

Return the dtypes in the DataFrame.

> Example:

```python
df.dtypes
```

###### 6. df.empty

Indicator whether DataFrame is empty.

> Example:

```python
df.empty
```

###### 7. df.flags

Get the properties associated with this pandas object.

> Example:

```python
df.flags
print(df.flags)
print(df.flags.allows_duplicate_labels)
# OR
print(df.flags["allows_duplicate_labels"])
```

###### 8. df.iat[rowIndex columnIndex]

Access a single value for a row/column pair by integer position.

> Example:

```python
df.iat[1,2 ]
```

###### 9. df.iloc

Purely integer-location based indexing for selection by position. It can also takes array of indexes

> Example:

```python
#  getting row at index 0
print(df.iloc[0])
#  Normal indexing
df.iloc[[2, 3, 4,5]]
```

###### 10. df.index

The index (row labels) of the DataFrame.

> Example:

```python
df.index
```

###### 11. df.loc

Access a group of rows and columns by label(s) or a boolean array.

> Example:

```python
print(df.loc[0])
print(df.loc[[1, 7]])

df.head().loc[df["Wind"] > 12].reset_index()
```

###### 12. df.ndim

Return an int representing the number of axes / array dimensions.

> Example:

```python
df.ndim
```

###### 13. df.shape

Return an int representing the number of axes / array dimensions.

> Example:

```python
df.shape
```

###### 14. df.size

Return an int representing the number of elements in this object.

> Example:

```python
df.size
```

###### 15. df.style

Returns a Styler object.

> Example:

```python
df.style
```

###### 16. df.values

Return a Numpy representation of the DataFrame.

> Example:

```python
df.values
```

### Methods

There are a lot of methods in pandas data frame but we will be focusing on few methods. You can find them here:

###### 1. df.abs()

Return a Series/DataFrame with absolute numeric value of each element.

> Example:
```python
pass
```


###### 2. df.add(), df.div(), df.mul(), df.pow(), df.mod() etc.

Get Addition of dataframe and other, element-wise (binary operator <add>).

> Example:

```python
df.head().add(1)
....
df.head().mod(7)
...

```

###### 3. df.all() // df.any()

Return whether all/any elements are True, potentially over an axis.

> Example:

```python
df.head().all()
df.head().any()
```

###### 4. df.append()

Append rows of other to the end of caller, returning a new object.

> Example:

```python
df2 = pd.DataFrame([[7, 15, 256.0, 12.0, 88, 7, 7],[9, 15, 256.2, 12.3, 89, 7, 7]], columns=["Unnamed: 0", "Ozone", "Solar.R", "Wind", "Temp", "Month", "Day"])

df.append(df2).tail(5)
```

###### 5. df.copy()

Make a copy of this object’s indices and data.

> Example:

```python
df2 = df.tail().copy()
df2
```

###### 6. df.cum<Fuct>

- cummax([axis, skipna])

  - Return cumulative maximum over a DataFrame or Series axis.

- cummin([axis, skipna])

  - Return cumulative minimum over a DataFrame or Series axis.

- cumprod([axis, skipna])

  - Return cumulative product over a DataFrame or Series axis.

- cumsum([axis, skipna])

      * Return cumulative sum over a DataFrame or Series axis.

  > Example:

```python
df2 = df.tail()
df2.cumsum(1)
```

###### 7. df.equals(df2)

Test whether two objects contain the same elements.

> Example:

```python
print(df2.equals(df.head()))
df2.equals(df.tail())

```

> There are a lot of functions refer to the docs [FUNCTIONS](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)

## Saving data to csv, txt and xlsx files

Suppose we want to create a file that will hold only 10, with the 'Wind x2' column which multiply the wind column by 2 in every row. We will output this to txt, xlsx and csv files.

#### Saving to csv file

`df.to_csv(path, sep) method`

> Example:

```python

df["Wind x2"] = df["Wind"] * 2
df2 = df.head(10)
df2
# Writing to csv
df2.to_csv("windx2.csv", index=False)
```

#### Saving to text file

`df.to_csv(path, sep) method`

> Example:

```python
df["Wind x2"] = df["Wind"] * 2
df2 = df.head(10)
df2
# Writing to csv
df2.to_csv("windx2.txt", sep="\t" ,index=False)
```

#### Saving to xlsx file

`df.to_excel(path) method`

> Example:

```python
df["Wind x2"] = df["Wind"] * 2
df2 = df.head(10)
df2
# Writing to csv
df2.to_excel("windx2.xlsx", index=False)
```

## Conditions on DataFrame

We can display data based on certain conditions. inside our files directory we have a file called 'HairEyeColor.csv` we want to display all people with brown eyes that are female. This can be done as follows.

```python
# Reading the data and show it
df = pd.read_csv("files/HairEyeColor.csv")
df

## Filter the data based on given the conditions

df = df.loc[(df.Eye == "Brown") & (df.Sex == 'Female')]
df.reset_index()

## Visulise the data using a bar graph

labels = []

for i in range(df.shape[0]):
    labels.append(f"{df.iloc[i].Hair} {df.iloc[i].Eye}" )

labels = np.array(labels)
# plot labes vrs Freq
height = np.array(df.Freq)
colors = np.array(["black", "brown", "red", "lightseagreen"])
plt.bar(labels, height,.5, color=colors, label=labels)
plt.xlabel("Hair-Eye Color",fontsize=14, fontfamily="arial", fontweight="bold" )
plt.ylabel("Frequency",fontsize=14, fontfamily="arial", fontweight="bold" )
plt.title("Female Hair and Eyes Color", fontsize=20, fontfamily="arial", fontweight="bold")

plt.show()
```

## Other resources

- [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)
- [Pandas API Documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.mul.html)

### Where to find datasets file for pandas?

- [forge.scilab.org](https://forge.scilab.org/index.php/p/rdataset/source/tree/master/csv)
- [teoalida.com](https://www.teoalida.com/cardatabase/)
