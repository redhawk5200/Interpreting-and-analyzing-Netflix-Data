<h1 align="center">Interpreting-and-analyzing-Netflix-Data</h1>

<p align="center">
  <img src="https://media.giphy.com/media/UoRR2d1b8xs04A2bV8/giphy.gif"></h1>
</p>
  
<h3>1. Loading the raw data from the CSV file </h3>
<br>
I will first import the CSV file which contains about 8000 rows and 11 columns of data. Got this data from [kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows). Then print the first 5 rows so that you can inspect it.
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
<br>
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
<br>
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
![scatterplot](https://user-images.githubusercontent.com/59371949/167449480-635fbbf8-6b52-42e6-803b-3da3d627bd2a.PNG)

<h3>4. Digging deeper </h3>![coloredscatter](https://user-images.githubusercontent.com/59371949/167663121-f2d238dc-104f-45c9-88a4-10d81087a419.PNG)

<br>
<p>Upon further inspection, something else is going on. Some of these films are under an hour long! Let's filter our DataFrame for movies with a duration under 60 minutes and look at the genres. This might give us some insight into what is dragging down the average.</p>

```python
# Filter for durations shorter than 60 
lessixty=netflix_movies_col_subset['duration']
short_movies = netflix_movies_col_subset[lessixty<60]

# Print the first 20 rows of short_movies
print(short_movies[0:20])
```

|     |                       title                       |    country    |     genre     | release_year | duration |
|:---:|:-------------------------------------------------:|:-------------:|:-------------:|:------------:|:--------:|
|  35 | #Rucker50                                         | United States | Documentaries | 2016         | 56       |
|  55 | 100 Things to do Before High School               | United States | Uncategorized | 2014         | 44       |
|  67 | 13TH: A Conversation with Oprah Winfrey & Ava ... | NaN           | Uncategorized | 2017         | 37       |
| 101 | 3 Seconds Divorce                                 | Canada        | Documentaries | 2018         | 53       |
| 146 | A 3 Minute Hug                                    | Mexico        | Documentaries | 2019         | 28       |

<p>Could not print the whole data as it was a lot to print here.</p>

<p>Interesting! It looks as though many of the films that are under 60 minutes fall into genres such as "Children", "Stand-Up", and "Documentaries". This is a logical result, as these types of films are probably often shorter than 90 minute Hollywood blockbuster</p>

<h3>5. Marking non-feature films</h3>
<br>
<p>We could eliminate these rows from our DataFrame and plot the values again. But another interesting way to explore the effect of these genres on our data would be to plot them, but mark them with a different color.

In Python, there are many ways to do this, but one fun way might be to use a loop to generate a list of colors based on the contents of the genre column. Much as we did in Intermediate Python, we can then pass this list to our plotting function in a later step to color all non-typical genres in a different color!
</p>

```python
# Define an empty list
colors = []

# Iterate over rows of netflix_movies_col_subset
for lab, row in netflix_movies_col_subset.iterrows():
    if row['genre']=="Children" :
        colors.append('red')
    elif row['genre']=="Documentaries" :
        colors.append('blue')
    elif row['genre']=="Stand-Up" :
        colors.append('green')
    else:
        colors.append('black')
        
# Inspect the first 10 values in your list        
print(colors[0:11])
```
['black', 'black', 'black', 'black', 'black', 'black', 'black', 'black', 'black', 'blue', 'black']

<h3>Plotting with color!</h3>
<br>
<p>Lovely looping! We now have a colors list that we can pass to our scatter plot, which should allow us to visually inspect whether these genres might be responsible for the decline in the average duration of movies.</pr>

```python
# Set the figure style and initalize a new figure
plt.style.use('fivethirtyeight')
fig = plt.figure(figsize=(12,8))

# Create a scatter plot of duration versus release_year
plt.scatter(netflix_movies_col_subset[["release_year"]],netflix_movies_col_subset[["duration"]], c=colors)

# Create a title and axis labels
plt.xlabel('Release Year')
plt.ylabel('Duration (min)')
plt.title('Movie duration by year of release')

# Show the plot
plt.show()
```


