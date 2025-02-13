## Git Cheat Sheet

This cheat sheet covers basic Git commands for managing your version control.

**Setup:**

* `git init`: Initializes a new Git repository in the current directory.
* `git config`: Sets up your user information for commits.
* `git clone [URL]`: Clones an existing Git repository from a remote URL.

**Basic Workflow:**

* `git status`: Shows the current status of your working directory and staging area.
* `git add [file]`: Adds a file to the staging area for the next commit.
* `git diff`: Shows the difference between your working directory and the index (staged changes) or the last commit.
* `git commit -m "<message>"`: Creates a new commit with a descriptive message.
* `git log`: Shows the commit history of the current branch.

**Branching and Merging:**

* `git branch`: Lists all local branches.
* `git branch [branch-name]`: Creates a new branch.
* `git checkout [branch-name]`: Switches to a different branch.
* `git merge [branch-name]`: Merges another branch into the current branch.

**Remote Repositories:**

* `git fetch [remote]`: Downloads the latest changes from a remote repository without merging.
* `git pull [remote] [branch-name]`: Fetches and merges changes from a remote repository.
* `git push [remote] [branch-name]`: Uploads local commits to a remote repository.

**Additional Commands:**

* `git tag`: Creates, lists, or deletes tags for specific commits.
* `git rm [file]`: Removes a file from the working directory and staging area.
* `git reset`: Discards changes and reverts to a previous state. (Use with caution!)
* `git stash`: Saves your uncommitted changes for later and removes them from the working directory.

**Resources:**

