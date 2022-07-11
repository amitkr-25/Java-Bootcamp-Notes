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
    - Three main stages: **Working Directory**, **Staging Area**, and **Repository**
    - Git allows the user to synchronize the local repository with other (remote) repositories.
    - Users with sufficient authorization can send new versions of their local repository to the remote repositories via the push operation. They can also integrate changes from other repositories into their local repository via the fetch and pull operation.
    
- Centralised vs Distributed VC

