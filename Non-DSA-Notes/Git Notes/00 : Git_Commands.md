
* Refer Git Notes :
  - 01 : index.html
  - 02 : index.html

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

* **Git Remotes :**

* $ git remote -v
    - origin https://github.com/you/project.git (fetch)
    - origin https://github.com/you/project.git (push)

* Connect to remote repo: (# Add a remote$ )
  - git remote add origin "repo-URL" 

* Push changes to remote repo: (# Push your commits to remote). pushing for the first time:
  - git push -u origin 'feature_branch_Name'
  - git push --set-upstream origin your_branch_name.
    then, just git push

  - -u (or --set-upstream) creates a link between your local branch and the remote branch.
    
* sync your local repo with repo: (# Pull latest changes from remote)
  - git checkout main
  - git pull origin main

* fetch changes : (# Fetch changes without merging (safe peek))
  - $ git fetch origin   


* git push : Upload your local commits to the remote. "Hey GitHub, here's my new work!"
* git pull : Download AND merge remote changes. pull = fetch + merge
* git fetch : Download changes but don't merge yet. Safe way to see what's new before integrating.

* **Typical Workflow :**
  1. git pull origin main — Get latest changes
  2. Make your changes, commit locally
  3. git push origin main — Share your changes

-----
-----

* Understanding Remote Tracking Branches : When you clone a repo, Git creates TWO types of branches locally:
  -  Local Branches (Read + Write) : You can checkout these. You can commit to these. You can modify these. These are YOUR working copies
    - main
    - feature/login
  -  Remote Tracking Branches (Read Only) : You cannot commit to these. These are bookmarks showing where remote was. Updated ONLY by fetch or pull. Like a "last known position" of remote.
    - origin/main
    - origin/feature/login

* Fetch vs Pull: The Real Difference

1) git fetch : Safe! You can review changes before merging.
   - Downloads new commits from remote
   - Updates origin/main (tracking branch)
   - Does NOT touch your local main
     
2) git pull : Convenient! But may cause merge conflicts.
   - Runs git fetch first
   - Then runs git merge origin/main
   - Modifies your local main


* Use git fetch when:
  - You want to see what changed before merging
  - You're not sure if merging will cause conflicts
  - You want to compare: git diff main origin/main

* Use git pull when:
  - You trust the remote changes
  - You want to quickly sync up
  - You're ready to handle any merge conflicts
------------
------------

* **Integrating Changes :** You're working on a team. Someone created a feature branch from main. Meanwhile, main has also moved forward with new commits. Now we need to combine them.

  **1) Merge commit :** Merge creates a new commit that combines both branches. The merge commit has two parents.
    - A merge commit is special — it has two parents instead of one.
    - Records integration point — "These two timelines converged here"
    - Preserves history — You can see that work happened in parallel
    - Easy to undo — git revert -m 1 <merge-commit> undoes the entire merge
    - Safe — Never changes existing commits, only adds new ones
      
    - git checkout main  (# First, switch to the branch you want to merge INTO)
    - git merge feature/login (# Then merge the feature branch)

    * **Advantages :**
      - Non-destructive operation
      - Complete historical record
      - Safe for shared branches
      - Easy to understand
        
    * **Merge Considerations :**
      - Creates extra "merge commits"
      - History can look cluttered with many branches
      - Harder to see linear progression

  **2) Rebase:** The Clean History Alternative. Rebase replays your commits on top of another branch. Instead of creating a merge commit, it rewrites history to appear as if you branched off from the latest commit. Rebase replays your commits on top of another branch, creating a linear history.
     - git checkout feature/login  (# From your feature branch)
     - git rebase main  (# Replay your commits on top of main)
       
     -  **Never rebase commits that have been pushed to a shared repository.**
     -  **Rebase creates new commits with new hashes. If someone else has the old commits, their history will diverge from yours — causing massive headaches.**
 


* **Use Merge When:**
  - Combining feature branch into main
  - Working with shared branches
  - You want to preserve "when did we integrate"
  - Default choice when unsure

* **Use Rebase When:**
  - Cleaning up local commits before pushing
  - You want to update your feature branch with the latest changes from main.
  - You want a clean, linear history
  - Commits haven't been shared yet

------
------

* Merge Conflicts : A conflict occurs when Git can't automatically merge because the same lines were changed differently in both branches.

* What a Conflict Looks Like in Your File :
  - <<<<<<< HEAD (Start of conflict (your version))
  - ======= (Separator between versions)
  - >>>>>>> branch (End of conflict (incoming version))


* How to Resolve a Merge Conflict :
  1) Git tells you there's a conflict
     - $ git merge feature/new-pricing
     - Auto-merging config.py
     - CONFLICT (content): Merge conflict in config.py
     - Automatic merge failed; fix conflicts and then commit.
       
  2) Open the file and decide what to keep
     - Keep YOUR version (HEAD)
     - Keep THEIR version (incoming)
     - Keep BOTH (if they should both exist)
     - Write something completely NEW
    
  3) Edit the file to resolve : Make sure to remove ALL conflict markers: <<<<<<<, =======, >>>>>>>
  4) Stage and commit the resolution
     - $ git add config.py
     - $ git commit -m "fix: Resolve pricing conflict, keep original price"
 

