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
