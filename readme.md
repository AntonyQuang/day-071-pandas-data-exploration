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

used .count() and isna().values.any() to look for NaN values in our DataFrame (this returns True or False), which we then replaced using .fillna()
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

ax1.plot(df_tesla.MONTH, df_tesla["TSLA_USD_CLOSE"], color="#ff3308", linewidth=1)
ax2.plot(df_tesla.MONTH, df_tesla["TSLA_WEB_SEARCH"], color="blue", linewidth=1)

ax1.set_ylabel('TSLA Stock price', color='#ff3308', fontsize=14)

ax2.set_ylabel('Search Trend', color='blue', fontsize=14)

ax1.set_ylim([0, 600]) 

ax1.set_xlim([df_tesla.MONTH.min(), df_tesla.MONTH.max()])

ax1.grid(color="gray", linestyle="--")

format the ticks
ax1.xaxis.set_major_locator(year)
ax1.xaxis.set_major_formatter(years_fmt)
ax1.xaxis.set_minor_locator(months)

plt.show()

from pandas.plotting import register_matplotlib_converters
register_matplotlib_converters()

Create locators for ticks on the time axis

year = mdates.YearLocator()
months = mdates.MonthLocator() 
years_fmt = mdates.DateFormatter('%Y')

ax1.xaxis.set_major_locator(year)
ax1.xaxis.set_major_formatter(years_fmt)
ax1.xaxis.set_minor_locator(months)

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

#A
top_cities = df_data.groupby("organization_city", as_index=False).agg({"prize": pd.Series.count})
top_cities.sort_values("prize", ascending=True, inplace=True)
#B
birthplaces = df_data["birth_city"].value_counts()[:20]
birthplaces.sort_values(ascending=True, inplace=True)
#A similar result to B

Add a separate line for sort_values, you can't combine it in one line

Pull a random sample from a DataFrame using .sample()

How to find duplicate entries with .duplicated() and .drop_duplicates()

duplicated_rows = df_apps_clean[df_apps_clean.duplicated()]
df_yearly.duplicated().values.any() returns True or False (Answers whether there are any duplicates)

How to convert string and object data types into numbers with .to_numeric()

How to use plotly to generate beautiful pie, donut, and bar charts as well as box and scatter plots 

genre_bar = px.bar(top_genres, x=top_genres.index, y=top_genres.values, color=top_genres.values, color_continuous_scale="Agsunset")
genre_bar.update_layout(xaxis_title="Number of Apps", yaxis_title="Genre", title="Top Genres", coloraxis_showscale=False)

genre_bar.show()

sun_plot = px.sunburst(sunburst, path=["organization_country", "organization_city", "organization_name"], values="prize")
sun_plot.show()


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

Making another column
df_data[df_data['winning_age']== df_data['winning_age'].min()]

Doing cumsum

prize_by_year = df_data.groupby(by=['birth_country_current', 'year'], as_index=False).count()
prize_by_year = prize_by_year.sort_values('year')[['year', 'birth_country_current', 'prize']]
cumulative_prizes = prize_by_year.groupby(by=['birth_country_current', 'year']).sum().groupby(level=[0]).cumsum()
print(cumulative_prizes)
cumulative_prizes.reset_index(inplace=True) 

Doing Seaborn's Histograms
plt.figure(figsize=(8, 4), dpi=200)
sns.histplot(df_data, x="winning_age", bins=10)
plt.xlabel('Winning Age')
plt.ylabel('Count')
plt.show()

Doing Seaborn's regression plot: regplot
plt.figure(figsize=(8, 4), dpi=200)
with sns.axes_style("whitegrid"):
  sns.regplot(data=df_data,
              y=df_data.winning_age,
              x=df_data.year,
              lowess=True,
              scatter_kws = {'alpha': 0.4},
              line_kws={'color': 'black'})
  plt.xlabel('Year')
  plt.ylabel('Winning Age')
  plt.title('Changes in Winning Age over Time')
plt.show()


Doing Seaborn's boxplot: boxplot

plt.figure(figsize=(8, 4), dpi=200)
with sns.axes_style("whitegrid"):
  sns.boxplot(data=df_data,
              y=df_data.winning_age,
              x=df_data.category)
  plt.xlabel('Category')
  plt.ylabel('Winning Age')
  plt.title('Winning Age in Categories')
plt.show()


Doing Seaborn's lineplot: lmplot

plt.figure(figsize=(8, 4), dpi=200)
with sns.axes_style("whitegrid"):
  sns.lmplot(data=df_data,
             y="winning_age",
             x="year",
             row="category",
             lowess=True,
             scatter_kws = {'alpha': 0.4},
             line_kws = {'color': 'black'})
  plt.xlabel('Year')
  plt.ylabel('Winning Age')
  plt.title('Changes in Winning Age over Time')
plt.show()

bw_line, = plt.plot(before_washing.date, 
                    before_washing.pct_deaths,
                    color='black', 
                    linewidth=1, 
                    linestyle='--', 
                    label='Before Handwashing')
aw_line, = plt.plot(after_washing.date, 
                    after_washing.pct_deaths, 
                    color='skyblue', 
                    linewidth=3, 
                    marker='o',
                    label='After Handwashing')
plt.legend(handles=[bw_line, aw_line],
           fontsize=18)


To create the legend, we supply a label to the .plot() function and capture return value in a variable. It's important to notice that .plot() returns more than one thing, so we need to use a comma (,) since we're only grabbing the first item. We can then feed these handles into plt.legend(). 


KDE:

plt.figure(dpi=200)
# By default the distribution estimate includes a negative death rate!
sns.kdeplot(df_before.pct_deaths, fill=True, clip=(0,100))
sns.kdeplot(df_after.pct_deaths, fill=True, clip=(0,100))
plt.title('Est. Distribution of Monthly Death Rate Before and After Handwashing')
plt.xlim(0, 40)
plt.show()

Use a t-test to determine if the differences in the means are statistically significant or purely due to chance.

If the p-value is less than 1% then we can be 99% certain that handwashing has made a difference to the average monthly death rate.

from scipy import stats

stats.ttest_ind(df_before.pct_deaths, df_after.pct_deaths)

I used Colabotory but you could also use Jupyter