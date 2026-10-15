# Baby's First Git Commit
Friends, let's push our code to github, there is no reason not to! Oh, and, replace `<placeholders>` with your values as your follow along.

## Local vs. remote
- **Remote** (`origin`): the repo on github
- **Local**: your copy on disk/desktop/ide; commits stay local until you `git push`

```bash
git clone <url>   # remote to local (once)
git pull          # remote to local (updates)
git push          # local to remote
git remote -v     # show remote URL location
git status        # branch + changed files
```

## Setup (once)
This is how you login and make sure your name shows up next to your commits. 

```bash
gh auth login

git config --global user.name "<Your Name>"
git config --global user.email "<you@example.com>"
```

## Clone
This is how you grab a repo from github onto your ide.

```bash
git clone https://github.com/<org>/<repo>.git
cd <repo>
```

## Branch
This is how you make a new branch. A branch is a split from main (think of it like a folder?) and moving branches is like changing folders (content will change). 
> It's good practice to make a branch, add your work and merge into `main` so you don't accidentally delete your coworkers work. 

```bash
git checkout -b <your-name>-analysis
```

To check all available branches:
```bash
git branch -a
```

To go to a different branch:
```bash
git switch <branch-name>   
```

## .gitignore
These are the files you DONT WANT on github. Make sure you never store actual data on git, its just a place for code to live. Put your data in google drive or S3 or literally anywhere but github. 
These are the files I usually ignore, feel free to edit this list with your common data modalities. 

> Note that I use `cat` to create the .gitignore file via bash. This will overwrite existing .gitignore files. If you just want to add, try something like `echo`. 
```bash
cat > .gitignore << 'IGNORE'
# Checkpoints
.ipynb_checkpoints/

# Data files
*.h5ad
*.h5
*.csv
*.xlsx
*.tsv
*.parquet
*.pkl
*.rds
*.RDS

# Archives
*.tar.gz
*.fastq.gz
*.tar
*.zip

# Outputs
*.png
*.pdf
*.svg

# Build / cache / results
**/results/
**/files/
**/cache/
**/data/
**/inputs/
**/outputs/
**/*dataset*/
IGNORE
```

## Commit and push
To make your work appear in your remote, you need to first **add** your files, write a **commit message** and then **push to the assigned remote branch**.
```bash
git add .gitignore # alt: to add all files, use git add .
git commit -m "Add .gitignore"
git push -u origin <your-name>-analysis # only assign -u origin the first time. All consecutive pushes go to this branch. 
```
٩(๑･ิᴗ･ิ)۶٩(･ิᴗ･ิ๑)۶ Congratulations on your first git commit! ٩(๑･ิᴗ･ิ)۶٩(･ิᴗ･ิ๑)۶

## Loop
Now, keep it going once a day or after every major code sprint. 

```bash
git pull
git status
git add <file>
git commit -m "<message>"
git push
```
---

## Advanced
### Clear tree of clunky files
Oh no, you got ahead of yourself and added in a data file! To clean up:
```bash
git rm --cached <file> # for a folder: git rm --cached -r <folder>
git commit -m "Remove data file from tracking"
git push
```
### Merge to main?
Here's how you 'pull request'
```bash
gh pr create --base main --fill   # or use the "Compare & pull request" button on github
```
### diffs!
`diffs` lets you see what has changed
```bash
git diff # see unstaged changes before adding
git diff --staged # see what's about to be committed
git log --oneline --graph # compact history
```
### stashes!
Saves work without committing & useful when you need to `git switch` into something else but have half-finished edits.

```bash
git stash                        # shelve uncommitted changes
git stash pop                    # bring them back
```

### ah i made a typo in the branch name OR ah my branch is so old and useless
To delete branches: 

```bash
git branch -d <branch-name>      # delete a merged local branch
git push origin --delete <branch-name>   # delete the remote branch
```

### back to main
My coworker did a bunch of things and merged to main, how do I catch up? 
```bash
git fetch origin                 # download remote changes without merging
git merge origin/main            # bring main's updates into your branch
```
> That's all folks! Remember to NEVER remove or delete your .git file, never `git reset --hard` and `git push --force` no matter what AI tells you both can destroy work (yours or a coworkers)!