import pandas as pd

df = pd.read_csv('youfilenamehere.csv')


Use .head(), .tail(), .shape and .columns to explore your DataFrame and find out the number of rows and columns as well as the column names.

Look for NaN (not a number) values with .findna() and consider using .dropna() to clean up your DataFrame.

You can access entire columns of a DataFrame using the square bracket notation: df['column name'] or df[['column name 1', 'column name 2', 'column name 3']]

You can access individual cells in a DataFrame by chaining square brackets df['column name'][index] or using df['column name'].loc[index]

The largest and smallest values, as well as their positions, can be found with methods like .max(), .min(), .idxmax() and .idxmin()

You can sort the DataFrame with .sort_values() and 

add new columns with .insert()

future_releases = data[data.Release_Date >= scrape_date]
future_releases
data_clean = data.drop(future_releases.index)
data_clean

To create an Excel Style Pivot Table by grouping entries that belong to a particular category use the .groupby() method


used .groupby() to explore the number of posts and entries per programming language

new_df.groupby("TAG").sum()

df_apps_clean[["App", "Installs"]].groupby("Installs").count()

clean_df['Mid-Career 90th Percentile Salary'].subtract(clean_df['Mid-Career 10th Percentile Salary'])

converted strings to Datetime objects with to_datetime() for easier plotting

reshaped our DataFrame by converting categories to columns using .pivot()

used .count() and isna().values.any() to look for NaN values in our DataFrame, which we then replaced using .fillna()
use df_data.isna().sum() to show how many NaN values there are in each column of dataframe df_data

created (multiple) line charts using .plot() with a for-loop

styled our charts by changing the size, the labels, and the upper and lower bounds of our axis.

added a legend to tell apart which line is which by colour

smoothed out our time-series observations with .rolling().mean() and plotted them to better identify trends over time.

roll_df = reshaped_df.rolling(window=6).mean()

df_roll_unemployment = df_unemployment[["UE_BENEFITS_WEB_SEARCH","UNRATE"]].rolling(window=6).mean()

colors_df['is_trans'].value_counts() is the same as colors_df.groupby('is_trans').count(), kinda

colors_df['is_trans'].value_counts()['f'] to show just the falses


filtering our DataFrame on a condition. We are retrieving the rows where the year column has the value 1949: sets['year'] == 1949.

Aggregate Data with the Python .agg() Function
Let's work out the number of different themes shipped by year. This means we have to count the number of unique theme_ids per calendar year.
Note, the .agg() method takes a dictionary as an argument. In this dictionary, we specify which operation we'd like to apply to each column. In our case, we just want to calculate the number of unique entries in the theme_id column by using our old friend, the .nunique() method. 
themes_by_year = sets_df.groupby('year').agg({'theme_id': pd.Series.nunique})

df_free_vs_paid = df_apps_clean.groupby(["Category", "Type"], as_index=False).agg({"App": pd.Series.count})
df_free_vs_paid.sort_values("App").head()

no_of_prizes = df_data.groupby(["year"], as_index=False).agg({"prize": pd.Series.count})

In this lesson we looked at how to:

use HTML Markdown in Notebooks, such as section headings # and how to embed images with the <img> tag.

combine the groupby() and count() functions to aggregate data

use the .value_counts() function

slice DataFrames using the square bracket notation e.g., df[:-2] or df[:10]

use the .agg() function to run an operation on a particular column

rename() columns of DataFrames

create a line chart with two separate axes to visualise data that have different scales.

create a scatter plot in Matplotlib

work with tables in a relational database by using primary and foreign keys

.merge() DataFrames along a particular column

create a bar chart with Matplotlib

plt.figure(figsize=(16,8), dpi=200)
plt.title('Number of Nobel Prizes Awarded per Year', fontsize=18)
plt.yticks(fontsize=14)
plt.xticks(ticks=five_year_ticks, 
           fontsize=14, 
           rotation=45)

ax1 = plt.gca()
ax2 = ax1.twinx()

    How to use .describe() to quickly see some descriptive statistics at a glance.

    How to use .resample() to make a time-series data comparable to another by changing the periodicity.

    How to work with matplotlib.dates Locators to better style a timeline (e.g., an axis on a chart).

    How to find the number of NaN values with .isna().values.sum()

    How to change the resolution of a chart using the figure's dpi

    How to create dashed '--' and dotted '-.' lines using linestyles

    How to use different kinds of markers (e.g., 'o' or '^') on charts.

    Fine-tuning the styling of Matplotlib charts by using limits, labels, linewidth and colours (both in the form of named colours and HEX codes).

    Using .grid() to help visually identify seasonality in a time series.


Total number of installs each app category has:

cat_number = df_apps_clean.Category.value_counts()
print(cat_number.head())

cat_merged = df_apps_clean.groupby("Category").agg({"App": pd.Series.count, "Installs": pd.Series.sum}).sort_values("Installs", ascending=False)
cat_merged.head()


Alternatively:
cat_number = df_apps_clean.groupby('Category').agg({'App': pd.Series.count})
cat_merged_df = pd.merge(cat_number, category_installs, on='Category', how="inner")
print(f'The dimensions of the DataFrame are: {cat_merged_df.shape}')
cat_merged_df.sort_values('Installs', ascending=False)

Pull a random sample from a DataFrame using .sample()

How to find duplicate entries with .duplicated() and .drop_duplicates()

duplicated_rows = df_apps_clean[df_apps_clean.duplicated()]

How to convert string and object data types into numbers with .to_numeric()

How to use plotly to generate beautiful pie, donut, and bar charts as well as box and scatter plots 

genre_bar = px.bar(top_genres, x=top_genres.index, y=top_genres.values, color=top_genres.values, color_continuous_scale="Agsunset")
genre_bar.update_layout(xaxis_title="Number of Apps", yaxis_title="Genre", title="Top Genres", coloraxis_showscale=False)

genre_bar.show()


    Use nested loops to remove unwanted characters from multiple columns

    Filter Pandas DataFrames based on multiple conditions using both .loc[] and .query()

    Create bubble charts using the Seaborn Library

    Style Seaborn charts using the pre-built styles and by modifying Matplotlib parameters

    Use floor division (i.e., integer division) to convert years to decades

    Use Seaborn to superimpose a linear regressions over our data

    Make a judgement if our regression is good or bad based on how well the model fits our data and the r-squared metric

    Run regressions with scikit-learn and calculate the coefficients. 


world_map.update_layout(coloraxis_showscale=True,)

import numpy as np

# Create locators for ticks on the time axis
year = mdates.YearLocator()
months = mdates.MonthLocator() 
years_fmt = mdates.DateFormatter('%Y')


Doing cumsum

prize_by_year = df_data.groupby(by=['birth_country_current', 'year'], as_index=False).count()
prize_by_year = prize_by_year.sort_values('year')[['year', 'birth_country_current', 'prize']]
cumulative_prizes = prize_by_year.groupby(by=['birth_country_current', 'year']).sum().groupby(level=[0]).cumsum()
print(cumulative_prizes)
cumulative_prizes.reset_index(inplace=True) 

I used Colabotory but you could also use Jupyter