# Lifting SuRun from Subversion

Most VCS conversions are horrible, `reposurgeon` addresses this. This project is an attempt of lifting SuRun from its Subversion repo all the while keeping the most important aspects of its history.

PS: this also is a small-scale demo of `reposurgeon`, which these days has been rewritten in Go, but when I last dabbled with it was written in Python.

## Preparational steps

1. use `svnrdump` to dump SuRun repo into, e.g. `surun.svndump`
2. use `svnadmin create` to create a local repo
3. use `svnadmin load $LOCALREPOPATH < surun.svndump`
4. use GNU make to have `reposurgeon` lift the repo contents, using the provided lift script

## More hints

* `git log --pretty=format: --name-only --diff-filter=A | sort -u | tee ../files.txt` to list all files that ever existed
* `git log --name-only --pretty=format: | sort | uniq -c | sort -nr | grep '\.png$' | awk '$1 ~ /1/ {$1=""; print}' | sed 's|^\s*||g' | tee ../single-commit-png-files.txt` list `.png` files with only a single commit
