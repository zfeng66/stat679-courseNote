# STAT 679 course note:
## git and GitHub to track and share versions

I extracted some important content from [this website](http://cecileane.github.io/computingtools/pages/notes0929.html).

### pushing to github to work with others

```zsh
git remote -v
git remote add origin git@github.com:cecileane/zmays-snps.git
git remote -v
git branch
git push -u origin master  # -u is to remember to "track" this remote place
```

### pulling from github

clone:
```zsh
# you do this, after checking that you are outside of a git repo:
git clone git@github.com:cecileane/zmays-snps.git
cd zmays-snps
git remote -v
```

update:
```zsh
echo "Samples expected from sequencing facility 2020-09-30" >> readme.md
git commit -a -m "added information about samples"
git push origin master # or just "git push" if my branch "master" knows what it's tracking
git log --pretty=oneline --abbrev-commit
```

Very important:
- pull often!
- commit your changes before pulling. Any change to an uncommitted file would stop the pull update.

### resolving conflicts and merge commits

```zsh
# collaborator does this:
echo -e ", downloaded 2020-09-26 from\nhttp://maizegdb.org into /share/data/refgen3/." >> readme.md
git commit -a -m "added download info"
git push origin master
# Cecile does this:
git commit -a -m "added genome download date"
git push origin master # Ahh, problem!!
git pull origin master
git status # conflict. tells me what to do to resolve it
git log --pretty=oneline --abbrev-commit
```

Resolve merge conflict manually, then push the conflict resolution.
```zsh
git status
git add readme.md
git status
git commit -a -m "resolved merge conflict in readme.md"
git status
git log --abbrev-commit --pretty=oneline --graph
git push origin master
```

Comments:
- merge commits have 2 parents, unlike usual commits.
- if you feel overwhelmed during a merge, do `git merge --abort` and start the various merge steps from scratch.
- remember: `git status` gives instructions
