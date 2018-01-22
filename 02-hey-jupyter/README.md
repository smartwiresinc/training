# Hey Jupyter

## Introduction

Jupyter Notebooks provide an interactive, web-based graphical interface for
processing and analyzing data, similar to proprietary software products like
MATLAB, Mathematica, and Maple. Jupyter is designed with with an architecture
that supports multiple programming languages (the project name comes from
[Julia](https://en.wikipedia.org/wiki/Julia_(programming_language)),
[Python](https://en.wikipedia.org/wiki/Python_(programming_language)), and
[R](https://en.wikipedia.org/wiki/R_(programming_language)), three of the
first languages supported on the platform). This architecture separates the
interface (running in the browser) from the execution environment (called
the _kernel_).

Python is a popular choice among data scientists due to its simplicity and
large ecosystem of numeric and statistical computing libraries. We will use
the [Python Data Analysis Library](https://pandas.pydata.org), also called
_pandas_, to explore a power system model.

## Key Concepts

1. **Cells**: Jupyter organizes documents into _cells_, which can contain
   rich text in [Markdown](https://en.wikipedia.org/wiki/Markdown) format,
   code, or the result of executed code. When a code-containing cell is
   executed via the _Run Cell_ command, the input and output are assigned
   a execution order indicator.
   
   For example, a cell marked marked `In [20]` means that the cell was last
   executed _after_ any cell numbered 19 or less, and _before_ any cell
   numbered 20 or more. It is often helpful to use the **Cell > Run All**
   menu option to ensure that all cells are up-to-date.

1. **Data Frames**: _pandas_ manages data in a tabular format called Data
   Frames, where the rows define individual records and the columns define
   various properties of the record (for example, a Person record might
   have columns labelled Name, Date of Birth, Birth Location, etc.) Input
   data is first read into data frames, and a set of built-in functions
   can be used to sort, filter, or otherwise process the data as needed.

## Exercises

### Hello World

Start the Jupyter Notebook server. Depending on your installation method,
there may be a "Jupyter Notebook" application, or you can open a terminal
(such as Command Prompt on Windows) and run `jupyter notebook`.
  
Running the command should open your default browser and navigate to the
running Jupyter instance on your local system, but if it doesn't, the
system should print a special URL to copy/paste into your browser:
   
```bash
$ cd /c/projects/training/02-hey-jupyter
$ jupyter notebook
[I 10:18:00.711 NotebookApp] Serving notebooks from local directory: C:\projects\training\02-hey-jupyter
[I 10:18:00.711 NotebookApp] 0 active kernels
[I 10:18:00.711 NotebookApp] The Jupyter Notebook is running at:
[I 10:18:00.711 NotebookApp] http://localhost:8888/?token=3635b10886fafde18eb8dc781639b068b00299b99ff76aa4
[I 10:18:00.711 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 10:18:00.714 NotebookApp]

    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://localhost:8888/?token=3635b10886fafde18eb8dc781639b068b00299b99ff76aa4
[I 10:18:00.987 NotebookApp] Accepting one-time-token-authenticated connection from ::1
```

The interface should show a list of all files in this directory.

### My First Notebook

Open the `scigrid.ipynb` file and execute all the cells. The CSV files
containing information about terminal nodes (such as substations) and
transmission lines should appear.

> Aside: The .ipynb extension refers to IPython, or Interactive Python,
> a predecessor to Jupyter.

### Count Records

Let's determine the number of substations in this dataset. Filter the
`terminals` data frame for entries with a `typ` of "substation":

```python
substations = terminals[terminals["typ"] == "substation"]
substations.head()
```

To determine a count, output `len(substations)` instead.

### Summary Statistics

_pandas_ provides tools for summary statistics. For example, to determine
the number of branches at each voltage level, we can use:

```python
branches.groupby(by="voltage").size()
```

Answer the following questions:

1. What is the most common voltage level for substations? For simplicity,
   ignore stations tha tlist multiple voltage levels.

1. How many unique transmission system operators are captured in this
   dataset? For simplicity, consider co-owned lines to be a separate
   operator.

   _Hint_: The results of a grouping for branches and terminals will
   need to be added together, unless you used a `merge` operation.

1. How many transmission lines are longer than 10km?

1. What are the two most common resistance/km values?

### Derived Values

We can derive new columns based on values of existing columns. For example,
to determine total resistance of a given line segment, we can use:

```python
branches["r_total"] = branches["r_ohmkm"] * (branches["length_m"] / 1000)
branches.head()
```

1. Which line has the largest total resistance?

1. What are the lines with the 10 largest X/R ratios? 10 smallest?

1. Which line has the highest total impedance? (magnitude only)

### Create a Pull Request

Save your Jupyter notebook with these exercises and create a Pull Request
containing your updated notebook. Remember to separate the exercises using
headers and/or short descriptions.

## License

Power system model data (`*.csv` files) is provided courtesy of the
[SciGRID project](http://www.scigrid.de/), and is used under the terms of the
[Open Database License](http://opendatacommons.org/licenses/odbl/1.0/). A
copy of the license is included as `LICENSE` in this directory.

## See Also

* [Pandas Cheat Sheet](https://github.com/pandas-dev/pandas/blob/master/doc/cheatsheet/Pandas_Cheat_Sheet.pdf):
  a listing of common tasks, commands, and outputs
* [10-minute tour of pandas](https://pandas.pydata.org/#quick-vignette)
