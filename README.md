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


