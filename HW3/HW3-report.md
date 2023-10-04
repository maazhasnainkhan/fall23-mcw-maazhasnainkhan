# HW 3 - CS 625, Fall 2023

Maaz Hasnain Khan 

Due: October 4, 2023

##  First Data

- The first data set is from Table 183 Section 3 Health Conditions, Diseases

    [Cancer--Estimated New Cases and Deaths by State](https://www2.census.gov/library/publications/2011/compendia/statab/131ed/tables/12s0183.xls)

### Data Wrangling

First we used open refine to clean the data and get rid of any unnecessary headers and footers in the *.xls* file and converted it into *.csv* file. There wasn't much worng with the data, therefore, there was not much data to be cleaned. After getting the *.csv* file, we used python to further manipulate and process the data. This was a complex process, hence, will be discussed in points:

#### For Bar Chart
* First, we mount Google Drive to access files, and then read a CSV file named *"Cancer-Data-Cleaned.csv"* into a Pandas DataFrame.
* Then, we remove the first row (index 0) from the DataFrame.
* After that, we randomly select 10 rows from the DataFrame as a subset.
* Then, we create a new DataFrame named *'cancer_data_state'* that contains only the *'State'* and *'New cases Total'* columns from the subset.
* Then, we sort the *'cancer_data_state'* DataFrame based on the *'New cases Total'* column in ascending order.
* Finally, we create a bar plot using the Seaborn library. The plot displays the 'State' on the x-axis and 'New cases Total' on the y-axis, with additional text annotations. The plot is formatted with specific dimensions and ticks for the axes.

#### For Scatter Plot
* First, we mount Google Drive to access files and read a CSV file named *"Cancer-Data-Cleaned.csv"* from Google Drive into a Pandas DataFrame called *'cancer_data'*.
* Then, we remove the first row (index 0) from the *'cancer_data'* DataFrame, resulting in a DataFrame called *'cases_death_cancer_data'*.
* After that, we randomly select 25 rows from the *'cases_death_cancer_data'* DataFrame to create a subset, which is stored in a new DataFrame called *'cases_death_cancer_data_25'*.
* Then, we create a scatterplot (dot plot) using the Seaborn library. The plot displays *'New cases Total'* on the x-axis and *'Deaths Total'* on the y-axis, with each dot colored based on the *'State'* column.
* Finally, we format the plot with a specified size, adjust the size and appearance of the dots, and set ticks on the axes for better readability.

##### Note:
The charts in the report and google colab might be different as we have used data in random form. For bar chart, we have used data from 10 random States and similarly for scatter plot, we have used data from 25 random states. So, upon running the code again the chart might come out different than the original one.

##  Second Data
- The second data set is from Table 181 Section 3 Health Conditions, Diseases

    [Organ Transplant](https://www2.census.gov/library/publications/2011/compendia/statab/131ed/tables/12s0181.xls)

### Data Wrangling



## References

* First Data Set CSV File, [Cancer-Data-Cleaned.csv](Cancer-Data-Cleaned.csv)
* Second Data Set CSV File, [Organ-Transplant-Cleaned.csv](Organ-Transplant-Cleaned.csv)
* First Data Set Raw File, [Cancer-Data-Raw.xls](Cancer-Data-Raw.xls)
* Second Data Set Raw File, [Organ-Transplant-Raw.xls](Organ-Transplant-Data-Raw.xls)
* Google Colab Jupyter Source File, [CS_625_HW3.ipynb](CS_625_HW3.ipynb) 
* PyData (Seaborn), <https://seaborn.pydata.org/generated/seaborn.objects.Dot.html>
* PyData (Pandas),<https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html>
* Markdown Guide, <https://www.markdownguide.org/basic-syntax/#links>