The basic steps for creating a pull request are explained in [CONTRIBUTING.md](https://github.com/junit-team/junit/blob/master/CONTRIBUTING.md). This page helps you with the more difficult parts of pull requests.

## Squashing commits

Sometimes you add further commits to your pull request in order to apply the recommendations of the
code review. Your commit log may look like this:

    d9b90bc Add feature X
    15c925c Apply code review
    dc23211 Apply further code review

Usually we ask you for squashing the feature commit and the code review commits. It means that they
merged into a single commit. This can be done using `git rebase`.

    git rebase -i HEAD~3

Replace the number 3 with the number of commits you want to squash. If you don't know how many commits to squash, **and** you haven't previously merged to your bran h from master, you can tell git to look at all commits you made on your branch since you branched off of `master`:

    git rebase -i master

After executing either command git opens your editor with the following file:

    pick d9b90bc Add feature X
    pick 15c925c Apply code review
    pick dc23211 Apply further code review

Change line 2 and 3 by replacing `pick` with `squash`.

    pick d9b90bc Add feature X
    squash 15c925c Apply code review
    squash dc23211 Apply further code review

When you save this file, git squashes the commits and your commit log has now a single commit that
consists of the changes of the three former commits.

    e52a32c Add feature X

You may want to merge from master before re-pushing to github:

    git checkout master
    git fetch upstream
    git merge upstream/master master
    git push
    git checkout your-branch
    git merge master
    git rebase -i origin/master
    git push --set-upstream origin your-branch

Your git graph is now incompatible with the remote on GitHub. Therefore you must use the `force`
flag for pushing.

    git push --force --set-upstream origin your-branch
