---
layout:	post
title:	"Git cheats"
date:	2022-09-02 18:44:55 -0500
audience: developers
excerpt:
---

A small note: this will be much less organized and thought out than my other blog posts because I have been unable to convince myself to write a blog in about 2 years. Instead these are some notes to myself that happen to be public for anyone who finds them useful.

A small note written after spending 5 minutes on this post: holy shit this is so deranged I'm turning into Gankra lmao

# Git

big fan of the data model.
not a fan of the UI.

Ok so before anything else, don't panic. Your code is probably still there somewhere you just can't find it. If you *stop running commands* right now, you can probably get it back.

## I had a commit and then I checked out a different branch and now I can't find the commit again 😭

Run `git reflog`, it shows you all the recent commits you were on.

## someone told me to rebase and I did that but now git says "failed to push some refs"??? why is this happening

The error probably looks like this:
```
$ git push
To github.com:jyn514/rust.git
 ! [rejected]                simplify-storage -> simplify-storage (non-fast-forward)
error: failed to push some refs to 'git@github.com:jyn514/rust.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

This is totally normal. Git just gives absolutely awful error messages. Run `git push --force-with-lease` and it should work fine.

Be careful using `--force`. 99% of the time it works. The other 1% someone else pushed to your branch and you just deleted their work. They will not be happy.

## wait but I ran git pull before I looked at your blog now what do I do???

Your latest commit probably looks like this:
```
commit 88fdea3dd2e876a92960601c019e729401e832ab (HEAD -> simplify-storage)
Merge: d6bd3ef8662 6b22a42e011
Author: Joshua Nelson <github@jyn.dev>
Date:   Fri Sep 2 19:24:33 2022 -0500

    Merge github.com:jyn514/rust into simplify-storage
```

Get rid of it. We don't want it. If you have changes since the latest commit, save them somewhere (e.g. `git stash`).
Then run `git reset --hard HEAD~`. Now go to the step above about `--force-with-lease`.

## I have a detached HEAD

### WTF does that mean

You have turned into the Nick the Headless Horseman. Have fun trying to join the Headless Hunt.

### No stop I came here for help

Git doesn't think you're on a branch or tag.

This is *not* the same as being on a commit that's not in any branch or tag. It's perfectly possible
to be on the same commit as the latest `main` and still have a detached HEAD. It just means that
any new commit you make in this state won't be on a branch.

### How does this help me I don't understand

Everything is fine. All your work is still here. You just need to figure out what you want to do next.

#### I don't care about any of the work I've done in the last day I just want a git repo that works I will wipe this directory if you don't help

DO NOT DO THIS IF YOU HAVE WORK YOU WANT TO SAVE

Run `git checkout --force $(git rev-parse --abbrev-ref origin/HEAD)`. If that gives an error for any reason try `git checkout --force origin/master `or `origin/main` instead. If none of those work IDK what to tell you maybe wiping the repo is the best idea after all. Good luck.

#### I have work I want to save please help me fix this I have a deadline in an hour

Ok. Pick which branch you want to put your work on. I'm going to pick `bark` because branches have bark. haha

Does the commit you're on have the work you want to save?

##### yes how do I get it to work

Run `git branch --delete bark && git checkout --branch bark`. This is the least invasive way to fix things;
whatever untracked code is in your working directory won't be modified, and the old branch will still be in your reflog if you really need it. If you don't know what that means, that's ok, you're on the right branch now and you can push it wherever you need.

##### no please I don't know how I got into this state I really hate git right now

Figure out which commit has the work you want to save. Then run `git checkout <that commit>` and then follow the steps about branches immediately above.

## Git tells me something about "would overwrite untracked files"? idk what that means I just want to pull the latest branch

I'm going to assume the error looks something like this:
```
error: The following untracked working tree files would be overwritten by reset:
        src/tools/rls/Cargo.toml
        src/tools/rls/README.md
Please move or remove them before you reset.
Aborting
fatal: could not move back to 9ba169a73acfa9c9875b76eec09e9a91cc6246df
```

There are three things I can think of that could be going wrong here:

1. You made some changes and didn't commit them. Commit them now. Go. Do it. `git add src/tools/rls && git commit`.
2. This is in a submodule and git got confused. If you don't know what a submodule is, mentally replace it with "code I have never modified and will never want to modify". You can ignore this by running `git deinit -f src/tools/rls` (or whichever directory the submodule starts in - you can check with `git submodule status`).

   DO NOT DO THIS if you have made changes to that directory you want to save. Git will destroy all you hold dear. It is a sharp and powerful tool. You might call it ... a subtle knife.

3. This used to be a submodule and it's no longer a submodule. You tried the `deinit` thing above and it didn't help. Try `rm -rf src/tools/rls`. This does exactly what it looks like, don't do it if you want to save your work.

If none of those fix it, glhf sucks to be you

## I'm in rust-lang/rust and Cargo.lock keeps showing modifications but I definitely didn't touch anything ???

yes this is a very specific problem. no I'm not going to take it out of the blog.

This happens because your submodules are out of date. Run `./x.py --help`, which updates submodules for you.
Under the hood this is running the equivalent of `git submodule update --init --recursive` which makes sure all the rust tool submodules are up to date.

### that didn't help.

sucks to be you

## AAA

yeah no that's it have fun kid