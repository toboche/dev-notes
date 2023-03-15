* Version Control Systems maintain snapshots and some metadata about them.
* trees are composed of trees of blobs (i.e. files) and folders.
* Git uses directed acyclic graph to model history:
    * every state points to its previous version in the history
    * every state contains some metadata (e.g. author, message,...)

Data structure:

    type blob = array<byte>
    type tree map<string, tree|blob>
    type commit = struct{
      parents: array<commit>
      author: String
      message: String
      snapshot: tree
    }

    type object = blob | tree | commit

    objects = map<String, object>

    def store(o):
      id = sha(o)
      objects[id] = o

    def load(id):
      return objects[id]

In practice, in many places instead of storing a value, pointers are stored. Ids are used to identify points in history.
As seen above, Git maintains objects. But it also references:

    refernces = map<string, string>
    // e.f "fix-encoding-bug" is mapped to a 40-char-long id

The entire history graph is immutable. But references are mutable.
(skipping a lot, as I'm using it every day)

* `git init` - inits a repo
* `git help <command>`
* `git status`
* `git commit`
* `git log`
* `git cat-file -p <hasz of an object>`  - more internal command to see what's behind a given id. This can be used to
  traverse the entire object's tree
* `git log --all --graph --decorate` - nicer log, shown as a tree
* `git checkout <sha|branch>`
* `git diff <hash> <optional second hash> <filename>` - <hash> by default is HEAD
* `git branch -vv` - list
* `git branch <branchname>` - create branch
* `git checkout <branchname>` - switch to a branch
* `git checkout -b <branchname>` - create a branch and switch to it
* `git merge <branch name(x)>` - merge to current branch
* `git merge --abort`
* `git mergetool`
* `git merge --continue` - once the conflicts are resolved
* `git remote <name> <url>`
* `git push <name of remote> <local branch>:<remote branch>`, when the upstream is set: `git push`
* `git clone <remote> <directory>`
* `git fetch <remote, not needed if one>`
* `git pull` == git fetch; git merge
* `git clone --shallow` - no version history, but downloads only the latest version
* `git add -p <filename>` - interactive way of committing changes, it walks you through pieces of changes and asks if
  you want to keep them
* `git blame`
* `git show <sha>` - get all the info about a commit
* `git stash`/`git stash pop`
* `git bisect` - can take a script to automate the checks
* 
* 