* 🆘 Help! I'm confused and want to start over. How do I abort a merge?
  - If you're in the middle of a conflicted merge and want to cancel it completely: This returns your working directory to the state before the merge. No harm done!
  - $ git merge --abort
 
* More Git Tools to Know :
  - 📦 git stash — (Temporarily save uncommitted changes)
    - $ git stash
    - $ git checkout other-branch (# Do other work, switch branches, etc.)
    - $ git checkout original-branch (# Come back and restore your changes)
    - $ git stash pop
    - $ git stash list (# View all stashed changes)

  - Git reset             : git reset --hard HEAD~1
  - ↩️ git revert abc     : Undo pushed commits safely
  - ✏️ git commit --amend : Fix the last commit
  - 🔮 git reflog         : Your Git Time Machine (Find "lost" commits)
  - 🍒 git cherry-pick    : Copy a specific commit
  - 🔍 git bisect         : Find which commit broke something
  - 🏷️ git tag            : Mark releases and versions
-----
-----

* Pull Requests (PRs) : A Pull Request is a proposal to merge your changes into another branch. It's where code review happens.
 
* create PR:
  - after PR is merged, delete your feature branch. push changes to your remote branch, then delete the branch locally first.
  - git branch -d 'feature_branch'

* to delete from remote repo:
  - git push origin --delete 'feature_branch'


* The Pull Request Lifecycle :
  1) Create a Branch & Make Changes: Work on your feature branch, commit your changes locally.
  2) Push to Remote : git push origin feature/your-branch
  3) Open a Pull Request : On GitHub, click "New Pull Request". Write a description of your changes.
  4) Code Review : Teammates review your code, leave comments, request changes.
  5) Merge! : Once approved, click "Merge Pull Request". Your code is now in main!

 
----
----

* Commit Often : Small, focused commits. Not one giant commit at end of day. Each commit should do one thing.
* Meaningful Branch Names : feature/user-auth, fix/payment-bug, refactor/api-cleanup — not my-branch.
* Review Before Commit : git diff to see changes. git diff --staged to see what's about to be committed.
* Never Commit Secrets : API keys, passwords, .env files — add to .gitignore. Once committed, they're in history forever.

----
----

* Practice & Resources :
  - [Visual Git Guide](https://marklodato.github.io/visual-git-guide/index-en.html)
  - [Learn Git Branching](https://learngitbranching.js.org/)
  - [ohmygit : game about learning git](https://ohmygit.org/)
  - [gitmastery.me : interactive challenges](https://gitmastery.me/)



----
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

