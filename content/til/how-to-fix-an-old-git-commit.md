---
title: "How to Fix an Old Git Commit"
date: 2020-08-10T08:03:11+02:00
tags:
- git
---

... which you do not have pushed to a remote repository.

```bash
git add <my fixed files>
git commit --fixup=OLDCOMMIT
git rebase --interactive --autosquash OLDCOMMIT^
```

via https://twitter.com/nnja/status/796876898005417984?s=03
via https://stackoverflow.com/questions/2719579/how-to-add-a-changed-file-to-an-older-not-last-commit-in-git/27721031#27721031
