Md Mainul Abrar

2.A
```bash
$ git branch test1
$ git branch test2
```

2.B and 2.C
```bash
$ git checkout test1
$ nano test.txt
```

2.D
```bash
$ add test.txt
$ commit --all
```

2.E
```bash
$ git checkout test2
```
No, I don't see the test.txt file in the hw/VCS directory as it has been committed to branch test1.

2.F
```bash
$ nano test.text
```

2.G
```bash
$ git checkout test1
error: The following untracked working tree files would be overwritten by checkout:
        hw/VCS/test.txt
Please move or remove them before you switch branches.
Aborting

$ git add .
$ git commit --all
$ git checkout test1
```

2.H
```bash
$ git checkout main
$ git merge test1
```
merge command given in main branch

2.I
The contents are readme.md and test.txt

2.J
```bash
$ git checkout test2
$ git checkout main
$ git merge test2
Auto-merging hw/VCS/test.txt
CONFLICT (add/add): Merge conflict in hw/VCS/test.txt
Automatic merge failed; fix conflicts and then commit the result.
```
The error rises as there is already a file called test.txt in main branch which has different content from that of test2 branch

2.K
```bash
$ git checkout test2
error: you need to resolve your current index first
hw/VCS/test.txt: needs merge
```

2.L
```bash
$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
The conflict exist because I have unmerged paths.

2.M
I edited the test.txt with nano

2.N
```bash
$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      test.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add .
$ git commit --all
$ git checkout test2
```

2.O
```bash
$ git branch -d test1
error: The branch 'test1' is not fully merged.
If you are sure you want to delete it, run 'git branch -D test1'.
```

2.P
```bash
$ git checkout main
$ git branch -d test1
Deleted branch test1 (was ee59d4f).
$ git branch
* main
  test2
```

2.Q
The difference is that the branch test1 is not fully merged with test2. So it gives a warning. But as it is merged with main I could delete it from main.

2.R
```bash
$ git checkout test2
$ git branch -d test2
error: Cannot delete branch 'test2' checked out at 'C:/Users/AbrarMdMainul/MM3/MMP23S'
```

2.S
```bash
$ git checkout main
$ git branch -d test2
$ git branch
* main
```

2.T
```bash
$ git add --all
$ git commit --all
$ git push --all
```




