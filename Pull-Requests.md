The basic steps for creating a pull request are explained in [CONTRIBUTING.md](https://github.com/junit-team/junit/blob/master/CONTRIBUTING.md). This page helps you with the more difficult parts of pull requests.

## Merging from master

If a pull request stays open for a while, often other people submit changes to touch the same file, so you need to merge in those changes.

    git checkout master
    git fetch upstream
    git merge upstream/master master
    git push
    git checkout your-branch
    git merge master
    git push --set-upstream origin your-branch

## Squashing commits

Sometimes you add further commits to your pull request in order to apply the recommendations of the
code review.

First, you may want to merge from master (see **Merging from master** abovce).

Many people suggest using `git rebase` to squash commits, but it's hard to use correctly and doesn't work well if you have already merged into the branch. Instead, we will create a new branch and reapply the changes there:

    git branch -m your-branch your-branch-orig
    git checkout -b your-branch master
    git read-tree -u -m your-branch-orig
    git commit

Give the commit message a good message for the overall commit.

Your git graph is now incompatible with the remote on GitHub. Therefore you must use the `force`
flag for pushing.

    git push --force --set-upstream origin your-branch
