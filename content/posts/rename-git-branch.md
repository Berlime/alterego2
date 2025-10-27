---
date: 2025-09-12T16:57:01+08:00
lastmod: 2025-09-12
showTableOfContents: true
title: Rename Git Branch
type: post
tags:
  - github
  - dev
---
To rename a Git branch, you must ==update the name locally first, then push the changes to your remote repository, and finally, delete the old branch from the remote==. 

Rename a local-only branch

If your branch has not been pushed to the remote repository yet, the process is straightforward. 

1. Switch to the branch you want to rename using `git checkout`.
    
    sh
    
    ```
    git checkout <old-name>
    ```
    
    Use code with caution.
    
2. Rename the local branch using the `git branch -m` command.
    
    sh
    
    ```
    git branch -m <new-name>
    ```
    
    Use code with caution.
    
    _Note: If you are not on the branch you want to rename, you can pass both the old and new names to the command: `git branch -m <old-name> <new-name>`._ 

Rename a branch that has been pushed

If the branch already exists on a remote repository (e.g., GitHub, GitLab, or Bitbucket), follow these additional steps.

1. Rename your local branch using the steps above.
    
    sh
    
    ```
    # Switch to the branch you want to rename
    git checkout <old-name>
    
    # Rename the local branch
    git branch -m <new-name>
    ```
    
    Use code with caution.
    
2. Push the new branch to the remote repository and set it to track the new remote branch.
    
    sh
    
    ```
    git push -u origin <new-name>
    ```
    
    Use code with caution.
    
3. Delete the old branch from the remote repository.
    
    sh
    
    ```
    git push origin --delete <old-name>
    ```
    
    Use code with caution.
    
     

Tell your team about the change

If others are collaborating on the repository, you should inform them of the change so they can update their local environment. They can do so with the following commands: 

1. Go to their local repository and fetch all changes from the remote.
    
    sh
    
    ```
    git fetch origin
    ```
    
    Use code with caution.
    
2. Switch to the `main` branch.
    
    sh
    
    ```
    git checkout main
    ```
    
    Use code with caution.
    
3. Delete their local reference to the old branch.
    
    sh
    
    ```
    git branch -d <old-name>
    ```
    
    Use code with caution.
    
4. Set up the new remote branch to track a new local branch.
    
    sh
    
    ```
    git checkout --track origin/<new-name>
    ```
    
    Use code with caution.