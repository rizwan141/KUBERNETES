# GIT

## Install Git
```
sudo apt update
sudo apt install git
git --version
```


## Demo

### lets create code on local 

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

### Want to share your project to others ?

```sql
create a repo on github
attached newly created repo to your project ---> git remote add origin <repo url>
all urls attached to your project -----> git remote -v

