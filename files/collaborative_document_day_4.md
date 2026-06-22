![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document Day 4

2026-05-26 Building Better Research Software

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------

This is the Document for today: https://edu.nl/v4ugn

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

Current code status

[link](https://github.com/rogerkuou/spacewalks)



## 👩‍🏫👩‍💻🎓 Instructors

Jaro Camphuijsen, Sander van Rijn, Ou Ku

## 🧑‍🙋 Helpers

Jaro Camphuijsen, Sander van Rijn, Ou Ku

## 🗓️ Agenda
|  Time | Topic                         |
| -----:|:----------------------------- |
| 09:30 | Welcome, icebreaker and recap |
| 09:45 | Testing                       |
| 10:45 | **Coffee break**              |
| 11:00 | Documentation                 |
| 12:00 | **Tea break**                 |
| 12:15 | Wrap-up                       |
| 12:45 | Post workshop survey          |
| 13:00 | END                           |

:::info
ℹ️**Change to the syllabus**

We decided to change the schedule and syllabus for this workshop. The episode [Software Management & Collaboration](https://carpentries-incubator.github.io/better-research-software/08-open-collaboration.html) will not be taught explicitly. Instead we integrate most of its contents with the other episodes. We do encourage you to have a look at the material and try it out!

If you want to dive further into these topics, we would recommend the [Intermediate Research Software Development in Python](https://carpentries-incubator.github.io/python-intermediate-development/) workshop. We will likely be teaching this workshop in November '26. Sign up for our [newsletter](https://esciencecenter.us8.list-manage.com/subscribe?u=a0a563ca342f1949246a9f92f&id=31bfc2303d) to be informed when you can register.
:::

## :hammer: Ice-breaker :snowflake:

### Venus 🪐♀️
![True color image of Venus](https://upload.wikimedia.org/wikipedia/commons/0/08/Venus_from_Mariner_10.jpg "Venus" =150x150)

### Mars 🪐♂️
![True color image of Mars](https://upload.wikimedia.org/wikipedia/commons/0/0c/Mars_-_August_30_2021_-_Flickr_-_Kevin_M._Gill.png "Mars" =150x150)


## 🔧 Exercises

### 1. Write a test for the `read_json_to_clean_dataframe` function (10 min, until 10:43)

```python=
def test_read_json_to_clean_dataframe():
    df = read_json_to_clean_dataframe("data/eva_data.json")
    # check shape
    assert df.shape == (330, 7)
    # check no na values in duration and date columns
    assert df["duration"].isna().sum() == 0
    assert df["date"].isna().sum() == 0
    # check date sorting
    assert df["date"].is_monotonic_increasing
```

## 🧠 Collaborative Notes

### ❓Questions and answers:

**Q: general python question; when do you use `'` and when `"`?**
A:
> In Python, single-quoted strings and double-quoted strings are the same. This PEP does not make a recommendation for this. Pick a rule and stick to it. When a string contains single or double quote characters, however, use the other one to avoid backslashes in the string. It improves readability.
For triple-quoted strings, always use double quote characters to be consistent with the docstring convention

_[https://peps.python.org/pep-0008/#string-quotes](https://peps.python.org/pep-0008/#string-quotes)_

Most formatters, such as `ruff`, will default everything to use double quotes `""`.

Here's some examples of how you would use single quotes in a double-quoted string and vice versa:

```python
>>> print("This string contains a single quote: '")
This string contains a single quote: '
>>> print('This string contains an escaped single quote: \'')
This string contains an escaped single quote: '

>>> print("This string contains an escaped double quote: \"")
This string contains an escaped double quote: "
>>> print('This string contains a double quote: "')
This string contains a double quote: "

>>> print("You will get a "syntax error" if you try to use the same quote type like this")
  File "<stdin>", line 1
    print("You will get a "syntax error" if you try to use the same quote type like this")
          ^^^^^^^^^^^^^^^^^^^^^^^
SyntaxError: invalid syntax. Perhaps you forgot a comma?
```

**Q: What should I put in a README's 'Installation instructions'? Did I make a package or should I clone it?**
A: The 'Installation Instructions' section of your README should give the currently relevant instructions for your project. If you have not taken any steps to 'package' your code, then a user will typically have to clone your repository in order to work with your code. So in that case, your instruction would probably include the following command:

```bash
git clone https://github.com/username/repository.git
```
:::info
_it is usually safest to use the `https` url here instead of the SSH url, in case people don't have an SSH key set up for GitHub_
:::

If you've added at least a minimal `pyproject.toml` file (see below), your project becomes installable with `pip`. This can be done directly from github using the `https` url, which you can find in the green 'code' button at the top of your repository page.

```bash
pip install git+https://github.com/username/repository.git
```

You can even install a specific branch or commit:
```bash
pip install git+https://github.com/username/repository.git@branch
```

:::success
#### `pyproject.toml`

A minimal `pyproject.toml` contains a `build-system` section and a `name` and `version` under the `project` section:
```toml
[build-system]
requires = ["setuptools >= 77.0.3"]
build-backend = "setuptools.build_meta"

[project]  # name and version are the minimally required keys
name = "mypackage"
version = "1.0"
```

For the build-system, you can just pick any from [these suggested examples](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#declaring-the-build-backend)

That page also contains an example of a ['complete' `pyproject.toml` file](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/#a-full-example), with explanation of all the possible keys.

From there, you can also continue into publishing your package to PyPI, so your package can be installed as `pip install packagename`
:::

### Extending tests

#### GitHub Issues

Jaro created an [Issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/learning-about-issues/quickstart) on Ou's GitHub repository: [Use Pytest's parametrize](https://github.com/rogerkuou/spacewalks/issues/2)

Use issues to record bugs, suggest new functionality. They are also a great place to have discussions before starting to write code. The earlier you find a bug or decide on the right thing to build, the more time you save!

#### Pytest Parametrize

Pytest's `parametrize` is a **decorator**: a function that acts on another function.

You don't have to understand how it does that, but just know you can apply it to a function with the `@` symbol:

```python=
test_data = [("11:30", 11.5), ("00:45", 0.75), ("2.15", 2.25)]

@pytest.mark.parametrize("input_text, expected_output", test_data)
def test_text_to_duration_value_correctness(input_text, expected_output):
    actual_output = text_to_duration(input_text)
    assert actual_output == expected_output
```

The `parametrize` function takes two arguments:
1. which function arguments will be passed in
2. a collection of argument values to test

In this case, `"input_text, expected_output"` are the arguments (can be either a comma-separated string, or a list of strings).
Then each tuple in the `test_data` list will be passed in by pytest, and will be run as a separate test. The values are passed in according to how you specified the argument names. Each of them will be tested and reported independently.

When testing the same function in the same way with multiple inputs, this is a much shorter way of writing those tests, rather than copying the code and changing the values in each copy.

#### Working on a branch

To address an issue, it is best to work on a separate branch. Before switching to a new branch, it is good practice to temporarily store away your changes first. This can be done with `git stash`: it takes all changes to tracked files and keeps them safe, while leaving your repository in a clean state.

Then we can create a new branch and switch to it:
```bash
git branch 2_adding_parametrize
git switch 2_adding_parametrize
# or in one go:
git switch -c 2_adding_parametrize`  # -c for 'create'
```

:::info
<details><summary><b>git checkout VS git switch/restore</b></summary>
A couple of years ago, `git switch` and `git restore` were introduced as separate commands for the overloaded `git checkout` command, which could do both depending on the arguments. The separate `switch` and `restore` commands are much clearer in what they do: `switch` changes branches, while `restore` changes files.
<p></p>
You may still find a lot of people who have been using git for a long time using `git checkout` out of muscle memory, and a lot of older information online will also be referring to it. The `checkout` command is still supported and will work, but is less intuitive because of it's overloaded behavior, so we recommend learning to use switch and restore instead.
</details>
:::

Now we are on the new branch, we can get our stashed changes back with `git stash pop`. With these changes on a fresh branch, we can commit as usual:

```bash
git commit -m "add parametrize to a unit test"
```

To push this new branch, we have to tell git to push it to our remote repository, which by default is called `origin`:

```bash
git push --set-upstream origin 2_adding_parametrize
```

The `--set-upstream` argument tells git to remember that we pushed this branch to the `origin` remote, meaning that next time we can just use `git push` without having to fully specify `git push origin 2_adding_parametrize`.

#### Pull Requests

Pull Requests (also called Merge Reguests on GitLab), are a way to collaborate with multiple people using git. If you are collaborators on the same repository, you can push your branches addressing the issue you're working on, and create a Pull Request (PR) for it. This requests the (other) maintainer(s) to merge your branch into e.g. the main branch. In a PR, you can review the proposed changes, make comments on even single lines of code, request further changes or approve them. Using CI/CD, you can set up a lot of automated checks to happen for each PR.

When the review has been approved, the PR can be merged, and the `main` branch will be updated on GitHub. You can then pull those changes down to your local repository.

GitHub will also offer to remove the branch that was merged in the PR. This strongly assumes that you were working in a dedicated feature branch, which is the recommended way. Some repositories may even be set up to automatically delete these branches, so don't make a pull request using a long-living branch unless you've discussed this way of working with your collaborators.

### Documentation

#### Docstrings

Docstrings are documentation in standard formats you can add to your functions and classes. They typically docs the general functionality, input arguments, outputs, and error raises.

A single line docstring:
```python=
def division(x, y):
"""Divide number x by number y."""
```

```python=
def division(x, y):
"""
Divide number x by number y.

Arguments:
    x: A number to be devided
    y: A number to devide by

Return:
    float: The devision of x by y

Raises:
    ZerodivisionError: when y is 0
"""
```

### README file

A general intro file for your repo, including installation guide, etc. It will be rendered in the GitHub landing page of the repo.

### LICENSE file

You can create a standard one using GitHub GUI. eScience Center usually works with Apache 2.0 which is very permissive

### Citation file

You can use the oline GUI [CFF init](https://citation-file-format.github.io/cff-initializer-javascript/#/) to generatate a `citation.cff` file, which will be redendered by GitHub and generate a citation button on your GitHub landing page.

## 🚗 Parking lot

- Using GitHub Co-pilot for writing tests
- How to get everyone on board with using branches on GitHub?
  - This always remains a social problem. It is good to remember that people will be most likely to do things if they see a benefit in it. So if you can find a problem you/they frequently run into that would be resolved by working with branches, try to focus on that to convince them. It's not some administrative overhead you want them to do, it's the solution to a problem they're facing. Depending on the level of experience, it may be necessary to slowly bring them up to speed by first introducing some more basic aspects of the workflow, before extending it. Lowering barriers to entry will also help people to make the step.

## 📚 Resources

- [Pytest Parametrize](docs.pytest.org/en/stable/example/parametrize.html)
- [mibitrans](https://github.com/MiBiPreT/mibitrans): The GitHub repo Jaro showed as the example for collaboration
- [CFF init](https://citation-file-format.github.io/cff-initializer-javascript/#/)
- [build.yaml](https://github.com/rogerkuou/spacewalks/blob/unit_tests/.github/workflows/build.yaml): A quick example of how to setup CI for the example spacewalk repo.
- [Python template from eScience Center](https://github.com/NLeSC/python-template)
