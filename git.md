# Git

#### How to rebase?
* [via GitLens](https://www.youtube.com/watch?v=P5p71fguFNI)

```bash
// on your branch
git rebase -i HEAD~number_of_commits
git push origin your_branch_name --force-with-lease
```

```bash
// all commits, e.g. on master
git rebase -i --root
git push origin master --force-with-lease`
```

#### How to commit?

- build: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
- ci: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
- docs: Documentation only changes
- feat: A new feature
- fix: A bug fix
- perf: A code change that improves performance
- refactor: A code change that neither fixes a bug nor adds a feature
- style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
- test: Adding missing tests or correcting existing tests
