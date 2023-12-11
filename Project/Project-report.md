# Final Project - CS 625, Fall 2023

Maaz Hasnain Khan 

Due: December 11, 2023

# Raw Data

FluNet, an online platform initiated in 1997, serves as a vital tool for worldwide surveillance of influenza viruses. It plays a crucial role in monitoring and understanding the global spread of these viruses by collecting and providing virological data, such as the count of influenza viruses categorized by subtype. This information is instrumental in interpreting epidemiological data. By using data acquired through FluNet, we will employ data science & data visualization techniques to analyze influenza virus trends post pre and post COVID-19 era.

**[Global Influenza Programme - FluNet](https://www.who.int/tools/flunet)**

## Data Wrangling/Cleaning

```

import pandas as pd
from google.colab import drive

drive.mount("/content/drive", force_remount = True)

influenza_df = pd.read_csv("/content/drive/MyDrive/CS_620/CS_620_Data_Project/VIW_FNT.csv")

columns_to_replace_null = [
    'AH1N12009', 'AH1', 'AH3', 'AH5', 'AH7N9',
    'ANOTSUBTYPED', 'ANOTSUBTYPABLE', 'AOTHER_SUBTYPE', 'AOTHER_SUBTYPE_DETAILS',
    'INF_A', 'BVIC_2DEL', 'BVIC_3DEL', 'BVIC_NODEL', 'BVIC_DELUNK',
    'BYAM', 'BNOTDETERMINED', 'INF_B', 'INF_ALL', 'INF_NEGATIVE',
    'ILI_ACTIVITY', 'ADENO', 'BOCA', 'HUMAN_CORONA', 'METAPNEUMO',
    'PARAINFLUENZA', 'RHINO', 'RSV', 'OTHERRESPVIRUS'
]

influenza_df[columns_to_replace_null] = influenza_df[columns_to_replace_null].fillna(0)

columns_to_remove = ['ITZ', 'MMWR_WEEKSTARTDATE', 'MMWR_YEAR', 'MMWR_WEEK', 'ORIGIN_SOURCE', 'SPEC_RECEIVED_NB', 'AOTHER_SUBTYPE_DETAILS', 'ILI_ACTIVITY', 'ADENO', 'BOCA', 'HUMAN_CORONA', 'METAPNEUMO', 'PARAINFLUENZA', 'RHINO', 'RSV', 'OTHERRESPVIRUS','OTHER_RESPVIRUS_DETAILS', 'LAB_RESULT_COMMENT', 'WCR_COMMENT', 'ISO2', 'ISOYW', 'MMWRYW']
influenza_df = influenza_df.drop(columns=columns_to_remove)

columns_to_convert = [
    'SPEC_PROCESSED_NB', 'AH1N12009', 'AH1', 'AH3', 'AH5', 'AH7N9',
    'ANOTSUBTYPED', 'ANOTSUBTYPABLE', 'AOTHER_SUBTYPE', 'INF_A', 'BVIC_2DEL', 'BVIC_3DEL', 'BVIC_NODEL', 'BVIC_DELUNK',
    'BYAM', 'BNOTDETERMINED', 'INF_B', 'INF_ALL', 'INF_NEGATIVE',

]

influenza_df[columns_to_convert] = influenza_df[columns_to_convert].apply(pd.to_numeric)

influenza_df = influenza_df.dropna(subset=['SPEC_PROCESSED_NB'])

columns_to_sum = [
    'INF_ALL', 'INF_NEGATIVE'
]

sum_of_columns = influenza_df[columns_to_sum].sum(axis=1)

influenza_df = influenza_df[sum_of_columns == influenza_df["SPEC_PROCESSED_NB"]]

sum_columns_set1 = influenza_df[['AH1N12009', 'AH1', 'AH3', 'AH5', 'AH7N9', 'ANOTSUBTYPED', 'ANOTSUBTYPABLE', 'AOTHER_SUBTYPE']].sum(axis=1)

sum_columns_set2 = influenza_df[['BVIC_2DEL', 'BVIC_3DEL', 'BVIC_NODEL', 'BVIC_DELUNK', 'BYAM', 'BNOTDETERMINED']].sum(axis=1)

influenza_df = influenza_df[(sum_columns_set1 == influenza_df['INF_A']) & (sum_columns_set2 == influenza_df['INF_B'])]

sum_inf_a_b = influenza_df["INF_A"] + influenza_df["INF_B"]

influenza_df = influenza_df[sum_inf_a_b == influenza_df["INF_ALL"]]

influenza_df = influenza_df[influenza_df['SPEC_PROCESSED_NB'] != 0]

influenza_df['ISO_WEEKSTARTDATE'] = pd.to_datetime(influenza_df['ISO_WEEKSTARTDATE'])

years_to_explore = [2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022]
filtered_df = influenza_df[influenza_df['ISO_YEAR'].isin(years_to_explore)].copy()

filtered_df['Month'] = filtered_df['ISO_WEEKSTARTDATE'].dt.month_name()
filtered_df['Year'] = filtered_df['ISO_YEAR']

month_order = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
filtered_df['Month'] = pd.Categorical(filtered_df['Month'], categories=month_order, ordered=True)

agg_df = filtered_df.groupby(['HEMISPHERE', 'Year', 'Month']).agg({'INF_ALL': 'sum'}).reset_index()

```

#### Explanation

First, the data is loaded from a CSV file, and missing values in specified columns are replaced with zeros. Unnecessary columns are then removed, and certain columns are converted to numeric types. Rows with missing values in a crucial column 'SPEC_PROCESSED_NB' (Specimen Processed for Influenza) are dropped. This column is crucial as it will help us in filtering the data which doesn't add up. The subsequent steps involve intricate filtering. Rows are retained where the sum of 'INF_ALL' (Total Positive Influenza Cases) and 'INF_NEGATIVE' (Total Negative Influenza Cases) matches the 'SPEC_PROCESSED_NB' (Specimen Processed for Influenza) value. Becuase if they don't match then there is something worng, therefore, it was decided that it is better to drop these rows. Similarly, further filtering is done to ensure that the sums of specific sets of columns containing subtypes of Influenza Type A and Influenza Type B align with their parent columns. A final filter is applied to keep only the rows where the sum of 'INF_A' (Influenza Type A) and 'INF_B' (Influenza Type B) equals the 'INF_ALL' (Total Influenza Cases) column. Additionally, rows with 'SPEC_PROCESSED_NB' (Specimen Processed for Influenza) values not equal to zero are retained. This data still had some columns and rows which needed to be processed. But we will discuss that in Final Chart's code explanation as they are closely linked together.

# Final Question

**Q. Has the relaxation of COVID-19 restrictions influenced the resurgence of influenza, and what patterns emerge when examining influenza cases both during and in the aftermath of pandemic-related lockdowns in Northern Hemisphere (NH) and Southern Hemisphere (SH)?**

# Final Chart

![CS625 Final Project Final Chart](CS625_Final_Project_Final_Chart.png)

## References

* First Dataset Raw, [dataset_1_raw.xls](dataset_1_raw.xls)
* Second Dataset EC Raw, [dataset_2_raw.xls](dataset_2_raw.xls)
* Python File, [CS_625_HW5.ipynb](CS_625_HW5.ipynb)
* First CSV (Boxplot, eCDF, Histogram, Scatter plot (Matplotlib), Barchart), [dataset1-boxplot-csv.csv](dataset1-boxplot-csv.csv)
* Second CSV (Choropleth, Scatter plot (Plotly)), [dataset1_popdensity.csv](dataset1_popdensity.csv)
* Seaborn, <https://seaborn.pydata.org/generated/seaborn.boxplot.html>
* Seaborn, <https://seaborn.pydata.org/generated/seaborn.ecdfplot.html>
* Seaborn, <https://seaborn.pydata.org/generated/seaborn.histplot.html>
* Plotly, <https://plotly.com/python/reference/layout/annotations/>
* Plotly, <https://plotly.com/python/text-and-annotations/>
* Plotly, <https://plotly.com/python/choropleth-maps/>
* Plotly, <https://plotly.com/python/line-and-scatter/>
* Medium, <https://lisandroabulatif.medium.com/create-charts-maps-and-scatter-matrix-with-plotly-and-google-colab-55a5303326ab>
* Youtube, <https://www.youtube.com/watch?v=oACIIEh6cgY>
* Youtube, <https://www.youtube.com/watch?v=sXuoikhChYo>
* Stackoverflow, <https://stackoverflow.com/questions/60199939/how-to-format-plotly-title-in-python-as-bold-when-the-title-is-a-variable>
* Stackoverflow, <https://stackoverflow.com/questions/71328058/add-more-than-two-variables-in-hover-text-of-plotly-object-with-more-than-one-tr>
* Stackoverflow, <https://stackoverflow.com/questions/71104827/plotly-express-choropleth-map-custom-color-continuous-scale>
* Stackoverflow, <https://stackoverflow.com/questions/50067301/make-plotly-annotation-font-bold>
* United States Census Bureau, <https://www.census.gov/library/publications/2009/compendia/statab/129ed/population.html>



