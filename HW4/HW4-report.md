# HW 4 - CS 625, Fall 2023

Maaz Hasnain Khan 

Due: October 25, 2023

### NOTE:
It has to be noted that the data was cleaned before plotting of charts and only meaningful data was extracted from each dataset for specific questions. The cleaned data are located in separate files named with the dataset and question number.

## Dataset 3

Table 102 - Expectation of Life at Birth, and Projections

**Q1:** Using Table 102, compare life expectancy for people born between 1970-1999 for the four categories, "Male", "Female", "White", "Black".

![Multiple Line Chart Dataset 3 Question 1](dataset3_q1_excel.png)

The line chart effectively illustrates how life expectancy has changed between 1970 and 1999 for various demographic categories: "Total Male," "Total Female," "Total White," and "Total Black." The chart primarily highlights the overall trends in life expectancy within this 30-year timeframe. A line chart is a suitable choice for this data because it effectively displays the changes in life expectancy for individuals born between 1970 and 1999, allowing for clear comparisons between different categories.

Idiom: Multiple Line Chart / Mark: Dots
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Year | Key, Temporal | Horizontal Position (X-axis) |
| Life Expectancy (Years) | Value, Quantitative | Vertical Position (Y-axis) |
| Sex | Key, Categorical | Color Hue (Third Channel) |

The x-axis denotes the years, spanning from 1970 to 1999, facilitating a temporal analysis. On the y-axis, life expectancy is represented, offering insight into the average expected age at birth for individuals in each of the specified categories.

The chart's key findings are as follows:

- "Total Female" consistently exhibits higher life expectancy compared to "Total Male," indicating that, on average, females tend to live longer than males.

- "Total White" generally demonstrates a higher life expectancy than "Total Black," reflecting disparities in life expectancy along racial lines.

- The chart reveals the variations in life expectancy from year to year. It shows a constant upward trend as the years go by indicating the increase in life expectancy for all demographics. This maybe due to several factors including betterment of the healthcare facilities and modern medicine.

In conclusion, the chart effectively presents the changing trends in life expectancy over a 30-year period, offering valuable insights into the differences among demographic groups and changes in life expectancy during this time frame.

**The Excel File for this chart, [dataset3_q1_excel.xlsx](dataset3_q1_excel.xlsx)**

**Q2:** How does this compare to the number of women in each age group who had a child (not necessarily their first) in that year? What does this say about the age of women giving birth in the US?

**Further Questions:** What further questions does this prompt?  What hypotheses do you have about what the answers might be?  Are there other tables that might help you address these questions?  

**Extra Credit [2 points]:** Combine the data from Tables 91 and 92 (Women Who Have Had a Child in the Last Year By Selected Characteristics) to investigate other factors that affect this.




## References

* First DataSet CSV File, [dataset_1.csv](dataset_1.csv)
* Second Data Set CSV File, [Organ-Transplant-Cleaned.csv](Organ-Transplant-Cleaned.csv)
* First Data Set Raw File, [Cancer-Data-Raw.xls](Cancer-Data-Raw.xls)
* Second Data Set Raw File, [Organ-Transplant-Raw.xls](Organ-Transplant-Data-Raw.xls)
* Google Colab Jupyter Source File, [CS_625_HW3.ipynb](CS_625_HW3.ipynb)
* Bar Chart in Excel XLSX File, [Cancer-Data-Cleaned.xlsx](Cancer-Data-Cleaned.xlsx)
* PyData (Seaborn), <https://seaborn.pydata.org/generated/seaborn.objects.Dot.html>
* PyData (Pandas),<https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html>
* Markdown Guide, <https://www.markdownguide.org/basic-syntax/#links>
* From Data to Viz, <https://www.data-to-viz.com/graph/barplot.html#:~:text=Definition,bar%20represents%20its%20numeric%20value.>
* Visme, <https://visme.co/blog/scatter-plot/>
* Python Charts, <https://python-charts.com/seaborn/grid/>
* Anaconda, <https://anaconda.cloud/seaborn-objects-system>
* Github, <https://github.com/mwaskom/seaborn/issues/3146>
* SaturnCloud, <https://saturncloud.io/blog/adding-text-relative-to-axes-in-seaborn-and-matplotlib-a-guide/>
* Stackoverflow, <https://stackoverflow.com/questions/41511334/adding-text-to-each-subplot-in-seaborn>
* United States Census Bureau, <https://www.census.gov/library/publications/2011/compendia/statab/131ed.html>
https://stackoverflow.com/questions/76644454/is-there-an-alternate-for-palette-while-plotting-barplot-through-seaborn-objec
https://stackoverflow.com/questions/74715767/how-to-rotate-the-xticks-with-seaborn-objects
https://stackoverflow.com/questions/53694724/how-to-prevent-matplotlib-from-showing-decimal-years-in-horizontal-axis