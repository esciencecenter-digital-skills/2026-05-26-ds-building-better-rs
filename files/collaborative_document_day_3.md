![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document Day 3

2026-05-26 Building Better Research Software

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------

This is the Document for today: https://edu.nl/eavf3

Collaborative Document day 1: https://edu.nl/vqn8u

Collaborative Document day 2: https://edu.nl/8avvk

Collaborative Document day 3: https://edu.nl/eavf3

Collaborative Document day 4: https://edu.nl/v4ugn

##  🫱🏽‍🫲🏻 Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.

 If you feel that the code of conduct is breached, please talk to one of the instructors (if the complaint is for one of the participants) or send an email to training@esciencecenter.nl (if the complaint is for one of the instructors).

## 🎓 Certificate of attendance

If you attend the full workshop you can request a certificate of attendance by emailing to training@esciencecenter.nl.
Please request your certificate within 8 months after the workshop, as we will delete all personal identifyable information after this period.

## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, raise your hand in zoom. Click on the icon labeled "Reactions" in the toolbar on the bottom center of your screen,
then click the button 'Raise Hand ✋'. For urgent questions, just unmute and speak up!

You can also ask questions or type 'I need help' in the chat window and helpers will try to help you.
Please note it is not necessary to monitor the chat - the helpers will make sure that relevant questions are addressed in a plenary way.
(By the way, off-topic questions will still be answered in the chat)

https://codimd.carpentries.org/1Hlmt-V_RpuQWDv7RHCeWg?both
## 🖥 Workshop website

[link](https://esciencecenter-digital-skills.github.io/2026-05-26-ds-building-better-rs/)

🛠 Setup

[link](https://carpentries-incubator.github.io/better-research-software/installation-instructions.html)

Download files

[Spacewalks data and analysis code](https://github.com/carpentries-incubator/better-research-software/raw/refs/heads/main/learners/spacewalks.zip)

## 👩‍🏫👩‍💻🎓 Instructors

Jaro Camphuijsen, Sander van Rijn, Ou Ku

## 🧑‍🙋 Helpers

Jaro Camphuijsen, Sander van Rijn, Ou Ku


## 🗓️ Agenda
|  Time | Topic                         |
| -----:|:----------------------------- |
| 09:30 | Welcome, icebreaker and recap |
| 09:45 | Code structure                |
| 10:45 | **Coffee break**              |
| 11:00 | Code structure                |
| 11:30 | Code correctness & testing    |
| 12:00 | **Tea break**                 |
| 12:15 | Code correctness & testing    |
| 12:45 | Wrap-up                       |
| 13:00 | END                           |


## 🔧 Exercises

### Add comments to our code that separate blocks of functionality (5 min)
Add comments (start the line with a `#` to make it a comment) in your code to separate your code out into (4 or 5) useful conceptual blocks and describe what each of them does.

### Make a function called `main` (5 min)
Put the remaining lines of code into a new function called `main`. Provide function arguments and call it somewhere.

### Project restructuring (8 min)
Restructure your software project so that input data is stored in data/ directory and results (the graph and CSV data files) saved in results/ directory off the project root.

Remove current result files eva-data.csv and cumulative_eva_graph.png from the project root (if they exist) as they will be recreated by re-running the code.

Remember to create the results/ empty directory before running the code or your code will fail.

### Limitations of manual testing (3mins)
If we only ensure the correctness by executing the software, what are the limitations/downsides?

* Not exploring all possible options like wrong inputs/extreme cases/ different python versions bugs (packages not yet deployed for those python versions)
* No test for change of dataset
* Environment version missmatch
* The graph could appear but show incorrect results

## 🧠 Collaborative Notes

### ⌨️ Code Snapshot: Continue From Here

Last week, we discussed using (trusted) external libraries rather than doing everything yourself. We will continue with the code as it is below, which has replaced the pure python implementation with one relying on [pandas](https://pandas.pydata.org) functionality.

```bash
(venv_spacewalks) $ python3 -m pip install pandas
```


```python=
import matplotlib.pyplot as plt
import pandas as pd

# Data source: https://data.nasa.gov/resource/eva.json (with modifications)
input_file = './eva_data.json'
output_file = './eva_data.csv'
graph_file = './cumulative_eva_graph.png'
eva_df = pd.read_json(input_file, convert_dates=['date'], encoding='ascii')
eva_df['eva'] = eva_df['eva'].astype(float)
eva_df.dropna(axis=0, subset=['duration', 'date'], inplace=True)
eva_df.to_csv(output_file, index=False, encoding='utf-8')
eva_df.sort_values('date', inplace=True)
eva_df['duration_hours'] = eva_df['duration'].str.split(":").apply(lambda x: int(x[0]) + int(x[1])/60)
eva_df['cumulative_time'] = eva_df['duration_hours'].cumsum()
plt.plot(eva_df['date'], eva_df['cumulative_time'], 'ko-')
plt.xlabel('Year')
plt.ylabel('Total time spent in space to date (hours)')
plt.tight_layout()
plt.savefig(graph_file)
plt.show()
```


### Preparation for today (see the code snapshot above)
1. Activate virtual environment: `source .venv/bin/activate`
2. Install the pandas library: `pip install pandas`. (You can verify with `pip list`)
3. Copy past the above code snapshot into your version of `eva_data_analysis.py`, replacing the old code.
4. Verify your `eva_data_analysis.py` can run by running `python eva_data_analysis.py`. A plot should show up. A csv file `eva_data.csv` and a png file `cumulative_eva_graph.png` should be generated.


### Gitignore
Create a new file with filename `.gitignore` in the root of your git repository (for our workshop this is inside the directory called `spacewalks`).
Any file pattern we put in here will be ignored by git.

Add the following lines in:

```
eva_data.csv
*.png
.DS_store
```

Commit and push this .gitignore file to your git repository to keep track of the changes in this document as well.

The `.venv` or `venv_spacewalks` folder, which contains our virtual environment, also has a `.gitignore` file, with a `*`, making this folder igores itself and all sub-folders in it.

### Code structures

We separate the code we have into functional blocks of code. First we just add some comments to separate lines that conceptually belong together.


```python=
import matplotlib.pyplot as plt
import pandas as pd

# filenames
# Data source: https://data.nasa.gov/resource/eva.json (with modifications)
input_file = './eva_data.json'
output_file = './eva_data.csv'
graph_file = './cumulative_eva_graph.png'

# load and clean data
eva_df = pd.read_json(input_file, convert_dates=['date'], encoding='ascii')
eva_df['eva'] = eva_df['eva'].astype(float)
eva_df.dropna(axis=0, subset=['duration', 'date'], inplace=True)
eva_df.sort_values('date', inplace=True)

eva_df.to_csv(output_file, index=False, encoding='utf-8')

# compute duration
eva_df['duration_hours'] = eva_df['duration'].str.split(":").apply(lambda x: int(x[0]) + int(x[1])/60)
eva_df['cumulative_time'] = eva_df['duration_hours'].cumsum()
plt.plot(eva_df['date'], eva_df['cumulative_time'], 'ko-')

# plotting code
plt.xlabel('Year')
plt.ylabel('Total time spent in space to date (hours)')
plt.tight_layout()
plt.savefig(graph_file)
plt.show()
```

Next we actually create the functions:

```python=
def read_json_to_clean_dataframe(file_name):
    df = pd.read_json(file_name, convert_dates=['date'], encoding='ascii')
    df['eva'] = df['eva'].astype(float)
    df.dropna(axis=0, subset=['duration', 'date'], inplace=True)
    df.sort_values('date', inplace=True)
    return df
```

Some notes:
- Make sure to add return values to your functions
- Use clear and concise function names
- Rething your variable names inside your function, they now live in a smaller (and perhaps more generic) context and therfore might need a change of name
- This also helps to avoid clashes with global variables
- To change the local variable name inside the function, you can double click `eva_df` in the function, press F2, and rename the variable only in the function

This function can be called as:

```python=
eva_df = read_json_to_clean_dataframe(input_file)
```

The next line, where the csv is written, does not have to be separated out into its own function because it is a single line with clear functionality.

```python=
def compute_durations(df):
    df_copy = df.copy()
    df_copy['duration_hours'] = df_copy['duration'].str.split(":").apply(lambda x: int(x[0]) + int(x[1])/60)
    df_copy['cumulative_time'] = df_copy['duration_hours'].cumsum()
    return df_copy
```
- Here we made a copy of our input argument dataframe to avoid changing the original dataframe unintentionally. At the end we return the newly created copy, this is called a pure function.

:::warning
<details>
<summary><b>Pure and impure functions</b></summary>

Pure fuctions are functions that do not modify the input arguements. It is recommended to write pure functions in Python, since it's easier to read and maintain, and does not create unexpected behavior. Below is an impure function example, which modifies the input `df`:

```python=
def compute_durations(df):
    df['duration_hours'] = df['duration'].str.split(":").apply(lambda x: int(x[0]) + int(x[1])/60)
    df['cumulative_time'] = df['duration_hours'].cumsum()
```

Since it directly modifies `df`, you do not need to return it.

</details>
:::

This function can be called as:

```python=
eva_df = compute_durations(eva_df)
```

We see a lambda function being applied to the df. To make it more informative, we can separate this function out as a new function:

```python=
def text_to_duration(duration):
    hours, minutes = duration.split(":")
    duration = int(hours) + int(minutes)/60
    return duration
```

Then use this function to replace the lambda function:

```python=
def compute_durations(df):
    df_copy = df.copy()
    df_copy['duration_hours'] = df_copy['duration'].str.split(":").apply(text_to_duration)
    df_copy['cumulative_time'] = df_copy['duration_hours'].cumsum()
    return df_copy
```


Our code state in `eva_data_analysis.py` now:

```python=
import matplotlib.pyplot as plt
import pandas as pd

# filenames
# Data source: https://data.nasa.gov/resource/eva.json (with modifications)
input_file = './eva_data.json'
output_file = './eva_data.csv'
graph_file = './cumulative_eva_graph.png'

def read_json_to_clean_dataframe(file_name):
    df = pd.read_json(input_file, convert_dates=['date'], encoding='ascii')
    df['eva'] = df['eva'].astype(float)
    df.dropna(axis=0, subset=['duration', 'date'], inplace=True)
    df.sort_values('date', inplace=True)
    return df

def text_to_duration(duration):
    hours, minutes = duration.split(":")
    duration = int(hours) + int(minutes)/60
    return duration

def compute_durations(df):
    df_copy = df.copy()
    df_copy['duration_hours'] = df_copy['duration'].str.split(":").apply(lambda x: int(x[0]) + int(x[1])/60)
    df_copy['cumulative_time'] = df_copy['duration_hours'].cumsum()
    return df_copy

def plot_eva_durations(file_name, df):
    plt.plot(df['date'], df['cumulative_time'], 'ko-')
    plt.xlabel('Year')
    plt.ylabel('Total time spent in space to date (hours)')
    plt.tight_layout()
    plt.savefig(graph_file)
    plt.show()


def main(input_file, output_file, graph_file):
    eva_df = read_json_to_clean_dataframe(input_file)
    eva_df.to_csv(output_file, index = False, encoding = 'utf-8')
    eva_df = compute_durations(eva_df)
    plot_eva_durations(graph_file, eva_df)

main(input_file, output_file, graph_file)

```

### Scripts vs libraries

When you are writing a Python software/project, you will often have you codes separated into functions. You might want to reuse these functions in other scripts as well, and you can by importing the script in any other python environment (e.g. `import eva_data_analysis`). When you import a Python file, all functions in the Python file will be available for use.
However, when you import a file with function calls and variable definitions that make up the "core functionality" of that file, you do not want it to be directly executed upon every import. You only want to use the functions in a different setting. Therefore we can define this "dunder name" check `__name__ = "__main__"` to make sure the script part only executed when the Python file is executed as a script directly.


```python=
if __name__ == "__main__":
    # filenames
    # Data source: https://data.nasa.gov/resource/eva.json (with modifications)
    input_file = './eva_data.json'
    output_file = './eva_data.csv'
    graph_file = './cumulative_eva_graph.png'

    main(input_file, output_file, graph_file)
```

### Commmand line interface
To make this script even easier to use, we can add a command line interface to the script. This will enable us to change the core variables (in our case the input and output files), without having to open and edit the script.

```python
...

import sys

...


if __name__ == "__main__":
    print(sys.argv) # This print out the input arguements

...
```

Note `sys.argv` is a list, with the position 0 always the Python script name.

```python
if __name__ == "__main__":
    if len(sys.argv) >= 3:
        input_file = sys.argv[1]
        output_file = sys.argv[2]
        print("Using custom input and output filenames")
    else:
        # Data source: https://data.nasa.gov/resource/eva.json (with modifications)
        input_file = './eva_data.json'
        output_file = './eva_data.csv'

    graph_file = './cumulative_eva_graph.png'

    main(input_file, output_file, graph_file)
...
```

We can use this to pass in the file names directly when calling the script on the command line. This way you can quickly change to a different input or rename your output files.

```shell
python eva_data_analysis.py eva-data.json clean_eva_data.csv
```

### Directory structure

It is useful to organize your software project with various directories. Again it is useful to follow conventions so that others will find common files where they expect them.

```shell
project_name/
├── README.md             # overview of the project
│── LICENSE               # license for your code (can also be put into the src/ directory)
├── data/                 # data files used in the project, including data license information. A separate LICENSE file with a data license can also be put in this folder.
│   ├── README.md         # describes where data came from
│   ├── raw/
│   └── processed/
├── manuscript/           # manuscript describing the results
├── results/              # results of the analysis (data, tables)
│   ├── preliminary/
│   └── final/
├── figures/              # results of the analysis (figures)
│   ├── comparison_plot.png
│   └── regression_chart.pdf
├── src/                  # contains source code for the project
│   ├── requirements.txt  # software requirements and dependencies
│   ├── main_script.py    # main script/code entry point
│   └── ...
├── doc/                  # documentation for your project
├── └──index.html         # entry point into the documentation website
└── ...
```

When changing directory structure, use `git mv` command to let git understand files have not been deleted or created, but only moved.

```shell
git mv FROM_FILE_NAME TO_FILE_NAME
```

Git will not track, or allow committing empty directories. Add a `.empty` file inside a directory that you want your users to have when cloning the project (e.g. a `results` directory).

### Code state

Our code is now in this state:
https://github.com/rogerkuou/spacewalks/blob/1342f475a4b45cc7f6d3b60efa39914eacce8816/eva_data_analysis.py


### Informal vs formal testing

Usually if you write code, you also test it. Just by running the script that you created before committing, or when you made a change, you are testing whether it still works. While this is valuable because it is quick and provides immediate feedback on your changes, there are some limitations and downsides:
 - working interactively is eror prone
 - you must repeat it every time to make sure nothing broke, this may become very time consuming
 - we rely on our own memory to assert which parts of the code have been tested and with what input values

This can be overcome by formalizing our testing process.

### Testing with pytest
We can use the testing framework `pytest` to structurally test our software functionality.

Create a `tests` folder and a file called `test_eva_analysis.py`.

Also install pytest in your virtual environment:

```shell

```

At the top of this ile we import pytest and the function we want to test.

```python
import pytest

from eva_data_analysis import text_to_duration

def test_text_to_duration_value_correctness():
    input_text = "11:30"
    expected_output = 11.5

    actual_output = text_to_duration(input_text)

    assert actual_output == expected_output

```

Run pytest using
```shell
python3 -m pytest
```

## 🚗 Parking lot
* Talk about lambda functions being applied to the df.
* Why would you add functions if it makes your code bigger?
    * It helps to abstract away parts of your code. If you use explicit and helpful function names, you don't need to know what code is actually inside the function to understand the whole script. You can still check what exactly happens by looking inside the function, in this case, the separation also helps, because you can limit the context, you only need to understand the few lines inside the code and whether they do what the function name suggests.
* Maybe something for the parking lot, or it could be outside the scope of the course, but some of my colleagues use CI/CD pipelines. Are we going to discuss or use those?
    * We might discuss this (both for automatically running tests and deploying documentation), but not in depth. The workshop materials have an auxiliary episode about this that you can check out: https://carpentries-incubator.github.io/better-research-software/ci-for-testing.html
    * If you use the eScience Center template for Python packages, you will automatically get some help on setting up CI/CD for you project: https://github.com/NLeSC/python-template

## 📚 Resources

- [NLeSC Python Template](https://github.com/NLeSC/python-template)
- [sarxarray](https://github.com/TUDelftGeodesy/sarxarray)
