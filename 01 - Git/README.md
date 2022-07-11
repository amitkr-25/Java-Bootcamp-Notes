# 01 Git Introduction
- What is version control system(VCS)?
    - Version control (or revision control, or source control) is all about managing multiple versions of documents, programs, web sites, etc.
    - The VCS allows you to capture the content and structure of your files at a certain point in time. You can use the VCS to switch between these versions and you can work on different versions of these files in parallel. The different versions are stored in a storage system which is typically called a repository.
    - Older VCS: 
        - A localized version control system keeps local copies of the files. This approach can be as simple as creating a manual copy of the relevant files.
        - A centralized version control system provides a server software component which stores and manages the different versions of the files. A developer can copy (checkout) a certain version from the central server onto their individual computer.
        - Both approaches have the drawback that they have one single point of failure. In a localized version control system it is the individual computer and in a centralized version control system it is the server machine. Both systems also make it harder to work in parallel on different features. To remove the limitations of local and centralized version control systems, distributed version control systems have been created.
        - CVS and Subversion use a “central” repository, users “check out” files, work on them, and “check them in”.
    - New VCS: 
        - In a distributed version control system each user has a complete local copy of a repository on his individual computer. The user can copy an existing repository. This copying process is typically called cloning and the resulting repository can be referred to as a clone. Every clone contains the full history of the collection of files and a cloned repository has the same functionality as the original repository.
        - Git, Mercurial
    - Benifits
        - Keep track of changes made to files (allows roll-backs)
        - Merge the contributions of multiple developers
- Git: Distributed VCS
    - Git is distributed. Most operations in Git only need local files and resources to operate, every operation in Git is local. If no access to server or VPN, no need to wait till we get the access because everything is available locally if not take it from your friend (peer). **Everyone has the complete history**.
    - Everything in Git is check-summed before it is stored i.e. It has integrity.
    - No central authority
    - Three main stages: **Working Directory**, **Staging Area(index)**, and **Repository**
    - Git allows the user to synchronize the local repository with other (remote) repositories.
    - Users with sufficient authorization can send new versions of their local repository to the remote repositories via the push operation. They can also integrate changes from other repositories into their local repository via the fetch and pull operation.
- Updating global configurations
    - see global configs
        `git config -l`
    - set global username
        `git config user.name "username"`
    - set global email 
        `git config user.email "abc@xyz.com"`
    - set default editor
        `git config global.core.editor notepad++`
- https://stackoverflow.com/questions/34175799/differencies-between-git-add-and-git-stage-command
- See commit history
    `git log`
- viewing changes of a commit
    `git show <commit-id>`
- add and commit in a single command
    `git commit -am "message"`
- deleting a file
    `git rm <filename>`, this will delete and stage the deletion
    `git restore <filename>`, to undo the above action
    - or simply delete and stage and commit
- Correct the changes of the commit with git amend
    - The `git commit --amend` command makes it possible to rework the changes of the last commit. It creates a new commit with the adjusted changes.
    - The amended commit is still available until a clean-up job removes it. But it is not included in the git log output hence it does not distract the user.
    - changing the commit message of the last commit, try to avoid using this and do not run this if already pushed to remote
        `git commit --amend -m "modified message for last commit"`
- Branches
    - git checkout servers three functions 
        1. checking out files
        2. checking out commits: Checking out a commit makes the entire working directory match that commit. View an old state without altering your current state in any way. Let’s you see an old version of that particular file, leaving the rest of your working directory untouched.
        3. checking out branches
    - list avalilable branches
        `git branch`
        `git branch -a`, shows the remote branched too
    - creating a new branch
        `git branch <branchname>`
    - switch to other branch
        `git checkout <branchname>`
    - create and switch to the branch instantly
        `git checkout -b mybranch`
    - create a branch based on master without the last commit(denoted by 1). To make a branch without last 3 commit change 1 to 3
        `git checkout -b mybranch master~1`
    - rename a branch
        `git branch -m old-branchname new-branchname`
    - deleting a branch
        `git branch -d branchname`, if the branch is not fully merged to master this will give error
    - force delete a branch
        `git branch -D branchname`
    - You can push the changes in a branch to a remote repository by specifying the target branch. This creates the target branch in the remote repository if it does not yet exist. If you do not specify the remote repository, the `origin` is used as default
        `git push origin testingbranch`, push current branch to a branch called "testing" to remote repository
    - scenarios
        1. `master` branch 3 files, file1 file2 file3
        2. switch to `branch2`
        3. delete file1 and file2, using `rm -R`, and do not stage any changes
        4. checkout to master
        5. The files will be delted in the master branch as well.
        6. To restore these files `git restore file1 file4`
    - scenario
        1. `master` branch 3 files, file1 file2 file3
        2. switch to `branch2`
        3. delete file1 and file2, using `git rm`, this deleted the files and stages the changes
        4. checkout to master
        5. The files will be delted in the master branch as well.
        6. To restore these files `git restore --stages file1 file4`
        7. Then run `git restore file1 file4`
    - see difference between two branched 
        `git diff branch1 branch2`
    - the following command shows the changes in your_branch and master since these branches diverged. older branch name comes first
        `git diff master...your_branch`
