# Git Collaboration strategy

### Part 1, Creating The Team Branch
0. `cd ~/dev`
1. `git clone https://github.com/GitUser/NameOfProject.git`
2. `cd NameOfProject`
3. `git checkout -b teambranch`
4. `git add .`
5. `git commit -m 'first commit'`
6. `git push -u origin teambranch`


### Part 2, Creating a Feature Branch
1. `git fetch origin`
2. `git checkout teambranch`
3. `git checkout -b featurebranch`


### Part 3, Synching a Feature Branch With Team Branch
0. `git fetch origin`
1. `git checkout featurebranch`
2. `git pull origin teambranch`
3. `git add .`
4. `git commit -m 'feature branch synched with team branch'`
5. `git push -u featurebranch`


### Part 4, Merging a Feature Branch into Team Branch
1. `git fetch origin`
4. `git checkout teambranch`
5. `git merge featurebranch`
6. `git add .`
7. `git commit -m 'merged featurebranch into teambranch'`
8. `git push -u origin teambranch`
