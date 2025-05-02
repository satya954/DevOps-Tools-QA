## ✅ Git, GitHub, GitLab

**Q: What is Git, GitHub, and GitLab? What are the differences?**  
A: Git is a distributed version control system used to track changes in source code. GitHub and GitLab are platforms that provide Git repository hosting with additional features like CI/CD, issue tracking, and access control. GitHub is known for its large open-source community, while GitLab offers a more integrated DevOps lifecycle tool, including built-in CI/CD and container registry. GitLab can be self-hosted; GitHub is typically used as a SaaS offering.

**Q: What is merge and rebase?**  
A: `Merge` integrates changes from one branch into another by creating a merge commit, preserving the commit history. `Rebase` moves or "re-applies" commits from one branch onto another, creating a linear history but potentially rewriting commit history, which can be problematic on shared branches.

**Q: How do you revert a commit in Git?**  
A: You can use `git revert <commit_hash>` to create a new commit that undoes the changes. Unlike `git reset`, it doesn’t change the history and is safe for shared branches.

**Q: Explain the difference between Git pull and Git fetch?**  
A: `git fetch` downloads changes from the remote repository but does not merge them. `git pull` fetches and automatically merges changes into your current branch.

**Q: Explain the branching strategies you have used.**  
A: I’ve used Git Flow (feature/develop/release/hotfix), trunk-based development (short-lived branches), and GitHub flow (main branch with feature branches and PRs). Choice depends on team size, release frequency, and CI/CD maturity.

**Q: How do you automate deployment rollbacks in ArgoCD?**  
A: ArgoCD maintains a history of previously deployed versions. Rollbacks can be automated by scripting a sync to a previous commit or revision using the ArgoCD CLI or UI. We can also set health checks and auto-sync policies to trigger rollbacks on health failures.

**Q: What is the purpose of `.gitkeep` and how is it different from `.gitignore`?**  
A: `.gitkeep` is a convention to track otherwise empty directories in Git (which doesn’t track empty folders). `.gitignore` tells Git to ignore certain files or patterns during commits.

**Q: How would you perform a force push safely in a shared repository?**  
A: Avoid if possible. If necessary, notify the team, ensure no one else is working on the branch, and use `git push --force-with-lease` instead of `--force` to prevent overwriting others' changes unintentionally.

**Q: What is git cherry-pick and what is its use?**  
A: `git cherry-pick <commit_hash>` applies the changes from a specific commit onto the current branch. Useful for hotfixes or applying selective changes without merging entire branches.

**Q: What is git hard reset and soft reset?**  
A: `git reset --soft` moves HEAD to a commit, keeping staged and working directory changes. `git reset --hard` moves HEAD and deletes all changes in the index and working directory, so use it with caution.

**Q: What conflicts have you faced in Git?**  
A: Merge conflicts in binary files, rebasing long-lived branches, and permission conflicts in protected branches. Resolved using tools like `git mergetool`, and by aligning with team policies.

**Q: Will `git pull` pull all branches or just a particular branch?**  
A: `git pull` only pulls changes for the current checked-out branch. Other branches need to be explicitly fetched or pulled.

**Q: What is git rebase?**  
A: `git rebase` is used to apply commits from one branch on top of another. It’s used to create a clean, linear history but can be dangerous if used improperly on shared branches due to history rewriting.

