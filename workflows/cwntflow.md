# Cwntflow Workflow

> Git Workflow inpired by Gitflow

<!-- toc -->

- [Git Team Workflows Best Practices: Merge or Rebase?](https://www.atlassian.com/git/articles/git-team-workflows-merge-or-rebase)
- Learn to use email with git! https://git-send-email.io/ (git email workflow)
* <https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows>
* <https://mirrors.edge.kernel.org/pub/software/scm/git/docs/gitworkflows.html>
* <https://martinfowler.com/articles/branching-patterns.html>

### Git Feature Branch Workflow

Project branches:

- master: code in production
- staging: code to be tested
- develop: code in development
    - branches of develop: issues/features/elements to be implemented

#### A) Implementation: `user-dev`

1) Update develop branch

```sh
git checkout develop
git fetch origin
git reset --hard origin/develop
```

2) Create a new branch with the name of the issue/feature/element

```sh
git checkout -b new-feature
```

3) Update, add, commit, and push changes
4) Push feature branch to remote

#### B) Review: Open Pull Request (PR)

1) `user-dev` opens a PR
    - can be just a tag inside the issue `new-feature`
2) `user-reviewr` pulls `new-feature` and starts reviewing the PR's `new-feature` branch

```sh
git pull origin new-feature
git checkout new-feature
```

3) `user-reviewr` reviews `user-dev`'s code
4) `user-dev` can make any adjustments in his local repository and push changes to remote
5) `user-reviewr` pulls new `user-dev` changes and review cicle continues
6) `user-dev` pushes final branch version
7) `user reviewr` pull/pushes final reviewd code, sealing this branch

#### C) Close PR: Merge/Publish feature

1) Merge `develop` to `new-feature` branch

a) ensure that HEAD is pointing to the correct merge-receiving branch
b) Make sure the receiving branch and the merging branch are up-to-date
```sh
git checkout receiving-branch
git fetch
git reset --hard origin/develop
git merge develop
```

2) `user-authority` merges `new-feature` branch to `develop`

2.1) Possible merge strategies:

a) simple merge commit

```sh
git checkout develop
git merge new-feature
```

b) squashes your `new-feature` branch down to one commit

```sh
git checkout develop
git merge --squash new-feature
# https://randyfay.com/comment/1093#comment-1093
```
or
```sh
git merge --no-commit --no-ff $BRANCH
# to examine the staged changes:
git diff --cached
# And you can undo the merge, even if it is a fast-forward merge:
git merge --abort
# [Is there a git-merge --dry-run option?](https://stackoverflow.com/questions/501407/is-there-a-git-merge-dry-run-option)
```

3) delete that brach from local and remote (if needed)

```sh
git branch -d branch-name
# to delete remote branch too
git push origin -d branch-name
```

Or, to cleanup branches from project, see[^clear-branches].

#### References

- [Git Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
- [What is the difference between git pull and git reset --hard origin/<branch>?](https://stackoverflow.com/questions/43037293/what-is-the-difference-between-git-pull-and-git-reset-hard-origin-branch)
- [Git merge conflicts](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts)
[^clear-branches] [How to Delete Already Merged Git Branches (local and remote)](https://www.w3docs.com/snippets/git/how-to-delete-already-merged-git-branches.html)
    - https://github.com/hartwork/git-delete-merged-branches
