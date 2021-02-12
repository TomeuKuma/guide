# Questions environment setup session

1. Can you provide a list of the most useful Terminal commands?

* [List of common terminal commands](https://purplemonkeydishwasher.co.uk/ubuntu-terminal-commands/)

2. I have a merge conflict problem when pulling the most recent updates from remote

* Run `git fetch [remote] <branch>` to get recent work from the remote repositories. This command pulls down all the new files and changes that have been committed in remote to your local folder __without__ merging them. It updates your local information about the remote branches.
* Run `git merge [remote]/<branch>` to combine the retrieve modifications with your local files. 
* `git pull [remote] <branch>` is a shortcut for the previous commands. 
* Merge conflicts arise when one tries to combine branches (locally or remotely) with competing commits. It frequently stems when different branches have the same file with competing line modifications. To solve this problem: 
        1. Use `git status` to get a list of the files or lines that originates the conflict
        2. Open the conflicting file. Find the lines that generate the error and fix them (determine the option that best suits you)
        3. Stage and commit the new solution. 
        4. Now you can safety pull the remote repository into your local machine
        
##### Resources 
* [Resolve a merge conflict](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line)
* [About merge conflicts](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-merge-conflicts)
