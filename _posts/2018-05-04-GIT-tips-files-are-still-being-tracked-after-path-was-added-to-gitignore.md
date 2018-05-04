---
layout: post
title: GIT tips - files are still being tracked after path was added to .gitignore
---


In case you are tracking a wrong folder / file, you have found that you don't have to track it anymore, you add it to .gitignore but git is still tracking it here are some steps to fix this:

**NOTE : First commit your current changes, or you will lose them.**

Then run the following commands from the top folder of your git repo:

```bash
git rm -r --cached .

git add .

git commit -m 'fixed untracked files'
```

Source: [https://stackoverflow.com/questions/11451535/gitignore-is-not-working](https://stackoverflow.com/questions/11451535/gitignore-is-not-working)
