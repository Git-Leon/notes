# Git Collaboration strategy

### Part 1, Creating The Team Branch
0. `cd ~/dev`
1. `git clone https://github.com/GitUser/NameOfProject.git`
2. `cd NameOfProject`
3. `git checkout -b nameofteam`
4. `git add .`
5. `git commit -m 'first commit'`
6. `git push -u origin nameofteam`


### Part 2, Creating a Feature Branch
1. `git fetch origin`
2. `git checkout nameofteam`
3. `git checkout -b nameofteam-feat-nameoffeature`


### Part 3, Synching a Feature Branch With Team Branch
0. `git fetch origin`
1. `git checkout nameofteam-feat-nameoffeature`
2. `git pull origin nameofteam`
3. `git add .`
4. `git commit -m 'feature branch synched with team branch'`
5. `git push -u nameofteam-feat-nameoffeature`


### Part 4, Merging a Feature Branch into Team Branch
1. `git fetch origin`
4. `git checkout nameofteam`
5. `git merge nameofteam-feat-nameoffeature`
6. `git add .`
7. `git commit -m 'merged nameoffeature into nameofteam'`
8. `git push -u origin nameofteam`
