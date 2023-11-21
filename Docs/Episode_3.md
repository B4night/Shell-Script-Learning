# git commands

`add, commit, pull, push`



branch: master branth and feature branch

```
C1 --- C2 ---  C3  ----- C4 --- C5		THIS IS MASTER BTANCH
		\				/
		 \			   /
		  \C'1 --- C'2/		THIS IS FEATURE BRANCH
```

## git branch

show branch name

## git checkout

switch branch

## git checkout -b \<branch name>

switch branch. If the branch does't exist, creat it.

## git diff \<branch name>

show the difference bewteen this branch and \<branch name>



# git workflow (collaborate on a large repo)

1. fork from the repo
2. now we have `master` branch
3. creat a new branch `feature`
4. edit and commit on the `feature` branch
5. create merge request

