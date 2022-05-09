<h1 align="center">Interpreting-and-analyzing-Netflix-Data</h1>

<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/0/08/Netflix_2015_logo.svg" width="500" />
</p>

<h3>1. Loading the raw data from the CSV file </h3>

```python
# Read in the CSV as a DataFrame
netflix_df = pd.read_csv("datasets/netflix_data.csv")

# Print the first five rows of the DataFrame
print(netflix_df[0:5])
```
