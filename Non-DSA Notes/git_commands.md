* steps:
  - Install python in the system
  - add python extension in vscode
  - clone git repo
  -
  - create a virtual env ------> outside project repo
  - (python -m venv venv)
  - activate the venv
  - (.\venv\Scripts\activate.bat) - if using cmd
  - (.\venv\Scripts\Activate.ps1) - if using powershell
  - 
  - select interpreter path before installing dependecies, choose the one that points to .venv inside your project folder.
  - (ctrl+shift+p -> type python:select interpreter)
  - 
  - install dependencies in requirement.txt
  - (pip install -r requirements.txt)



* Navigate to project folder
* setup username n mail :
  - git config --global user.name "your name"
  - git config --global user.email "your email"

* HTTPS/SSH Authentication

* Initialize git :
  - git init

* check current branch:
  - git branch    : show only local branches
  - git branch -r : shows remote branches
  - git branch -a : shows all branches


* create n switch to new branch for your changes:
  - git checkout -b 'feature_branch'

* new branch starts from the current's branch state.
  - when you create a new branch and switch to it, git will copy the current state of your working directory including uncommited  changes into that new branch


* check git status:
  - git status

* pull changes:
  - git pull origin main


* Add changes :
  - git add filename/.

* commit changes :
  - git commit -m "message"

* pushing for the first time:
  - git push --set-upstream origin your_branch_name

** for future changes, simply use git push.

* git restore . :
  - To discard uncommitted changes (modifications) you've made to files in your working directory, you can use:

-------------------------------------------------------------------------------

* Connect to remote repo:
  - git remote add origin "repo-URL"

* Push changes to remote repo
  - git push origin your branch-Name


* create PR:
  - after PR is merged, delete your feature branch. push changes to your remote branch, then delete the branch locally first.
  - git branch -d 'feature_branch'

* to delete from remote repo:
  - git push origin --delete 'feature_branch'

* sync your local repo with repo:
  - git checkout main
  - git pull origin main

------------------------------------------------------------------------------------------------
* git reset --hard HEAD :
  - if you want to completely overwrite your local changes and make your
  - local branch identical to the remote branch(discarding your local changes)

* git pull origin main - This command fetches the changes from the main branch of the remote named origin and merges them into your current branch.
--------------------------------------------------------------------------------------------------
* to bypass the vscode execution policy for single session as a temp solution:
  - Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

-------------------------------------------------------------------

* git commit --author="Saumya Sachan <ssachan1@ford.com>" -m "Commit message"
* git show --name-only


------------------
------------------

###########################################################################################################################

Markdown syntax :

* Headings : To create a heading, add number signs (#) in front of a word or phrase. #, ##, ###....
* Paragraph : To create paragraphs, use a blank line to separate one or more lines of text, don’t indent paragraphs with spaces or tabs.
* Line Break : To create a line break or new line (<br>), end a line with two or more spaces
* Bold : To bold text, add two asterisks or underscores before and after a word or phrase.
* Italic : To italicize text, add one asterisk or underscore before and after a word or phrase. 3# for both bold and italic.
* BlockQuote : To create a blockquote, add a > in front of a paragraph. Add a > on the blank lines between the paragraphs.

* Ordered Lists : To create an ordered list, add line items with numbers followed by periods.

* Unordered Lists : To create an unordered list, add dashes (-), asterisks (*), or plus signs (+) in front of line items. Indent one or more items to create a nested list.

* Images : To add an image, add an exclamation mark (!), followed by alt text in brackets, and the path or URL to the image asset in parentheses
eg: ![Tux, the Linux mascot](/assets/images/tux.png)

* Code : To denote a word or phrase as code, enclose it in backticks (`).

* Horizontal line : To create a horizontal rule, use three or more asterisks (***), dashes (---), or underscores (___) on a line by themselves.

* Code block : To create code blocks, indent every line of the block by at least four spaces or one tab.

* Links : To create a link, enclose the link text in brackets (e.g., [Duck Duck Go]) and then follow it immediately with the URL in parentheses (e.g., (https://duckduckgo.com)).
eg: My favorite search engine is [Duck Duck Go](https://duckduckgo.com).

###########################################################################################################################

