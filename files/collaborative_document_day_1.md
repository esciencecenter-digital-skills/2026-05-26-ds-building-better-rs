![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document Day 1

2026-05-26 Building Better Research Software

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------

This is the Document for today: https://edu.nl/vqn8u

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

## 👩‍🏫👩‍💻🎓 Instructors

Jaro Camphuijsen, Sander van Rijn, Ou Ku, Fenne Riemslagh

## 🧑‍🙋 Helpers

Jaro Camphuijsen, Sander van Rijn, Ou Ku, Fenne Riemslagh

## 🗓️ Agenda

|  Time | Topic                                       |
| -----:|:------------------------------------------- |
| 09:30 | Welcome and icebreaker                      |
| 09:50 | Software for open and reproducible research |
| 10:15 | **Coffee break**                            |
| 10:30 | Better start with a software project        |
| 12:00 | **Coffee break**                            |
| 12:15 | Reproducible software environments          |
| 12:45 | Wrap-up                                     |
| 13:00 | END                                         |

## 🔧 Exercises

### Assess the software project (10 min)
Individually inspect the code and data. Try and see if you can understand what the code is doing and how it is organised.

In the shared document, write down anything that you think is not “quite right”, not clear, is missing, or could be done better.

1. no documentation, only "old" and V2 but no clear indication of changes. data link broken. directory unstructured (goes doreclty from projects --> analysis folder --> csv file), hard-coded import
2. Folder is called 'old' and 'v2', undocumented, no read me, unclear if you should use 'my code' or 'code', file locations are hard coded, data as csv and json, no 'main', imports at bottom of script
3. V2 of the code, no documentation
4. Hard coded file path, import in the middle, not intuitive variable name such as ttt, l. No inline comment nor docstrings.
5.
   1. without opening the json file, I don't why the code refer to range(375), there should be a smarter way to read the line number.
   2. Why is there a .DS_Store file? 3. No clear annotation in the code, nor README file. 4.Used absolute path definition.
6. Folder has no readme.md. Non-descriptive file-naming. Terrible variable naming. Nested decision tree. Import not at top of file. Scripting style. Magic numbers. Unformatted data file.
7. Broken data link. No project structure. Missing README, metadata, autorhsip, citation, version control, etc. No good practice about the file path to read input data. No documentation or explanations of what functions do.



### Update filenames (5 min)
Try to make these changes yourself.

Give our Python script and input data file informative names - `eva_data_analysis.py` and `eva-data.json`, respectively.
Update other file names and paths used in the script - output CSV data (eva-data.csv to match the new input data name) and plot(cumulative_eva_graph.png).
Stage and commit these changes in the Git repository.

**Solution:**
Update the file references in the python file:
```python
data_f = open('./eva-data.json', 'r')
data_t = open('./eva-data.csv', 'w')
g_file = './cumulative_eva_graph.png'
```
Then track rename the files and track the changes with git:
```bash
git mv data.json eva-data.json
git mv my_code_v2.py eva_data_analysis.py
git add eva_data_analysis.py
git commit -m "Implement informative file names"
```


## 🧠 Collaborative Notes

### Questions and answers:

Q: What is a `.DS_Store` file?
A: It is used by MacOS to store custom folder attributes. It is unused by Windows and Linux and can be safely removed.

Q: I there a reason for using a normal dash - for the data name and an underscore _ for the code name?
A: Using dashes can sometimes cause issues: You cannot import from a python file with dashes in the name, since they are treated as 'minus'. Other than that, it is mostly just a convention you should decide on.

### Used commands:

`git init` - Initialize a git repository in the currently active folder


`rm -r astronaut-data-analysis-old` - Remove the old folder (the -r stands for recursive and is needed to remove the whole directory)

:::warning
<details>
<summary><b>Warning: Removing untracked files</b></summary>

In the teaching materials of this course, this folder is removed before initializing version control. This means that the old files are really lost. In practice it is usually better to first start version control on the original state of the project you inherited and only then start removing things.

An exception to this might be when you inherit a project that include a large amount of data/binary files that you know do not belong in your software project (e.g. someone added in a 1 hour video or a folder full of powerpoint slides). Git is really geared towards version control for text based files, like source code, the large non-text files will clutter your history, and creating a local copy of the repository will then always include these huge unnecessary files.
</details>
:::

`git add my\ code\ v2.py`
`git add data.json` - Stage the code and data files to be ready to commit

`git status` - View the status of our repository: Which branch we're on, which changes are ready to be committed, which changes are seen but not going to be committed, and which files are currently untracked by git.

`git commit -m "Add the initial spacewalks data and code"` - Make a commit of the proposed changes: record the added files in the repository.

`git mv my\ code\ v2.py my_code_v2.py` - Rename file and immediately tell git to track this change

:::info
<details>
<summary><b>Info: `git mv`</b></summary>

`git mv` is git's alternative to Linux' own `mv` command. When just using `mv`, git will consider the original file as `deleted` and see a new untracked file. To track the rename, you would have to `git rm [old_name]` and `git add [new_name]`, which git will notice as a rename action. Using `git mv` is just a faster way of achieving that.
</details>
:::

`git commit -m "remove space from the mycode file"` - Commit the renaming of the file

`git log` - Show the history of commits we've made so far: author, date, time and the summary message for each commit

Create a new empty repository on GitHub: no license, no README, etc. This will show the Quick Setup instructions by GitHub, and will let us directly push our local repository to GitHub.

![](https://codimd.carpentries.org/uploads/upload_24cef8d4b6a07d4a91cceb887db82fec.png)

:::danger
You cannot push an existing repository to a newly created GitHub repository that already has some files in it. If you want to add a README or license to your existing local repository, you must do so after creating the repository.
:::

## 📚 Resources
Options to store your opendata, instead of dumping them on GitHub:

- [Zenodo](https://zenodo.org/)
- [Figshare](https://figshare.com/)
- [DANS](https://dans.knaw.nl/nl/) - Dutch expertise center for research data
