<h1 align="center">Interpreting-and-analyzing-Netflix-Data</h1>

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/0/08/Netflix_2015_logo.svg" width="500" />
</p>

<h3>1. Loading the raw data from the CSV file </h3>
<br><br>
-I will first import the CSV file which contains about 8000 rows and 11 columns of data. Got this data from [kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- :thinking: I’m currently open for: `An Intern` or a new `job opportunity`, this is [my Résumé](https://drive.google.com/file/d/1j4Khc23fEXEO1ydd5LGZpDej_RLeUFMl/view?usp=sharing).
<br>

```python
# Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

# Print the first five rows of the DataFrame
print(netflix_df[0:5])
```
