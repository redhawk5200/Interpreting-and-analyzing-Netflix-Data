<h1 align="center">Interpreting-and-analyzing-Netflix-Data</h1>

<p align="center">
  <img src="https://media.giphy.com/media/UoRR2d1b8xs04A2bV8/giphy.gif"></h1>
</p>
  
<h3>1. Loading the raw data from the CSV file </h3>
<br><br>
-I will first import the CSV file which contains about 8000 rows and 11 columns of data. Got this data from [kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows). Then print the first 5 rows so that you can inspect it.
</br>

<p></p>

```python
# Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

# Print the first five rows of the DataFrame
print(netflix_df[0:5])
```
|   | show_id |   type  | title |      director     |                        cast                       |    country    |     date_added    | release_year | duration |                    description                    |       genre      |
|:-:|:-------:|:-------:|:-----:|:-----------------:|:-------------------------------------------------:|:-------------:|:-----------------:|:------------:|:--------:|:-------------------------------------------------:|:----------------:|
| 0 | s1      | TV Show | 3%    | NaN               | João Miguel, Bianca Comparato, Michel Gomes, R... | Brazil        | August 14, 2020   | 2020         | 4        | In a future where the elite inhabit an island ... | International TV |
| 1 | s2      | Movie   | 7:19  | Jorge Michel Grau | Demián Bichir, Héctor Bonilla, Oscar Serrano, ... | Mexico        | December 23, 2016 | 2016         | 93       | After a devastating earthquake hits Mexico Cit... | Dramas           |
| 2 | s3      | Movie   | 23:59 | Gilbert Chan      | Tedd Chan, Stella Chung, Henley Hii, Lawrence ... | Singapore     | December 20, 2018 | 2011         | 78       | When an army recruit is found dead, his fellow... | Horror Movies    |

<h3>2. Filtering for movies. </h3>
<p>Okay, we have our data! Now we can dive in and start looking at movie lengths.

  Or can we? Looking at the first five rows of our new DataFrame, we notice a column <code>type</code>. Scanning the column, it's clear there are also TV shows in the dataset! Moreover, the <code>duration</code> column we planned to use seems to represent different values depending on whether the row is a movie or a show (perhaps the number of minutes versus the number of seasons)?
  
</p>

```python
# Subset the DataFrame for type "Movie"
netflix_df_movies_only = netflix_df[netflix_df.type=="Movie"]
# Select only the columns of interest
netflix_movies_col_subset=netflix_df_movies_only[['title','country','genre','release_year','duration']]
# Print the first five rows of the new DataFrame
print(netflix_movies_col_subset[0:5])
```
|   | title |    country    |     genre     | release_year | duration |
|:-:|:-----:|:-------------:|:-------------:|:------------:|:--------:|
| 1 | 7:19  | Mexico        | Dramas        | 2016         | 93       |
| 2 | 23:59 | Singapore     | Horror Movies | 2011         | 78       |
| 3 | 9     | United States | Action        | 2009         | 80       |
| 4 | 21    | United States | Dramas        | 2008         | 123      |
| 6 | 122   | Egypt         | Horror Movies | 2019         | 95       |

<h3>Creating a scatter plot of the data.</h3>
<p>Okay, now we're getting somewhere. We've read in the raw data, selected rows of movies, and have limited our DataFrame to our columns of interest. Let's try visualizing the data again to inspect the data over a longer range of time.</p>

```python
# Create a figure and increase the figure size
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus year
plt.scatter(netflix_movies_col_subset[["release_year"]],netflix_movies_col_subset[["duration"]])

# Create a title
plt.title('Movie Duration by Year of Release')

# Show the plot
plt.show()
```


<p align="center">
  <img src="https://github.com/redhawk5200/Interpreting-and-analyzing-Netflix-Data/blob/main/scatterplot.PNG![scatterplot](https://user-images.githubusercontent.com/59371949/167449370-d99e2206-9cb3-441d-935a-a68ef81f05a4.PNG)
"/>
</p>