* [https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)
* [https://education.github.com/pack](https://education.github.com/pack)

## Git, merge strategies

In Git, merge strategies define how the repository combines changes from different branches. When you execute a `git merge` command, Git attempts to find a common ancestor commit between the branch you're on (current branch) and the branch you're merging from (target branch). It then analyzes the changes introduced in both branches based on that common ancestor and creates a new "merge commit" that incorporates those changes.

Here's a breakdown of Git merge strategies:

**Default Strategy (Ours):**

* This is the most common strategy, chosen by Git by default in most scenarios.
* It performs a 3-way merge, comparing the current branch head, target branch head, and the common ancestor commit.
* If there are no conflicts (changes to the same lines of code), Git automatically merges the changes and creates a merge commit.
* This strategy is efficient but can lead to merge conflicts if both branches modify the same file sections.

**Other Strategies:**

* **Recursive (deprecated):** Similar to ours but can have issues with complex merges. No longer recommended.
* **Fast-forward:** Applies when the target branch is a direct linear descendant of the current branch. Git simply moves the branch pointer to the target branch's commit, essentially fast-forwarding the current branch.
* **Octopus:** Creates a merge commit with multiple parents (one for each merged branch). Use with caution as it can make history harder to follow.
* **Resolve:** Similar to ours but requires manual intervention to resolve merge conflicts before creating a merge commit.

**Specifying Strategies:**

You can explicitly specify the merge strategy using the `-s` flag with the `git merge` command. For example:

```
git merge -s ours <branch-name>
```

This command uses the "ours" strategy to merge the `<branch-name>` branch.

**Choosing the Right Strategy:**

* For simple merges without conflicts, "ours" (default) is usually sufficient.
* If you anticipate conflicts, using `resolve` allows you to manually address them before creating the merge commit.
* Avoid "octopus" unless you have a specific need for a merge commit with multiple parents.

By understanding merge strategies, you can effectively combine changes from different branches in your Git workflow.

## Git fetch and Git pull

Both `git fetch` and `git pull` are used to update your local Git repository with changes from a remote repository, but they differ in their functionality:

**Fetch:**

* Downloads the latest changes from a remote repository **without merging them into your working directory.**
* Updates the remote-tracking branches in your local repository. (These branches track the remote branches but don't directly correspond to them.)
* Safer option, as it doesn't modify your working directory and avoids accidental merge conflicts.
* Useful when you want to see what changes exist on the remote repository before integrating them.

**Pull:**

* Combines `git fetch` and `git merge` in a single command.
* Fetches the latest changes from a remote repository.
* Attempts to automatically merge those changes into your current branch.
* Convenient option for a streamlined workflow, but can lead to merge conflicts if unaddressed.

**Here's a table summarizing the key differences:**

| Feature          | Fetch (git fetch) | Pull (git pull) |
|------------------|------------------|----------------|
| Downloads changes | Yes               | Yes            |
| Merges changes    | No                | Yes (attempts to) |
| Modifies working directory | No                | Yes (if merge successful) |
| Risk of conflicts | No                | Yes (if changes conflict) |
| Use case          | Preview changes, avoid accidental conflicts | Streamlined workflow |

**In essence:**

* Use `git fetch` when you want to be cautious and review changes before merging.
* Use `git pull` when you're confident about merging the latest changes and want a quicker workflow.

Imagine you and a teammate are working on the same project together, but you both have your own separate copies of the code. Git fetch and merge are commands that help you keep your code in sync with your teammate's work.

**Git Fetch: Downloading Updates**

* Think of `git fetch` like checking your mailbox for new mail from your teammate. 
* It doesn't bring the new mail (code changes) into your inbox (local codebase) yet. 
* It just tells you there's new mail (tells git that there are new commits on the remote server that you can potentially merge into your local code).

**Git Merge: Combining Changes**

* This is where you actually integrate your teammate's work into your local codebase. 
* It's like bringing the new mail (code changes) from your mailbox (remote server) into your inbox (local codebase) and merging it with your existing mail (local code).
* If there are no conflicts (changes in the same part of the code by you and your teammate), the merge happens smoothly.
* But sometimes, there might be conflicts (like two emails replying to the same thread). In this case, git will tell you about the conflict and you'll need to manually fix it by deciding which changes to keep.

**Here's a step-by-step breakdown:**

1. You and your teammate work on your assigned parts of the codebase.
2. You both commit your changes locally (like saving your work in your inbox).
3. You use `git fetch` to check if your teammate has pushed any new commits (like checking the mailbox for new mail).
4. If there are new commits, you can use `git merge` to bring those changes into your local codebase (like merging the new mail with your existing mail).
5. If there are conflicts, git will highlight them, and you'll need to resolve them manually (like fixing conflicting replies in an email thread).

**Benefits of using git fetch and merge:**

* Ensures everyone on the team is working on the latest version of the code.
* Helps prevent errors caused by working on outdated code.
* Makes collaboration easier by allowing everyone to see each other's changes.

**Remember:**

* It's a good practice to `git fetch` regularly to stay up-to-date with the latest changes.
* Always resolve conflicts before committing your merged code.

By using `git fetch` and `git merge`, you can effectively collaborate with your teammates and keep your codebase in sync, ensuring a smooth and efficient development process.

A Git branching strategy is a set of guidelines that define how developers use branches in a Git version control system. Branching is essentially creating a copy of your codebase to work on specific features or bug fixes without affecting the main code. Different branching strategies offer varying workflows depending on your team size, project complexity, and release cadence. Here's a breakdown of three popular strategies:

**1. Git Flow:**

   - Ideal for larger teams with complex projects and multiple releases.
   - Defines specific branches with designated purposes:
      - `master` (or `main`): Holds the production-ready code.
      - `develop`: Branch for ongoing development work.
      - `feature`: Separate branches for individual features.
      - `release`: Branches created from `develop` to prepare for releases.
      - `hotfix`: Branches for urgent bug fixes in production.

   - Developers create feature branches from `develop`, work on their features, and merge them back to `develop` after completion.
   - `release` branches are created from `develop` for stabilizing and testing a release.
   - Once tested, the release is merged into `master` and tagged with a version number.
   - `hotfix` branches are created from `master` to fix critical issues, then merged back to both `master` and `develop`.

**2. GitHub Flow:**

   - Simpler strategy suited for smaller teams or less complex projects.
   - Uses a single `main` branch that stores the deployable code.
   - Developers create feature branches from `main` for new features and bug fixes.
   - When finished, they create pull requests to merge their branch code back into `main`.
   - Code review through pull requests ensures quality and collaboration before merging.

**3. GitLab Flow:**

   - Similar to GitHub flow with an added layer for deployments.
   - Maintains a `main` branch for production-ready code.
   - Uses feature branches for development work.
   - Introduces an environment branch (like `production` or `staging`) to represent the deployment target.
   - Merges are made to the environment branch first for testing before merging to `main`.
   - Offers more control over the deployment process compared to GitHub flow.

Choosing the right strategy depends on your specific needs. Consider factors like team size, project complexity, and desired release workflow. 

Here's a Git branching strategy for your scenario using Dev, QE, UAT, Prod, and hotfix branches, along with the rule that developers fetch changes, update their branch, create a new branch, and then create a pull request:

**Workflow:**

1. **Development:**
    * Developers work on features and bug fixes in their local clones.
    * Before starting work, developers should:
        * `git fetch` to retrieve the latest changes from the remote repository.
        * `git merge origin main` (or your main branch name) to update their local `main` branch with the latest code from the central repository.
    * Developers create a new feature branch from `main` for each specific feature or bug fix they are working on. Use a clear and descriptive naming convention for branches (e.g., `feature/add-search-functionality`, `bugfix/login-error`).
    * Developers commit their changes regularly to their feature branch with meaningful commit messages.
2. **Code Review and Pull Requests:**
    * Once a feature branch is complete and ready for review, the developer pushes it to the remote repository.
    * The developer creates a pull request (PR) from their feature branch to the `main` branch.
    * The PR should include a clear description of the changes made and any relevant testing information.
    * Other developers or reviewers can then review the code, discuss changes, and suggest modifications through the PR interface.
3. **Integration and Testing:**
    * After code review and approval, the feature branch can be merged into the `main` branch. This can be done through the GitHub UI or using the `git merge` command from the developer's local machine.
    * Once merged into `main`, the code can be deployed to a testing environment (e.g., QE) for further testing.  

**Additional Branches:**

* **Release Branch (Optional):** 
    * You can optionally introduce a `release` branch for creating a stable version for deployment to UAT or production. In this case, you would merge approved features into the `release` branch and then deploy from there.
* **Hotfix Branch:**
    * If a critical bug is identified in production, a hotfix branch can be created from the last deployed version (e.g., `main` or `release`). The hotfix is developed and tested quickly, then merged back to both the `main` branch (for future development) and the production branch (to fix the issue).

**Benefits:**

* **Clear separation of concerns:**  This branching strategy keeps development work isolated from the main codebase until it's reviewed and approved.
* **Improved code quality:**  Code review through pull requests helps identify and fix bugs early in the development process.
* **Easier rollback:**  If a problem arises, it's easier to identify the source of the issue by looking at specific feature branches.
* **Collaboration:**  The pull request workflow encourages collaboration and knowledge sharing among developers.

**Remember:**

* Enforce consistent naming conventions for branches to improve clarity.
* Encourage developers to write clear and concise commit messages.
* Utilize code review tools and guidelines to maintain code quality.
* Adapt this strategy to your specific team size, project needs, and release cadence.

**Git reset** is a powerful command in Git that allows you to undo changes in your repository. It can be used to reset the current HEAD to a specified state, effectively changing the commit history. Here are the main types of `git reset`:

1. **Soft Reset (`--soft`)**: Moves the HEAD to the specified commit, but leaves the changes in the staging area (index). This is useful if you want to uncommit changes but keep them staged for a new commit.
   ```bash
   git reset --soft <commit>
   ```

2. **Mixed Reset (`--mixed`)**: This is the default option. It moves the HEAD to the specified commit and resets the staging area, but leaves the working directory unchanged. This is useful for undoing commits and un-staging changes.
   ```bash
   git reset --mixed <commit>
   ```

3. **Hard Reset (`--hard`)**: Moves the HEAD to the specified commit and resets both the staging area and the working directory to match the specified commit. This is a destructive operation as it will discard all changes in the working directory.
   ```bash
   git reset --hard <commit>
   ```

Would you like to know more about how to use any specific type of reset?

**Git Revert** is a command used in Git to undo changes by creating a new commit that reverses the changes made by a previous commit. Unlike `git reset`, which can alter the commit history, `git revert` is a safe way to undo changes because it doesn't remove any commits from the history.

Here's a basic example of how to use `git revert`:

1. **Identify the commit to revert**: Use `git log` to find the commit hash you want to revert.
2. **Revert the commit**: Run `git revert <commit-hash>`. This will create a new commit that undoes the changes made by the specified commit.

```bash
git log
# Find the commit hash you want to revert
git revert abc1234
# This will create a new commit that reverses the changes of commit abc1234
```

Would you like to know more about other Git commands or need help with something specific?

**Git Revert** and **Git Reset** are both commands used to undo changes in Git, but they work in different ways and are used for different purposes:

### Git Revert
- **Purpose**: Safely undo changes by creating a new commit that reverses the changes made by a previous commit.
- **Usage**: `git revert <commit-hash>`
- **History**: Preserves the commit history, making it clear that a change was undone.
- **Example**:
  ```bash
  git revert abc1234
  # Creates a new commit that undoes the changes of commit abc1234
  ```

### Git Reset
- **Purpose**: Move the current branch to a different commit, optionally modifying the index (staging area) and working directory.
- **Usage**: `git reset [--soft | --mixed | --hard] <commit-hash>`
- **History**: Can alter commit history, especially with `--hard` and `--mixed` options.
- **Options**:
  - `--soft`: Moves the branch pointer to the specified commit, but leaves the index and working directory unchanged.
  - `--mixed` (default): Moves the branch pointer and resets the index, but leaves the working directory unchanged.
  - `--hard`: Moves the branch pointer, resets the index, and resets the working directory to match the specified commit.
- **Example**:
  ```bash
  git reset --hard abc1234
  # Moves the branch pointer, resets the index, and working directory to commit abc1234
  ```

### Key Differences
- **Safety**: `git revert` is safer as it doesn't rewrite history, while `git reset` can rewrite history, especially with `--hard` and `--mixed`.
- **Use Case**: Use `git revert` when you want to undo changes without altering the commit history. Use `git reset` when you need to move the branch pointer and potentially modify the index and working directory.

Would you like to dive deeper into any of these commands or have another question?

**Git Amend** is a command used to modify the most recent commit. It's useful for making small corrections, such as fixing a typo in a commit message or adding files that were accidentally left out of the last commit.

### How to Use Git Amend
1. **Make changes**: Edit your files or stage new changes.
2. **Amend the commit**: Use `git commit --amend` to modify the most recent commit.

Here's an example:

```bash
# Make changes or stage new files
git add <file>

# Amend the last commit
git commit --amend
```

### Options
- **Amend the commit message**: If you only want to change the commit message, you can run `git commit --amend` without staging any new changes. This will open your default text editor to edit the commit message.
- **Add changes to the last commit**: If you want to add changes to the last commit, stage the changes first with `git add`, then run `git commit --amend`.

### Example
1. **Fixing a commit message**:
   ```bash
   git commit --amend
   # This opens the editor to change the commit message
   ```

2. **Adding a file to the last commit**:
   ```bash
   git add forgotten_file.txt
   git commit --amend
   # This adds forgotten_file.txt to the last commit
   ```

### Important Note
- **History Rewriting**: `git commit --amend` rewrites the commit history, so it's best used before pushing commits to a shared repository. If you've already pushed the commit, you'll need to force-push (`git push --force`), which can disrupt other collaborators.

Would you like to know more about any other Git commands or need help with something specific?


**Git Rebase** is a command used to integrate changes from one branch into another. It allows you to move or combine a sequence of commits to a new base commit. This can help create a cleaner, more linear project history.

### How Git Rebase Works
When you rebase, Git applies the changes from your current branch onto the tip of another branch. This effectively "replays" your commits on top of the target branch.

### Basic Usage
1. **Switch to the branch you want to rebase**:
   ```bash
   git checkout feature-branch
   ```

2. **Rebase onto the target branch**:
   ```bash
   git rebase main
   # This will apply the commits from feature-branch onto the tip of main
   ```

### Example
Let's say you have the following commit history:

```
A---B---C feature-branch
     /
D---E---F main
```

After running `git rebase main` on `feature-branch`, the history will look like this:

```
D---E---F---A'---B'---C' feature-branch
```

### Options
- **Interactive Rebase**: Use `git rebase -i <base>` to interactively edit, reorder, or squash commits.
  ```bash
  git rebase -i main
  # Opens an editor to modify the commit history interactively
  ```

- **Abort Rebase**: If you encounter conflicts or want to stop the rebase, use `git rebase --abort`.
  ```bash
  git rebase --abort
  ```

- **Continue Rebase**: After resolving conflicts, use `git rebase --continue` to proceed.
  ```bash
  git rebase --continue
  ```

### Important Notes
- **History Rewriting**: Rebasing rewrites commit history, so it's best used on local branches that haven't been pushed to a shared repository.
- **Force Push**: After rebasing, you'll need to force-push (`git push --force`) if the branch has already been pushed.

Would you like to explore more about interactive rebase or any other Git commands?






