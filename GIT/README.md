# GIT

## Install Git
```
sudo apt update
sudo apt install git
git --version
```


## Demo

### munna wants to create code on his local 

```sql
mkdir git-demo # create directory

cd demo # enter the dir

git init # initializing git repo

ls -al # check .git directory (history will store in this directory)

touch test.txt # create one file

git status # you can see untracked files

git add test.txt # put file in staging area

git status # file is tracked now

git commit -m "added test.txt file" # save in git history (-m statnds for provide a msg)

git status # nothing to commit

vi test.txt # add something

git status # fils is modified

git add . # added to stage

git restore --staged test.txt  # remove from stage without commeting it

git add . \
git commit -m "added lines in test.txt" # again add and commit the file

git status # check insertations and output

git log # check the history

rm -rf test.txt  # delete the file and again do git add and commit

git log # you can see delete history is there but you want to clean from history

git reset <##########################> # use hash values .... whatever commit you copied it will delete above ones

git log # now you can see that comment which you want to keep

git status # now delete history is in unstage area

# create some more files and add them to stage area.... now you dont want this files in stage area and you dont want to loose this changes. but later you will need this files 
git stash

# use git status and log command to see everything is back to previous step

# now you want bring back those files which you stash

git stash pop # files will back in stage area again

git stash clear # if you dont want those files 

```

### munna Want to share his project to others ?

```sql
create a repo on github
attached newly created repo to your project ---> git remote add origin <repo url> i.e local and repo is connected with each other 
how many urls attached to your project -----> git remote -v
push the changes in repo  ----->  git push origin master
```

### munna will use Branching Strategy

- munna can not push code directly on main/master branch
- coz code is not finalized yet
- along with munna there are some other developers as well whoes are going to contribute to this project

```sql
git branch feature # create new branch feature
git checkout feature # change branch to feature
git merge feature # now code is finalized so we can merged into main/master so that other people can use the same

