# And Git was Good.
  
  
## Intro

Democracy is not a perfect political organization system, but it's the best the world has. And git is the best version control system the world has, but it is not perfect.  
  
So we have a standard that we follow to keep the quality of our code as high as possible. We have rules in place to give a reference to 90% of the situations you'll find yourself in. But for the other 10% you'll be on StackOverflow, you'll be asking your coworkers for thoughts, and they'll be asking you as well.  
  
We use a rebase flow for all of our repositories, and that may be new to you. We also have a specific style for our git commits with a `basic` and a `full` version.  
  
The rules below are clear and simple. And when we all follow them, we make more clients happy.  
  
And you may find ways to improve this document. So if you do submit a pull request, you'll make everyone happy!  
  
  
## Branching
All of our projects have two main branches, `master`, and `next`. Then we do work based on branches off of `next`.
  
`master`: Production branch. This is code that's live for the project.  
`next`: Staging branch. This represents what will be included in the next release. 
  
As we work on features, we branch off of the `next` branch: `git checkout -b feature/new-nav-bar`.  
  
Working branches have the form `<type>/<feature>` where `type` is one of:  

- feat
- fix
- hotfix
- chore
- docs
- refactor  

**In Process Branches**  
Have a branch that's not complete, but want to share it? Use `<type>/<feature>` where `type` is one of:  
  
- discuss  
- temp  

## Commit Messages
### Basic
`<type>(<scope>):<subject>`  
  
Your basic commit messages should have a **type**, **scope**, and **subject**. _Type_ is one of the types listed above. _Scope_ is the area of the code that the commit changes. And _subject_ is a brief description of the work completed.
### Full
```
# <type>(<scope>): <subject>


# Why was this necessary?


# How does this address the issue?


# What side effects does this change have?


```
  
We all like to write code that is so elegant that it's function is self-evident. But when we what we've done is not so obvious, having a full commit message is necessary.  
  
We use this template in our `.gitmessage` file so that we can easily write descriptive and useful commit messages for our colleagues. 

## Merging 
### Rebasing
When you're ready to merge your branch, you rebase your commits to get the latest from the `next` branch. 

From your branch:  
```
git fetch
git rebase origin/next
```

Rebasing gives a straight-line history of commits for the repository, avoids message `merge` commits, and leads to fewer conflicts. (YouTube: _[Rebase as an Alternative to Merge](https://www.youtube.com/watch?v=PnHlnx_nmCI)_)
  
When you've done the above, push your branch and submit a Pull Request:
```
git push -u origin <branch-name>
```
  
### Making Changes
If you need to modify your code before it is accepted, please make the necessary changes.
  
Only make new commits if it makes sense. Otherwise, you should amend your commits or rebase your branch with new changes:

1. `git rebase -i next`
2. `make updates to chosen commits`  
_note: you MUST do `git rebase -i next` before making changes to your code otherwise you will run into an unstaged changes error._  

  
You'll edit any commits that are effected by the request for changes. `git rebase -i next` opens your editor with a list of commits. Where appropriate, change 'pick' to 'edit'. 

For each commit you're editing git will pause the rebase for you to make your modifications.

When you're done making changes to your files and ready to move to the next commit for editing:
```
git add .
git rebase --continue
```


When you're done modifying all commits, force push your changes:
```
git push origin <branch-name> -f
```

At that point close your existing pull request and open a new one. 
