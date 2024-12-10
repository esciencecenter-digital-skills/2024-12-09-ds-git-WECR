![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document 'Collaborative version control with Git and GitLab'

2024-12-09

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------
This is the Document for today: [edu.nl/jrhjr](edu.nl/jrhjr)

##  🫱🏽‍🫲🏻 Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.
 
## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, just raise your hand.

If you need help from a helper, place an orange post-it note on your laptop lid. A helper will come to assist you as soon as possible.

## 💻Important links

🖥 Workshop website

https://esciencecenter-digital-skills.github.io/2024-12-09-ds-git-WECR/

🛠 Setup

https://esciencecenter-digital-skills.github.io/2024-12-09-ds-git-WECR/#setup

GitLab subgroup

https://git.wur.nl/fb-it/wecr-research/gitcourse_subgroup

## 👩‍🏫👩‍💻🎓 Instructors

Sven van der burg, Lucas Esclapez

## 🧑‍🙋 Helpers

Willem-Jan van Zeist, Heleen Bartelings


## 🗓️ Agenda
09:45	Walk-in with coffee and cookies
10:00	Welcome and icebreaker
10:15	Workshop introduction
10:30	Introduction to Git, setting up Git
10:45	Creating a repository, tracking changes.
11:00	Coffee break
11:15	Exploring history, ignoring things
12:00	Remotes in GitLab
12:30	Lunch Break (photo)
13:30	Collaboration with Git and GitLab: The git workflow
15:15	Coffee break
15:30	Good practices for collaboration @MAGNET
16:45	Wrap-up
17:00	Drinks and dinner @Minglemush (at own cost)

## 🏢 Location logistics
* Coffee
* Wifi
* Toilets (in case of other emergencies)
* Emergency

## 🎓 Certificate of attendance
If you attend the full workshop you can request a certificate of attendance by emailing to training@esciencecenter.nl.
Please request your certificate within 8 months after the workshop, as we will delete all personal identifyable information after this period.


## 🧠 Collaborative Notes

### Introduction to Git:
 - Why use git ?
     - Keep track of changes
     - Sharing
     - Collaborate
 - Documents are series of changes
 - Changes can be independent, merged in the future

### Configuring git
Open `git bash` by right clicking on your desktop or in your file explorer and click 'Open Git Bash here'.

We teach with the command line. 
* This is what `Git` was designed for and it is a good way to learn the basics of `Git`. 
* This knowledge is then transferable to any Graphical User Interface for Git (like git tortoise). 
* * Some functionality of Git is not supported by git GUIs (like blobless cloning) so it is good to be familiar with Git in the command line.

Some useful commands:
`ls`: List files in current directory
`pwd`: Path to current working directory

Configuring your username and email
```bash
git config --global user.name "Your name"
git config --global user.email "your@email.com"
```

Edit your configuration:
```bash
git config --global --edit
```

Configure your configuration
```bash
git config --global core.editor "nano -w"
```

### Creating a repository
Create a new folder called `planets`, and move into it
```bash
mkdir planets
cd planets
```

Initialize a new Git repository in this folder.
This is telling Git that everything in this folder we want Git to keep track of.
```bash
git init
```

List all files (also hidden files)
```bash
ls -a
```

The `.git` folder is a hidden folder in which everything related to Git is stored.

Ask Git for the current status of Git
```bash
git status
```
This shows you we are on branch `main` and have not changed any files.
```
On branch main

No commits yet
```

Switch to a new branch called `main`
```bash
git switch -c main
```

### Tracking changes
Use nano to create a file called `mars.txt`
```bash
nano mars.txt
```

Print content of `mars.txt`
```bash
cat mars.txt
```
Output:
```
Cold and dry, but everything is my favorite color.
```
Request the status of Git:
```bash
git status
```
This will show you you have one untracked file called `mars.txt`

```bash
git add mars.txt
```

`git status` will show you that you now have 'changes to be committed'

[Visualization of concepts around staging area](https://esciencecenter-digital-skills.github.io/digital-skills-slides/modules/git-lesson/git-slides#/5/0/1)

Commit the changes in the staging area
```bash
git commit -m "Start notes on Mars as a base"
```

`git status` will tell you now you have nothing to commit

Show the git history:
```bash
git log
```

Edit `mars.txt` again:
```bash
nano mars.txt
```

`git status` will show you that you modified `mars.txt`

You can add and commit these changes:
```bash
git add mars.txt
git commit -m 'Further thoughts about Mars'
```

`git status` will show you that you now have nothing to commit.
`git log` will show you a history with two commits

Add another line to mars.txt, edit the file using nano:
```bash
nano mars.txt
```

Show the difference between your changes and the version of those files in the repository:
```bash
git diff
```
You can add and commit these changes:
```bash
git add mars.txt
git commit -m 'Add the mummy thoughts'
```

### Exploring the Git history
- You can always go back to older version of the repository that are stored in the history.
- A commit is given a unique identifier, or `git hash` which is an alpha-numeric list of characters.
- A special reference to a commit is the `HEAD`, which refers to the last commit of the branch

 - Use `git log`, to see the history
 - To show the changes between the current version of the `mars.txt` file and a specific commit, use `git diff <a_hash> mars.txt`
 - Alternatively, you can use `HEAD` to refers to a commit.. Use `git diff HEAD~2` to show the diff between the `mars.txt` file and the file in his state 2 commits before HEAD.
 - You can restore a file to its state at a given commit, use `git restore  -s HEAD~2 mars.txt` to set back the mars.txt file back to its state at `HEAD~2`. Nothing is changed in the history, the `mars.txt` file on your file system is updated to its old state. If you want to actually set back the file to its old state in the history, you will need to `git add` and `git commit`.
 - `git restore mars.txt` without a git commit ID will use the latest version, i.e. it is equivalent to `git restore HEAD mars.txt`.

### Ignore certain files
 - Files you do not want in Git: output of program, solution files (*.sol), log files (*.log).
 - To mimic this, create empty files using `touch file.log` and `touch run1.sol`.
 - Those files will show up when you do a `git status`.
 - If you want to ignore those file, you can add them to a `.gitignore`. Git always check for the presence of the `.gitignore` and will ignore all the file with the `.log` or `.sol` extention if you add `*.log` and `*.sol` in the `.gitignore` file.


### Remotes
- First create a new repository on GitLab in the GITCourse_subgroup
- Top-right, click on the blue button `New project`
    - In the new window, set the project name as `planets_<myname>`
    - Use the default Project URL
    - Untick the Initialize repository with a README
    - Ignore the rest
    - Wrap-up with create project !
- In the backgroup, GitLab ran the `git init` command
- Go back to your `planets` folder in gitbash, let's now add the project URL we created on GitLab as a remote to our local git reposity.
- Copy the "git remote add ..." from the GitLab interface and run it in the planets folder.
- Use `git remote -v ` to show the remote was added to the repository.
- An `origin` remote is shown. `origin` is the default name for the remote
- `git push origin main` will order git to push your local repository to the `origin` remote repository. In particular it pushes the `main` branch.
- Go back to GitLab, you should now be able to see the `main` branch in your repository.

### Collaborating with GitLab
 - (R) Someone R open an issue and assign Someone S to the issue.
 - (S) Clone the repository R is working on to your local computer (get the URL from the bleu button "Code") using `git clone`
 - (S) Create a new branch: DO NOT WORK in MAIN, using `git switch -c "1-fix_issue_venus"`
 - (S) Do some work to fix the issue: create a new file with the properties of Venus.
 - (S) Use, `git add` and `git commit` to add and commit the new file to the repository
 - (S) Use `git push origin "1-fix_issue_venus"` to push the work to R repository. Note that `git clone` automatically added Someone R repository as `origin`.
 - (S) Create a `Merge Request` on GitLab, to merge the `1-fix_issue_venus` into `main`. You can select the source branch and the target branch. Assign (R) to the merge request.
 - (R) Look at the merge request opened by (S), make comments if needed, approve the merge request if the changes to the code address the issue.

### Best practices

 - How to avoid long-term divergence of your branch compared to the origin master ? -> regularly pull from origin master using `git pull origin master`. Doing this every day or evry week, if conflict arise they can be fixed without too much headache.
 - Merge vs rebase: `rebase` for cleaner history, but more difficult if there are a lot of changes, `merge` for branch you intent to share with other people.
 - `git stash` can be used to stash temporary changes away, for instance while doing some other tests, and you can recover what was stashed away using `git stash apply`.


## 🔧 Exercises

### Create a Git repository
#### Places to Create Git Repositories

Along with tracking information about planets (the project we have already created),
Dracula would also like to track information about moons.
Despite Wolfman's concerns, Dracula creates a `moons` project inside his `planets`
project with the following sequence of commands:

```bash
$ cd ~/Desktop   # return to Desktop directory
$ cd planets     # go into planets directory, which is already a Git repository
$ ls -a          # ensure the .git subdirectory is still present in the planets directory
$ mkdir moons    # make a subdirectory planets/moons
$ cd moons       # go into moons subdirectory
$ git init       # make the moons subdirectory a Git repository
$ ls -a          # ensure the .git subdirectory is present indicating we have created a new Git repository
```

Is the `git init` command, run inside the `moons` subdirectory, required for
tracking files stored in the `moons` subdirectory?se


#### (Optional) Correcting `git init` Mistakes
Wolfman explains to Dracula how a nested repository is redundant and may cause confusion down the road. Dracula would like to remove the nested repository. How can Dracula undo his last git init in the moons subdirectory?


##### Solution (use with caution, you can remove important files accidentally):
Git keeps all of its files in the .git directory. To recover from this little mistake, Dracula can just remove the .git folder in the moons subdirectory by running the following command from inside the planets directory:
```bash
rm -r moons/.git
```

#### (Optional) Creating a project in GitLab
If you create a project in GitLab, what do you think happens behind the scenes? (Which Git command is being run?)

##### Solution
If you create a project in GitLab, behind the scenes a new folder is created on the GitLab server and the `git init` command is called in this folder.

### Tracking changes exercise
#### 1. Which command(s) below would save the changes of myfile.txt to my local Git repository?n

1. `git commit -m "my recent changes"`
2. `git init myfile.txt`
   `git commit -m "my recent changes"`
3. `git add myfile.txt`
   `git commit -m "my recent changes"`
4. `git commit -m myfile.txt "my recent changes"`


#### 2. Committing Multiple Files
Remember that the staging area can hold changes from any number of files that you want to commit as a single snapshot.

1. Add some text to ``mars.txt`` noting your decision to consider Venus as a base
2. Create a new file ``venus.txt`` with your initial thoughts about Venus as a base for you and your friends
3. Add changes from both files to the staging area, and commit those changes.

#### 3. (optional) A new repository
1. Create a new Git repository on your computer called bio.
2. Write a three-line biography for yourself in a file called me.txt.
3. Add the file to the staging area, and commit your changes.
4. Make a modification.
5. Display the differences between its updated state and its original state.


### Exercise: Working as a project collaborator (in pairs)

Do this exercise in pairs. Each person is submitter (S) and reviewer (R) once. You can work on parallel (so you both start with creating an issue in your own repository)

#### Part 1
- PERSON R: Create an issue in the repository
- PERSON S: Clone this repository to your system
- PERSON S: Create a new branch, using `git switch -c new_feature`
- PERSON S: Make the changes requested in the issue
- PERSON S: Push the changes to the remote repository on GitLab, using `git push origin new_feature`
- PERSON S: submit a Merge Request, refer to the issue (e.g. "Closes #1")

#### Part 2
- PERSON R: review the Merge Request
- PERSON S: address the comments
- PERSON R: approve the Merge Request
- PERSON S: merge the Merge Request

#### Part 3 (Optional) Creating merge conflicts (in pairs)
Do this exercise in pairs. Each person is submitter (S) and reviewer (R) once.
- PERSON S and R: Create a new branch
- PERSON S and R: Make changes to the same lines of code/text
- PERSON S: Open a Merge Request and merge the changes in your feature branch to the main branch
- PERSON R: Open a Merge Request to merge the changes to the main branch, you will get a merge conflict:
![](https://codimd.carpentries.org/uploads/upload_0630f52dac780c340bf1fcfcbe0046b2.png)
- PERSON R (but person S look what's happening): Switch to the `main` branch with `git switch main`, do `git pull` to pull the latest commits from the remote. 
- PERSON R: Switch back to your feature branch, using `git switch new_feature`. Merge `main` branch into your feature branch: `git merge main`. This will trigger a merge conflict resolution mode. 
- PERSON R: Edit the file that has a merge conflict with `nano`. Choose how you want to resolve the conflict. You can choose one of the versions of the code or combine them into a better solution.
- PERSON R: Add the resolved changed to the staging area. Then commit to wrap-up the merge. 
- PERSON R: Push your changes to GitLab: `git push origin NAME_OF_FEATURE_BRANCH`





## Advanced git exercises
### Exercise: git stash
Git stash is used to temporarily 'stash' some changes.
You can for example use it in this situation:

I am in the middle of implementing a feature. A colleague comes in and asks me a question. To answer the question I need to demonstrate running code. What to do with my half-written code? -> Stash

How does it work:
1. Make same changes in a file
2. `git status` will show those changes
3. `git stash` will stash all the changes in the working directory
4. Run `git status` to check this
5. `git stash apply` will apply your stashed changes again
6. You can also add a message to a stash with `git stash push -m "my_stash_name"
7. Then list the stash with `git stash list`
8. You can then apply a specific item of this list with `git stash apply 0`. Were 0 is the index of the item in the stash list.

### Exercise: Merging vs rebasing
1. Read 'Changing Multiple Commit Messages' in [this guide on Rewriting History in Git](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
2. Have a look at: ![](https://github.com/ssciwr/git-rebase-xkcd-example/blob/main/xkcd.png?raw=true)
3. This should not end up in main. Instead, it is better to rewrite the history before the merge to main. Rebase has an interactive mode for that.
4. Clone the git-rebase-xkcd-example repository: `git clone https://git.wur.nl/fb-it/wecr-research/gitcourse_subgroup/git-rebase-xkcd-example.git`
5. Look at the commit history: `git log --oneline`
6. Try to improve the commit history using `git rebase -i 7686562` (last argument is the commit ID of the last commit not part of the rebase)

## 💬 Feedback
Can you help us improve this course? 
For next time we teach it, but also adjusting to your preferences in the afternoon.
Please write down one thing that went well and one thing that can be improved.
### What went well? 👍
- Instructors are friendly and eager to respond to all questions. 
- Nice to have time for deepd dive discussions, learnt stuff already that were hidden by tortoise 
- Good to have a step by step approach
- I really like the course so far. The explanation is clear and you are approachable
- I like the "under the hood" approach of using the command line - then you can use any GUI
- Good instructors!
- I like to work from scratch and buid up
- The simple code (wolfman and friends) for the examples is helpful. 
- Very good to have hands on experience on Gigit t especially for people like me starting almost from scratch
- Good interaction with the crowd
- Very interesting to learn what is happening behind toroise git to understand the process better
- I liked how it was built up, starting from the very basic.
-Thank you for adapting your presentation to make it easy to follow online.

### What can be improved? 💡
- Be mindful on when to stop picking questios that will be answered later in a practical way. :+1: :+1: 
- It's tempting to ask too many questions but are we on the track with time?
- For me the pace could be a bit faster :+1::+1: :+1: 
- We need to power through more. :+1: :+1:
- Too many theoretical questions from the audiance is slowing the pace of the course.
- perhaps stop discussions a bit faster to make sure we get to the end of the course material.
- Focus on learning by doing, agreeing with some of comments abouve :+1:

### Feedback summary
- We will park too specific off-topic questions for later. Please help us in not deviating too much from the main content.
- We will have time later for more 1-on-1 discussions when we have longer practical exercisesa
- We will skip details for some of upcoming topics

## Post-workshop survey
Please [fill in the post-workshop survey](https://www.surveymonkey.com/r/8Z9YHBW).

## 📚 Resources
- [Slides collaborative version control with Git and GitLab](https://esciencecenter-digital-skills.github.io/digital-skills-slides/modules/git-lesson/)