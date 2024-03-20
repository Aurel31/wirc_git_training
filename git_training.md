# Git Sandbox Tutorial

Welcome to the Git Sandbox Tutorial! This guide is designed to help you understand and practice basic Git operations, including managing branches, merges, handling conflicts, and collaborating with others in a simplified workflow.

## 1. Setting up your sandbox

Before we start, ensure you have Git installed on your computer.
For this tutorial, you will play the role of two people, Alice and Bob, working together on a project.
Follow these steps to set up your local sandbox environment:

1. **Create a Sandbox repository**: This will be your working directory for this tutorial.
   ```bash
   mkdir -p git_sandbox
   ```
2. **Create a Bare Repository**: This will act as our "remote" central repository.
   ```bash
   mkdir -p git_sandbox/remote_git_repo
   git init --bare git_sandbox/remote_git_repo/MyRemoteRepo.git
   ```
3. **Create Alice and Bob repositories**: This will represent the local machine of two users.
   ```bash
   mkdir -p git_sandbox/Alice git_sandbox/Bob
   ```

## 2. Adding Content to the Local Repository

For this first step, Alice is working on her own and locally (for this tutorial, it means working in Alice’s directory and changing files without pushing on the remote). First, she clones the remote repo
```zsh
cd git_sandbox/Alice
git clone ../remote_git_repo/MyRemoteRepo.git AliceLocalRepo
```
As the repository is empty, a warning should say `warning: You appear to have cloned an empty repository.`. There is nothing to worry about; Alice will add some content to this repo.
Now that Alice has cloned the repository, it's time to add some content. She will create a file named `file.txt` containing some initial text.

1. **Navigate to Alice's Local Repository**:
   Make sure you are in the correct directory:
   ```bash
   cd AliceLocalRepo

2. **Create a New File**:
   Alice now creates a file named `file.txt` and adds some content to it:
   ```bash
   echo "This is a list:" > file.txt
   ```

3. **Add the File to the Repository**:
   To track the file with Git, Alice needs to add it to the staging area:
   ```bash
   git add file.txt
   ```

4. **Commit the Changes**:
   With the file added, Alice can now commit the changes to her local repository:
   ```bash
   git commit -m "Added file.txt with initial content"
   ```

5. **Add more content and commit again**:
   Alice now creates a file named `file.txt` and adds some content to it:
   ```bash
   echo "- item 1" >> file.txt
   git add file.txt
   git commit -m "Add item 1 to list"
   ```
   
Alice has successfully added a new file to her local repository and committed the changes. This demonstrates the basic workflow of making changes and saving them with Git.

## 3. Branching and Merging with Alice

Now that Alice has made her initial commits to the master branch, let's explore branching and merging. Branching allows us to diverge from the main line of development and work on new features or changes in isolation, while merging allows us to bring those changes back into the main branch.

#### Questions
- **Q3.1** *Creating a New Branch*: How can Alice create a new branch named `develop` and switch to it?
- **Q3.2** *Making Commits on the Develop Branch*: Once on the `develop` branch, Alice decides to add a new item to the list called `item 2`. How can she add and commit changes to the `develop` branch with a meaningful commit message?
- **Q3.3** *Merging Develop into Master*: After adding the new item on the `develop` branch, Alice needs to merge these changes back into the `master` branch. What steps should she follow to successfully merge `develop` into `master` without losing any work?

## 4. Handling Merge Conflicts with Alice

In this part of the tutorial, we'll explore how to handle merge conflicts with Alice's project. Merge conflicts occur when Git cannot automatically reconcile changes in two branches, and they need to be resolved manually. We'll intentionally create a conflict to learn how to resolve it.

#### Questions
- **Q4.1** *Adding item 4 on master*: Alice needs to add another item to her list, but this time directly on the `master` branch. How can she add `- item 4` to `file.txt` while on the `master` branch?
- **Q4.2** *Adding item 3 on develop*: Now, without knowing about the changes on `master`, Alice also wants to add `- item 3` to the same list in `file.txt`, but on the `develop` branch. How can she do this?
- **Q4.3** *Merging and solving the conflict*: Alice realizes that both branches have changes to the same part of `file.txt` and decides to merge `develop` into `master`. How can Alice merge the branches and resolve the conflict so that `file.txt` ends up with an ordered list including "item 1, item 2, item 3, item 4"?

This scenario is designed to mimic real-world situations where developers work on different features or bug fixes simultaneously. Understanding how to resolve merge conflicts is essential for maintaining a smooth and efficient workflow in collaborative projects.

## 5. Advancing with Remote Collaboration and GitFlow

As we continue our journey with Alice, it's time to explore more complex workflows involving remote repositories and adopting a simplified GitFlow approach. GitFlow is a branching model for Git, designed around project releases. This part of the tutorial will cover merging changes between branches to keep them up-to-date and pushing branches to a remote repository to facilitate collaboration.

#### Next Steps for Alice

Alice is ready to synchronize her work with the remote repository and lay the groundwork for collaborative development using GitFlow. Here's what she needs to do next:

1. **Merge `master` into `develop`**: This ensures that `develop` contains all the updates from `master`, keeping the project history consistent and up-to-date.
    ```bash
    git checkout develop
    git merge master
    ```
3. **Create a new feature branch from `develop`**: Alice will start working on a new feature in a separate branch, following the GitFlow practice of branching off from `develop` for new features. She also adds an new item to the list
    ```bash
    git checkout -b alice_feature
    echo "- item 5" >> file.txt
    git add file.txt
    git commit -m "Add item 2 to the list"
    ```
4. **Push `master`, `develop`, and the new feature branch to the remote repository**: This makes her changes available to other collaborators and integrates the remote repository into her workflow.
    ```bash
    git checkout master
    git push -u origin master
    git checkout develop
    git push -u origin develop
    git checkout alice_feature
    git push -u origin alice_feature
    ```

#### Bob Joins the Project

Bob is now ready to collaborate on the project with Alice. To start, Bob needs to clone the repository to his local machine. This will give him access to all the branches, including `master`, `develop`, and Alice's feature branch `alice_feature`.
```bash
cd ../../Bob
git clone ../remote_git_repo/MyRemoteRepo.git BobLocalRepo
cd BobLocalRepo
```
#### Questions
- **Q5.1** *Create a new branch for Bob's developments*: Bob wants to contribute. He wants to add a file "new_file.txt" with the content "this is a new file". To follow our gitflow paragigm and the previous branches naming convention, what should he do?
- **Q5.2** *Alice wants to share her developments with Bob*: On her side, Alice thinks that her developments can be shared with the dev team using the develop branch. She needs to merge her branch with develop and share it remotely. What strategy does she have to use?
- **Q5.3** *Bob wants to add his new features to develop*: Bob wants to add his new developments to the changes Alice made on develop. What is the process for doing this?
- **Q5.4** *Bob wants to make a new release on master*. The development is done. Bob wants to release the new developments through the master branch and create a tag for "1.0". What should he do?
