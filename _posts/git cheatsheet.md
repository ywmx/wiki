  Git Cheatsheet  body { background-color: black; color:white; font-family: monospace; font-size: 18px; } [SpaceLegion.wiki](index.html)  

GIT CHEATSHEET

  
\# 1 Install git  
  
Debian/Ubuntu - _sudo apt install git_  
Arch - _sudo pacman -S git_  
Fedora22 - _sudo dnf -y install git_  
Gentoo - _emerge --ask --verbose dev-vcs/git_  
FreeBSD - _pkg install git_  
OpenBSD - _pkg_add git_  
Solaris 11 - _pkg install developer/versioning/git_  
NixOS - _nix-env -i git_  
openSUSE - _zypper install git_  
RHEL, CentOS - _yum install git_  
Solus - _sudo eopkg install git_  
  
Check git version using _git --version_  
  
  
\# 2 Create and git initialize a directory  
  
_mkdir sample_ (creating a folder)  
  
_cd sample_ (moving to the directory)  
  
_git init_ (git initialize the directory)  
  
  
\# 3 Configure git  
  
_git config --global user.name (username)_  
  
_git config --global user.email (user email)_  
  
  
\# 4 Create a file  
  
_touch sample.html_ (creating an html sample file)  
  
_touch sample.py_  
  
_touch main.js_  
  
_touch index.html_  
  
  
\# 5 Add a file  
  
_git add sample.html_  
  
  
\# 6 Add all file in the directory  
  
_git add ._ (Add all the files)  
  
  
  
  
_git add git -A_ (Add all new and changed files to the staging area)  
  
  
\# 7 Add all files which has the same extension  
  
_git add *.html_ (It wil add all the .html)  
  
  
\# 8 View current git status  
  
_git status_  
  
  
\# 9 Remove a file  
  
_git rm --cached index.html_ (removes index.html file)  
  
  
\# 10 Commit all files  
  
_git Commit_  
  
  
\# 11 Commit directly to master branch  
  
_git commit -m "your changelog"_  
  
  
\# 12 Create a branch  
  
_git branch sample_  
  
  
\# 13 Switch between branches  
  
_git checkout sample_  
  
  
\# 14 Merge branches  
  
_git merge sample_  
  
  
\# 15 Add remote url  
_git remote add origin (repo url)_  
  
  
\# 16 View repo  
  
_git remote_  
  
  
\# 17 Push all the files to git repository  
  
_git push -u origin master_  
  
  
\# 18 To pull a file  
  
_git pull (repo url)_  
  
  
\# 19 Remove all files from git repo  
  
_git rm -f *_  
  
  
\# 20 To clone any git repo  
  
_git clone_  
  
  

By [Sarosx](https://github.com/sarosx)