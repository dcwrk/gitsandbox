# Playground for testing Git Flow

Highly recommended to install Microsoft's [Visual Studio Code](https://code.visualstudio.com). It is available for OSX, Linux and Windows.


- Create directory `mkdir sandbox`.
- Optionally add any file (README.md for example).
- Initialize the git repository `git init` 
- See log `git log`
- Add files to staging area `git add README.md`
- Commit staged area to repo `git commit -m "Added my first file"`
- See log again `git log`

This so far has version control enabled locally. Next step is to sync this to a remote repository.

- See current list of repostories to sync to/from. `git remote -v`
- Add github project `git remote add origin git@github.com:dcwrk/gitsandbox.git`



For production, only need to clone the 'dashboard' branch and install requirements as following: 

```console
    git clone --single-branch --branch dashboard --recursive <url> clide-sim-dashboard
    cd clide-sim-dashboard
    python3 -m pip install -r requirements.txt
```

For developement, make sure to set the hooksPath variable to use the .githooks directory.

    git clone --recursive <url> clide-sim-devel
    cd clide-sim-devel
    python3 -m pip install -r requirements.txt

    git config --local core.hooksPath .githooks/
    git config --global user.email "<email address>"
    git config --global user.name "<Name>"

    # Note that the only the git 'submodules' defined in the master branch will get 
    # recursively updated. To update a submodule located exclusively on another branch,
    # switch to that branch first and the update the module

    git checkout subtest
    cd subfolder
    git submodule update --init --recursive

    # To pull latest changes in branch, including submodules:
    git pull --recurse-submodules


#
# Git reference commands
#
#  for forward updates only to prevent divergence
#  see: https://blog.sffc.xyz/post/185195398930/why-you-should-use-git-pull-ff-only
git config --global pull.ff only

# Unset any of these if needed as following:
#    git config --global --unset diff.tool

# Use VSCODE as diff visual tool
git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --new-window --wait --diff $LOCAL $REMOTE'

git config --global difftool.prompt false

git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --new-window --wait --merge $REMOTE $LOCAL $BASE $MERGED'

# Alternatively, set all these in ~/.gitconfig
# cat ~/.gitconfig
#  [user]
#          email = <email addresS>
#          name = <name>
#  [remote "origin"]
#          prune = true
#  [init]
#          defaultBranch = master
#  [fetch]
#          prune = true
#  [pull]
#          ff = only
#  [diff]
#          tool = vscode
#  [difftool "vscode"]
#          cmd = code --new-window --wait --diff $LOCAL $REMOTE
#  [difftool]
#          prompt = false
#  [merge]
#          tool = vscode
#  [mergetool "vscode"]
#          cmd = code --new-window --wait --merge $REMOTE $LOCAL $BASE $MERGED



## merging
git checkout dashboard
git merge -m "Merging devel into main" david-devel

## tagging
git tag -a <tagname> HEAD -m "message"
git push <remote> --tags 
git tag --list -n99

## log
git log --oneline

## git submodules

# Link an external git repo to a folder as a submodule
git submodule add https://github.com/dbarnett/python-helloworld.git subtestdir

# a clone of that directory is automatically pulled
# Older versions of git may also require:
git submodule update --init --recursive
