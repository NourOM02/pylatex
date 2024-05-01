# PyTabTex

Developped by a M. Eng. student in AI & Data science, who usually find himself preparing reports of projects using LaTex. This implies summarizing results in tables, as we can find in a lot of scientific papers. In the context of Machine Learning projects, the results are most probably  the output of a python code. So why copying them from python and have a painful time creating the table in LaTeX ?

The goal is to use python to translate these results directly into LaTeX format with a reasonable amount of customization while still working with Python!


## Key features
+ Work with multilevel column.
+ Load data from dataframe, csv file or dictionary.
+ Automatically highlight max/min by rows/cols.

## Installation

You can clone the repository or simply installing it from PyPI using `pip`
```bash
pip install pytabtex
```

## How to use
For the moment, the specific use case of this library is tables assembling results.

### Define columns:

The columns parameter is a dictionary where each key is the name of the columns, the value is 0 if there are no subcolulmns, or a list of subcolumns names if there are subcolumns.

**Example (simple columns) :**

Desired output :

![Simple columns](media/simple.png)

Python code :
```python
columns = {"column 1" : 0, "column 2" : 0, "column 3" : 0, "column 4" : 0}
```

**Example (multilevel columns) :**

Desired output :

![Multilevel columns](media/multilevel.png)

Python code :
```python
columns = {"column 1" : ["Sub-column 1", "Sub-column 2"],\
           "column 2" : 0,
           "column 3" : 0}
```

### Define body of the table

The body of the table can be a dictionary, a pandas Dataframe or a csv file path.

**Example**

![Body](media/body.png)

**Dictionary**

```python
{
    "id 1" : [29, 31, 90],
    "id 2" : [97, 78, 67]
}
```

**Dataframe**

if the dataframe has a header, don't include it.


|||||
|-|-|-|-|
|id 1|29|31|90|
|id 2|97|78|67|

**CSV file**

if the dataframe has a header, don't include it.

```python
csv_file = "path\to\csv"
```

### Create table

+ columns : columns defined in the format specified above.
+ body : table rows in one of the different formats.
+ title : title of the table if needed.
+ highlight : {func : axis} defined as follows - max by rows : {max: 0}, max by cols : {min: 0}, min by rows : {min: 0}, min by cols : {min: 1}
+ orientation : "P" for portrait and "L" for landscape
+ position of the table : htbp by default, check latex for other positions.
+ align cols : "c" center, "l" left, "r" right.

```python
from pytabtex import Table

table = Table(columns = columns,\
              body = body,\
              title=None,\
              highlight=None,\
              caption=None,\
              orientation="P",\
              position="htbp",\
              align_cols="c"
            )
```

## Use case examples

### Example 1

![Table 1](media/table_1.png)
src : [Zhenwen Li, Tao Xie Using LLM to select the right SQL Query from candidates](https://arxiv.org/pdf/2401.02115)

**Defintion of columns**

```python
"columns": { "Model" : 0, "Base":0, "10 MTS" : 0, "15 MTS": 0, "Fuzzing": 0, "SQLite Format" : 0, "7-shot" : 0, "9-shot" : 0 }
```

**Body from csv file**

open [data1.csv](tests/data1.csv)