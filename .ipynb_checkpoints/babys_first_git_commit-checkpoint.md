# Baby's First Git Commit

Replace `<placeholders>` with your values.

## Local vs. remote

- **Remote** (`origin`): the repo on GitHub, shared with the team.
- **Local**: your copy on disk. Commits stay local until you `git push`.

```bash
git clone <url>   # remote -> local (once)
git pull          # remote -> local (updates)
git push          # local -> remote
git remote -v     # show remote URL
git status        # branch + changed files
```

## Setup (once)

```bash
gh auth login

git config --global user.name "<Your Name>"
git config --global user.email "<you@example.com>"
```

## Clone

```bash
git clone https://github.com/<org>/<repo>.git
cd <repo>
```

## Branch

```bash
git checkout -b <your-name>-analysis
```

## .gitignore

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

```bash
git add .gitignore
git commit -m "Add .gitignore"
git push -u origin <your-name>-analysis
```

## Daily loop

```bash
git pull
git status
git add <file>
git commit -m "<message>"
git push
```
