# Basics

## Useful commands
```
git status
git status -uno # git status but ignore untracked files
git log
git log --oneline
git branch

# see which files your master branch is tracking (change 'master' to whatever branch you want to check)
git ls-tree -r master --name-only
```

## Basic workflow

Make some changes to fileName.txt. `git status` at any time to check your status.

```
git add fileName.txt
git commit -m "Commit message"
git push
```

If you want to make a longer/more detailed commit message then use just `git commit` and a text editor will open.

# Reverting/undoing

Handy guide: https://github.blog/2015-06-08-how-to-undo-almost-anything-with-git/

## See what a file looked like in the past

Let's say we want to see what fileName.txt looked like at some previous commit. Find the relevant commit using `git log` or `git log --oneline`, let's say it has the hash 507c182:

```
git checkout 507c182
```

This puts you in a `detached HEAD` state. You can now see your file(s) as they were in this commit. To get back to the present:

```
git checkout dev
```

(assuming you were in the `dev` branch in the first place).

## Revert a single file to how it was in a previous commit

Reference: https://stackoverflow.com/q/215718/8291169

Let's say you want to revert fileName.txt to how it was in a previous commit. Find the relevant commit using `git log` or `git log --oneline`, let's say it has the hash 507c182:

```
git checkout 507c182 -- fileName.txt
```

you can also do multiple files:

```
git checkout 507c182 -- fileName1.txt fileName2.txt fileName3.txt
```

and you're done. Once you're happy with fileName.txt, just commit as normal. This method doesn't rewrite your commit history.

# Branches

You should do all your development work in a seperate development branch. The `master` branch is for things that are complete and work.

## Creating a new branch

Create and switch to a new branch, which we'll call `dev`

```
git checkout -b dev
```

or do it in two steps

```
git branch dev
git checkout dev
```

If you try to push your new branch to your remote repo using just `git push` you'll get an error message:

```
$ git push
fatal: The current branch dev has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin dev
```

So do `git push --set-upstream origin dev` (or `git push -u origin dev` for short) (assuming the local alias of your remote repo is `origin`, which it probably is).

## Merging branches

In branch `dev`, make some changes to fileName.txt, commit and push as usual to (remote) `dev` branch, i.e.:

```
$ git branch
* dev
  master  
$ git add fileName.txt
$ git commit -m "Commit message"
$ git push
```

Now we're happy with fileName.txt and want the changes we made to be reflected in branch `master`. Switch to the master branch and merge:

```
git checkout master
git merge dev
```

# Initialising a repo/uploading a repo to github

https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/
