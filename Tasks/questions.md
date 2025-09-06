### Answer the following questions in you own words.

> It's not necessary that you havee to know and answer all the questions. Just answer the ones
> you know and write in your own words.

1. Give the difference between the remotes - upstream and origin - with an example.

You answer: origin is the default name that git gives to the remote connection on one's local machine when they clone their fork whereas the connection to the original repository is called upstream (from which origin is forked from) which is used to fetch updates from the main repo.

eg : Suppose there is a github project and when you clone it, it becomes the origin. To keep your fork up to date with the original repository, we add upstream `git remote add upstream <repo_url>`. In order to update your origin you need to run `git fetch upstream` and merge the changes `git merge upstream`.

---

2. You have two branches A and B and you have currently made some changes in branch A.
You want to move into branch B but do not want to commit the current changes in branch A.
What will you do?

You answer: `git stash` is used here which save the modifications in branch A and cleans the workin directory then one can go to branch B (`git checkout B`) to make make and commit the changes. Once you are back to branch A(`git checkout A`) the modifications can be brought back by `git stash pop`.

(This is generally suggested for unfinished workin branch A or else one can always commit the changes and move to branch B).

---

3. You were assigned a work to implement a feature and create a PR to your organization's remote repository.
For this you made a branch (say A) and made some changes and commited them. Now you moved to some other branch 
(say B) to do some other assigned work. But later you realisd that have to complete the task assigned earlier 
first and commited some changes in branch B which are meant for branch A. How will you use git to bring the 
changes from branch B to branch A?

You answer: First to uncommit the changes we need to run `git reset HEAD~1` and then to save the modifications in branch B `git stash`. Now we need to switch to branch A `git switch A` and then apply the saved changes here `git stash pop`. Now use `git commit -m "..."` to finally commit them in the correct branch.

---

3. What is the difference between fetching changes and pulling changes?

Your answer:  we use fetch to download the changes that we made in the original repo (using ustream), but the changes won't directly get added into the current working directory until one merges them. But pulling does both fetching and automatically merging them into the working files of the current branch.

---

4. What does -i flag stand for? What is it's significance in git?

You answer:

---

5. You are working in an organization that follows very strict guidelines for PRs and commits.
You made three commits in your PR and the maintainer says you were supposed to make a single commit.
What will you do in this case?

You answer: `git reset --soft <commit>`  can be used here. As we need to go back 3 commits we use `git reset --soft HEAD~3` which reset back 3 commits before HEAD but doesn't unstage them so we can commit the changes one last time by `git commit -m "..."`.

---

6. Explain `git merge` and `git rebase` with example(s).

You answer: `git merge [branch-name]` is used to combine changes made in one branch to another whereas `git rebase` generally takes the commits of that branch to the latest point of the other branch.The history of commits now will look linear(instead of branched).

---

7. Write the flow how you create a repository and push changes to it. Also mention the commands used at each step.

You answer: 
* `git init` – creates a Git repository inside the folder  
* `git add .` – adds all the files that have been created  
* `git commit -m "..."` – saves the files at that point with a commit message  
* `git remote add origin <git_repo_link>` – links the local repo with GitHub  
* `git push -u origin main` – pushes the changes into the repository 

(or else one can directly create a repository from GitHub using  `git clone <repo_link>`, then add the files, commit them, and directly push those into the repo)  

---

8. How would you prevent a file or folder from getting tracked by git?

Your answer: To prevent this, we need to create a file called `.gitignore`.  When we run `git add .` these files will get skipped. In case somebody has accidentally committed a file without further pushing it, then `git rm --cached [file-name]` can be used to stop Git from tracking the file (generally `.env` or `config.json`).  

---

9. You did not implement the step you mentioned in question 8 and now you have committed and pushed your database's
secret key to the github. How will you remove the key from your git's commit history to avoid any misuse?

You answer: Firstly, I would run `git rm --cached [file-name]` to stop git from tracking it further and add it to `.gitignore`. The time when I by mistakenly pushed the env file with api keys I used BFG Repo-Cleaner where I mirror cloned my repo and erased all `.env` files from the history and pushed it back again. But later I found out that there is a better method i.e `git filter-repo` to rewrite Git history by deleting the secret key from all past commits. 
