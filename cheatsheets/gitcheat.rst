###############
git cheat sheet
###############




checkout remote branch to local
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
To checkout a branch from the repository that is not yet present locally:
::

  $ git checkout --track origin/develop
 
 
This creates a local branch named develop based on on the remote branch "origin/develop".
Git uses the same name for the local branch. 
 
 deleting
 ~~~~~~~~
 
delete branch locally:
::

  $ git branch -d localBranchName

delete branch remotely:
::
  
  $ git push origin --delete remoteBranchName
