# Better-Spark-Show

Small Function that displays Sparks .show() in a better UI (similar to Pandas) in a notebook

## [Code](https://github.com/JohnSesana/Better-Spark-Show/blob/main/better_show.py)

```python
from IPython.display import HTML


def better_show(df, num_rows=50):
    """
    Display a PySpark DataFrame as an HTML table in Jupyter notebook.

    Parameters:
    df (DataFrame): The PySpark DataFrame to display.
    num_rows (int): Number of rows to display. Default is 50.
    """
    # Collect the specified number of rows as a list of dictionaries
    rows = df.limit(num_rows).collect()

    # Create an HTML table string with column headers
    html = "<table border='1'><tr>" + "".join([f"<th>{col}</th>" for col in df.columns]) + "</tr>"

    # Add the rows to the table
    for row in rows:
        html += "<tr>" + "".join([f"<td>{value}</td>" for value in row]) + "</tr>"

    html += "</table>"

    # Display the HTML table
    return HTML(html)
```

## Usage Example

```python
# Your spark context

spark_df = spark.read.format("orc").load(your_table) # Change the format as you need

better_show(spark_df, 15) # By default shows 50 rows
```
