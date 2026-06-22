![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document Day 2

2026-05-26 Building Better Research Software

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------

This is the Document for today: https://edu.nl/8avvk

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


## 🖥 Workshop website

[link](https://esciencecenter-digital-skills.github.io/2026-05-26-ds-building-better-rs/)

🛠 Setup

[link](https://carpentries-incubator.github.io/better-research-software/installation-instructions.html)

Download files

[Spacewalks data and analysis code](https://github.com/carpentries-incubator/better-research-software/raw/refs/heads/main/learners/spacewalks.zip)

[Code state at the start of day 2](https://github.com/carpentries-incubator/bbrs-software-project/tree/03-reproducible-dev-environment)

```
git clone git@github.com:carpentries-incubator/bbrs-software-project.git
cd bbrs-software-project
git switch 03-reproducible-dev-environment
```

## 👩‍🏫👩‍💻🎓 Instructors

Jaro Camphuijsen, Sander van Rijn, Ou Ku

## 🧑‍🙋 Helpers

Jaro Camphuijsen, Sander van Rijn, Ou Ku


## 🗓️ Agenda
|  Time | Topic                        |
| -----:|:---------------------------- |
| 09:30 | Welcome,icebreaker and recap |
| 09:45 | Reproducible Environments    |
| 10:20 | Code readability             |
| 10:45 | **Coffee break**             |
| 11:00 | Code readability             |
| 11:30 | Code structure               |
| 12:00 | **Tea break**                |
| 12:15 | Code structure               |
| 12:45 | Wrap-up                      |
| 13:00 | END                          |

## 🔧 Exercises

### Rename our variables to be more descriptive (5 min)
Let’s apply this to eva_data_analysis.py.

1. Edit the code as follows to use descriptive (and consistent) variable names:

- Change data_f to input_file
- Change data_t to output_file
- Change g_file to graph_file
- Be sure to change all the occurrences of each variable name.

2. What other variable names in our code would benefit from renaming? Rename these too. Hint: variables w, t, tt and ttt could also be renamed to be more descriptive.

3. Commit your changes to your repository. Remember to use an informative commit message.


## 🧠 Collaborative Notes

### ❓Questions and answers:

**Q: How to solve `UnicodeEncodeError: 'gbk' codec can't encode character '\xc2' in position 100: illegal multibyte sequence`?**
A: \xc2 is an emoji and you need a package to be able to process emoji's
Holkan: Actually you can print emojis without any package. Look at [this]( https://www.geeksforgeeks.org/python/python-program-to-print-emojis/) and the [Unicode](https://unicode.org/emoji/charts/full-emoji-list.html
) for emojis
The solution for this is to enforce the encoding:
```python=
data_f = open('./eva_data.json', 'r', encoding='ascii')
data_t = open('./data.csv','w', encoding='utf-8')
```

**Q: Can I share my virtual environment folder?**
A: The virtual environment folder is relatively big and very personal to your computer. The easier way to share your environment is by sharing your requirements in e.g. a requirements.txt file.

**Q: Can we use pip show (library) instead of python -m pip show (library) ?**
A: It is recommended to use `python -m pip https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens...`  instead of just `pip ...` to guarantee that you're using the pip associated with your virtual environment. However if you have checked by `which pip` and made sure the `pip` is from your virtual environment, usually it is fine to directly call `pip ...`

**Q: is there a command to show your python version, operating system and CPU type (AMD/Intel)?**
A: You can use `python --version` to print your current python version. If you want to manage it automatically, you will have to specify it in e.g. `pyproject.toml` or using Conda's `environment.yml`. For most projects, this should not be necessary, as long as your desired package versions are supported. If it's necessary to know the operating system and CPU type, then your use-case is a lot more specialized than we assume for this workshop 🙂

**Q: How can I share an exact version of my code?**
A: Depending on the level of maturity of your project, there's a few options, at least assuming your git repository is online on e.g. GitHub.
- Each git commit has a unique hash (shown e.g. when using the `git log` command.) This hash will always point to the same code. In GitHub, clicking the "XXX commits" above the file list shows the list of all commits.
    - For each commit, this shows a (shortened) version of the hash (e.g. `dc33f6c`). In the terminal, you can 'load' that state of the repository by using `git restore -s dc33f6c` or `git switch --detach dc33f6c`.
        - Using `restore` changes your files locally but does not change your current branch/commit, so be careful not to commit those before continueing
        - Using `switch --detach` puts you in a 'detached head' state. Any commits made from there will not be tracked by a branch unless you make a new one.
    - It also shows a link "browse repository at this point" for each commit, which you can copy and share for people to view online.
- While commit hashes are fixed, they are not very descriptive. You can use [tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) to give descriptive names to specific commits. Tags are different from branches, in that the tags "stay put" when you make a new commit, while branches "follow along" with the new commits. You can make tags in your terminal and push these, or make them through GitHub's interface.
    - `git restore -s tag-name` or `git switch --detach tag-name` will then also work.
- If you've published your code as a package, version numbers are required, so you can use those.

**Q: How to judge what dependencies to include, and which not, and how to avoid conflicts?**
A: There are several indicators of a "good" dependency:
- Mature packages are preferred as dependencies. These can be recognised by having many users, large community, being open source, active maintenance/release activity. If a dependency is only managed by a single developer, you should only use it only if it adds much values for your research.
- Try to 'effectively' use packages you import. If you add e.g. PyTorch (a very large package to install) to your project only for a small utility function, you can probably find that functionality somewhere else.
- There is no ultimate guarantee on no conflict, other than not relying on external packages in the first place: a package you don't use can't conflict with anything. Working with up-to-date versions of actively maintained packages usually reduces your risk the most. Sometimes you have to decide not using some certain dependencies becasue it's too out-dated. But keeping an indenpendent Python environment is usually enough to avoid most of the conflicts.

**Q: I've been told to use Personal Access Tokens to share access to my repository. How does that work?**
A: Access tokens are basically a password you can create that is linked to a repository with specific access. They are an alternative to the SSH key you are using to let your computer talk with GitHub on your behalf. See e.g. this GitHub page on [Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) for more information.

**Q: Jupyter Notebooks, what are they, what are they good/not good at?**
A: Jupyter notebooks are excellent for interactively exploring data and trying things out. Because you can run one cell at a time, you can incrementally work on problems, figuring out each next step as you go. The inclusion of headers and markdown cells makes it easy to document your process as you go. This is often used to write reports where the focus might be on the results, while still having all code and intermediate steps available too for the potential reader.

However, it is not recommended to use notebooks long term for your software projects, as there are two main things working against making it a sustainable way to develop software:

1. Execution order arbtrary and history can be rewritten. As a notebook user, you can (re-)execute any cell at any time in any order, and after executing a cell, you can rewrite what is in it, without the results being updated. This opens usage up to a lot of pitfalls regarding reusability/replicability, and relies on the writer's discipline to avoid them.
2. Notebooks are stored as `json` files with a lot of metadata about execution order and results included. This makes notebooks annoying to include in version control: changes in metadata such as when a notebook was run, or simply a cell being re-run with a higher order count will show up as modified files, any print statements or logging will be included which may be time dependent, and images are encoded as a very large single line of base64 encoded bytes, making diffs very hard to read. There are tools that can clean up your notebook for you, but this again relies on user discipline.

In general, notebooks are good for exploring or for demonstrations, e.g., tutorial documentation, but any reusable code, algorithms, etc, is better off in regular python files/packages where they can be imported.

See also:

- [Marimo](https://marimo.io): Jupyter alternative that enforces execution order
- [literate programming](https://en.wikipedia.org/wiki/Literate_programming): Wikipedia article about Literate Programming in general
- [Entangled](https://entangled.github.io): Stricter implementation of literate programming, developped by an RSE at the eScience Center

### ⌨️ Code Along

In VS code, press 'CTRL + /' when having code selected to comment out all lines

Use Python to create a virtual environment for your project:
```bash
$ python -m venv venv_spacewalk`  # create folder 'venv_spacewalk' with virtual environment
```

To use the virtual environment, you must activate it:
```bash
$ source venv_spacewalk/Scripts/activate  # Command for Windows
$ source venv_spacewalk/bin/activate      # Command for Linux/Mac
```

You will see `(venv_spacewalk)` appear in your terminal, to indicate your active environment

Now `python` will refer to the python in the virtual environment, without polluting your system python, or conflicting with other environments for other projects

```bash
$ python -m pip install matplotlib  # install matplotlib in your virtual environment
Collecting matplotlib
  Downloading matplotlib-3.10.9-cp314-cp314-win_amd64.whl.metadata (52 kB)
Collecting contourpy>=1.0.1 (from matplotlib)
  Downloading contourpy-1.3.3-cp314-cp314-win_amd64.whl.metadata (5.5 kB)
Collecting cycler>=0.10 (from matplotlib)
  Using cached cycler-0.12.1-py3-none-any.whl.metadata (3.8 kB)
[...  further output skipped for brevity]
Successfully installed contourpy-1.3.3 cycler-0.12.1 fonttools-4.63.0 kiwisolver-1.5.0 matplotlib-3.10.9 numpy-2.4.6 packaging-26.2 pillow-12.2.0 pyparsing-3.3.2 python-dateutil-2.9.0.post0 six-1.17.0
```

Pip can also show information about your installed packages:
```bash
$ python -m pip show matplotlib
Name: matplotlib
Version: 3.10.9
Summary: Python plotting package
...
```

Pip can print a list of your omittedinstalled packages:
```bash
$ python -m pip freeze > requirements.txt  # or manually copy the output of python -m pip freeze
```

This `requirements.txt` can be used to 'share' your environment: it's a compact specification that pip can use to exactly recreate it using `install -r`:
```bash
python -m pip install -r requirements.txt
```

#### Take-over by Jaro: How to use A GitHub repository to "catch up"

From github, clone the repository to download it into a folder named "spacewalks"
```sh
$ git clone git@github.com:rogerkuou/spacewalks.git
...
$ cd spacewalks
```

**ONLY If you are not up to date with the venv**, remove the old one and install from the `requirement.txt` from OuMaybe add one or two practical experiences in your work (3-5 min show-case)

First remove the old venv with the `rm` command

Create fresh virtual environment:
```bash
$ rm -r venv_spacewalk       # remove old environment if it exists
$ python -m venv .venv       # Create fresh environment
$ source .venv/bin/activate  # or .venv/Scripts/activate for Windows
(.venv) $ python -m pip install -r requirements.txt  # install requirements
```

:::info
<details><summary><b>Virtual environment name can differ from folder name</b></summary>
You can use the `--prompt` argument to change the name that shows up in brackets:

```bash
$ python -m venv .venv --prompt spacewalks
$ source .venv/bin/activate  # or .venv/Scripts/activate for Windows
(spacewalks) $ ...
```
</details>
:::

To run the python script, you need to first make sure the path is correctly configfured:

```python=
data_f = open('./eva_data.json', 'r)
data_t = open('./data.csv', 'w')
```

:::info
For Windows users, you need to enforce the encoding:
```python=
data_f = open('./eva_data.json', 'r', encoding='ascii')
data_t = open('./data.csv','w', encoding='utf-8')
```
:::


Let's put these changes in git history:

```bash=
git add eva_data_analysis.py
git commit -m "Specify path and data encoding"
```

Then you can execute the Python script:

```python=
python eva_data_analysis.py
```

In VSCode, you can use "Alt + up" and "Alt + down" to move the selected code blocks

### Code readability

#### Moving import statements to top

Currently the `import` statements are spreaded around the code. This does not give us a good overview of which libraries are usedm. It is also fragile if someone inserts more codes before the importing. So it's nice to organize all the importing at the beginning:
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
```python=
# Start of eva_data_analysis.py
import json
import csv
import datetime as dt
import matplotlib.pyplot as plt
```

Add these changes to the git history, and push to remote.

```
git add eva_data_analysis.py
git commit -m "Move import statements to the top"
git push
```

#### Variable names

Good examples:

```python=
my_awesome_variable # all small letters, use "_" to separate

```

The following works but not recommended:
```python
myAwesomeVariable # Capitable letters usually indicates class names but not variable names
```


These do not work:
```python=
my awesome variable # space is not acceptable in Python

my-awesome-variable # "-" will be interpreted as minus
```

In VSCode, You can use "Ctrl + F" to search and "Ctrl + H" to replace a certain pieces of text. Using "F2" provides a better functionality for renaming variables. For example, when renaming `t` for `duration_dt`, it will not rename `ttt` to `duration_dtduration_dtduration_dt` but understands that `ttt` is a different variable and leaves it alone.

Jaro edited `eva_data_analysis.py` during the exercise of updating variable names, and pushed to GitHub. You can have the lates version at the [Instructor's code-along repository](https://github.com/rogerkuou/spacewalks)


#### Use third-party libraries

We will not dive into this part of the teaching material. It is recommended to use third-part libraries, like `pandas`, to avoid reinventing wheels. However you should consider following factors:

- when "improving code readability", you should be careful on not changing the code readability.
- you should consider how many dependencies to add to your code project, each one may make the installation workflow fragile in the future


### Some more git commands

Check unstaged changes (in red):

```shell=
git diff <unstaged_file>
```

Revert unstaged changes (in red):

```shell=
git restore  <unstaged_file> # Note your unstaged changes will lost!
```

Revert staged changes (in green):

```shell=
git restore --staged <staged_file>
```

Revert committed changes (already in git history):

```shell=
git revert <commit-hash> # A new commit will be added to revert the change
```


## 📚 Resources

- [Instructor's code-along repository](https://github.com/rogerkuou/spacewalks)
- [Python Style Guide: imports](https://peps.python.org/pep-0008/#imports)
- [Python Style Guide: prescriptive naming conventions](https://peps.python.org/pep-0008/#prescriptive-naming-conventions)
- [Personal Access Tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens)
- [Marimo](https://marimo.io): Jupyter alternative that enforces execution order
- [literate programming](https://en.wikipedia.org/wiki/Literate_programming): Wikipedia article about Literate Programming in general
- [Entangled](https://entangled.github.io): Stricter implementation of literate programming, developped by an RSE at the eScience Center

### Tools for managing your (virtual) environment:
- [Documentation](https://docs.python.org/3/tutorial/venv.html) for Python's venv module
- [UV](https://docs.astral.sh/uv/)
    - `uv pip ...` is a drop-in replacement for `pip`, but written in Rust for much faster environment creation and package installation
    - This tool is created by the same company as [ruff](https://docs.astral.sh/ruff/)
    - Note: Astral has been [acquired by OpenAI](https://astral.sh/blog/openai). The existing tools are still open source, and will continue to be in the future, but it is a possible risk for their longevity: development may stop, or new features may become paid-only 🤷.
- [Conda](https://anaconda.org/anaconda/conda)
    - Conda is an alternative environment manager. It can also manage your Python versions, and has an alternate package index especially suited for complex packages with compiled backends. It can still work together with regular `pip`, but may cause issues when combined incorrectly.
- [Mamba](https://anaconda.org/channels/conda-forge/packages/mamba/overview)
    - Similar to `uv pip` for `pip`, `mamba` is a drop-in replacement for `conda`, rewritten in C++ for much better performance when creating environments and installing packages.