- Tagging in git
    - Git has the option to add additional metadata to commits. This can be used to document for example a commit which is used to perform a software release. This is done via tags
    - Git supports two different types of tags, lightweight and annotated tags.
    - A **lightweight tag** is a named pointer to a commit, without any additional information about the tag.
    - An **annotated tag** contains additional meta data: the name and email of the person who created the tag, tagging message similar to a commit message, the date of the tagging
    - Annotated tags can also be signed and verified with GNU Privacy Guard (GPG).
    - list available tags
        `git tag`
    - create a lightweight tag
        `git tag 1.1.7`
    - see the commit a tag points to
        `git show 1.1.7`
    - You can create a new annotated tag via the git tag -a or the git tag -m "message" command. To specify the tag message, use the -m parameter. 
        `git tag 1.6.1 -m "message"`
        `git tag -a 1.6.2`, youll have to write message explicitly, so use the above command instead
    - You can use the option -s to create a signed tag. These tags are signed with GNU Privacy Guard (GPG) and can also be verified with GPG. 
    - You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by switching back to a branch. If you want to create a new branch to retain commits you create, you may do so (now or later) by using -c with the switch command. Example:  `git switch -c <new-branch-name>` or undo this operation with `git switch -`
    - By default the git push command does not transfer tags to remote repositories. You explicitly have to push the tag with the following command. 
        `git push origin <tag-name>`, push a tag or branch called tagname
    - to explicitly push a tag and not a branch
        `git push origin tag <tagname>`
    - push all tags
        `git push --tags`
    - deleting tags
        `delete tag -d 1.1.7`
    - delete tag in remote repository called origin
        `git push origin :refs/tags/1.7.0`
    - show logs between two tags
        `git log tag1...tag2`
        `git shortlog tag1...tag2`
    - git diff uses
        `git diff`, shows the changes introduced in the working tree compared with the staging area 
        `git diff --cached`, shows the differences between the staging area and the last commit
        `git diff COMMIT_REF1 COMMIT_REF2`, shows the differences introduced between two commit references
        `git diff -- [file_reference]`, shows the differences introduced in the working tree compared with the staging area for (file_reference)
    - git log 
        `git log`
        `git log HEAD~10`, shows the history of commits starting from the HEAD~10 commit
        `git log COMMIT_REF`, shows the history of commits starting from the COMMIT_REF commit
        `git log --oneline`, --oneline - fits the output of the git log command in one line. --oneline is a shorthand for "--pretty=oneline --abbrev-commit"
        `git log --abbrev-commit`, --abbrev-commit - the log command uses shorter versions of the SHA-1 identifier for a commit object but keeps the SHA-1 unique. This parameter uses 7 characters by default, but you can specify other numbers, e.g., --abbrev-commit --abbrev=4.
        `git log --graph --oneline`, graph - draws a text-based graphical representation of the branches and the merge history of the Git repository.
        `git log --decorate`, decorate - adds symbolic pointers to the log output
        `git log -n <number of commits to show>`
        `git log --author="pattern"`
        `git log --grep="pattern"`
        `git log > gitlog.txt`
    - reverting/deleting a commit. The Git revert command undoes a committed snapshot.
        `git revert <commit-sha>`
    - If Git revert is a “safe” way to undo changes, Git reset is the dangerous method. There is no way to retrieve the original copy. It is a permanent undo
        `git reset`, Reset the staging area(after `git add`) to match the most recent commit but leave the working directory unchanged.
        `git reset <filename>`, Remove the specified file from the staging area but leave the working directory unchanged.
    - 
    


    



