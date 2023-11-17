# Pandas-Countries.csv-Dataset

import pandas as pd

countries_df = pd.read_csv('countries.csv')
countries_df

countries_df.shape

num_countries = countries_df.shape
print(f'There are {num_countries} in dataset')

num_countrie = countries_df.name
num_countrie

print(f'{num_countrie} in dataset')

# retrieve a list of contents from the dataset?

continents = countries_df.columns
continents

# what is the total latitude of all the listed in the dataset

total_latitude = countries_df.latitude.sum()
print(f'The total latitude is {total_latitude}')

# what is the overall life expectaion in the world

life_expect_mean = countries_df.latitude.mean()
life_expect_median = countries_df.latitude.median()

print(f'life expectation of mean {life_expect_mean} and meadian {life_expect_median}')

# 10 highest countries latitude

most_latitude_df = countries_df.sort_values('latitude', ascending=False).head(10)
most_latitude_df

countries_df['gdp'] = countries_df.longitude / countries_df.latitude
countries_df

lowest_gdp = countries_df.sort_values('gdp', ascending=True)
lowest_gdp

# Creat the data frame that counts the numbers countries in each continent?

countries_count_df = countries_df.groupby('name')[['region_id', 'subregion_id', 'latitude', 'longitude']].count()
countries_count_df

countries_df_sum = countries_df.groupby('name')[['region_id', 'subregion_id', 'latitude', 'longitude']].sum()
countries_df_sum

covid_data_df = pd.read_csv('country_wise_latest.csv')
covid_data_df

total_test_missing = covid_data_df.Active.isna()
total_test_missing

# merged data set

combined_df = countries_df.merge(covid_data_df, left_on='name', right_on='Country/Region')
combined_df

combined_df['test_per_million'] = combined_df['Deaths / 100 Cases'] * 1e6 / combined_df['Confirmed last week']
combined_df['cases_per_million'] = combined_df['Recovered / 100 Cases'] * 1e6 / combined_df["Confirmed last week"]
combined_df['deaths_per_million'] = combined_df['Deaths / 100 Recovered'] * 1e6 / combined_df['Confirmed last week']
combined_df

# highest test per million

highest_test_df = combined_df.sort_values('test_per_million', ascending=False).head(10)
highest_test_df

highest_cases_df = combined_df.sort_values('cases_per_million', ascending=False).head(10)
highest_cases_df

higest_deaths_df = combined_df.sort_values('deaths_per_million', ascending=False).head(10)
higest_deaths_df

highest_test_per_million = combined_df.test_per_million.count()
highest_test_per_million

highest_deaths_per_million = combined_df.deaths_per_million.count()
highest_deaths_per_million

combined_df.columns

