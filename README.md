<h1 align="center">Interpreting-and-analyzing-Netflix-Data</h1>

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/0/08/Netflix_2015_logo.svg" width="500" />
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
