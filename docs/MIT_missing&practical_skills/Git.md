# Version Control(Git)
## Git's data model
Git has a well-thought-out model that enables all the nice features of version control, like maintaining history, supporting branches, and enabling collaboration.  
### Snapshots
Git models the history of a collection of files and folders within some top level directoty as a series of snapshots. In Git terminology, a file is called a "blob" and it's just a bunch of bytes. A directory is called a "tree", and it maps names to blobs or trees(so directories can contain other directories). A snapshot is the top-level tree that is being tracked.
### Modeling history: relating snapshots
In Git, a history is a directed acyclic graph (DAG) of snapshots. That may sound like a fancy math word, but don’t be intimidated. All this means is that each snapshot in Git refers to a set of “parents”, the snapshots that preceded it. It’s a set of parents rather than a single parent (as would be the case in a linear history) because a snapshot might descend from multiple parents, for example, due to combining (merging) two parallel branches of development.Git calls these snapshots “commit”s.   
Commits in Git are immutable. This doesn’t mean that mistakes can’t be corrected, however; it’s just that “edits” to the commit history are actually creating entirely new commits, and references (see below) are updated to point to the new ones.
### Data model, as pseudocode

```
// a file is a bunch of bytes
type blob = array<byte>

// a directory contains named files and directories
type tree = map<string, tree | blob>

// a commit has parents, metadata, and the top-level tree
type commit = struct {
    parents: array<commit>
    author: string
    message: string
    snapshot: tree
}
```
### Objects and content-addressing
An “object” is a blob, tree, or commit: `type object = blob | tree | commit`.  In Git data store, all objects are content-addressed by their [SHA-1 hash](https://zh.wikipedia.org/wiki/SHA-1).  
```
objects = map<string, object>

def store(object):
    id = sha1(object)
    objects[id] = object

def load(id):
    return objects[id]
```
Blobs, trees, and commits are unified in this way: they are all objects. When they reference other objects, they don’t actually contain them in their on-disk representation, but have a reference to them by their hash.  
For example, the tree for the example directory structure above (visualized using git cat-file -p 698281bc680d1995c5f4caaf3359721a5a58d48d), looks like this:
```
100644 blob 4448adbf7ecd394f42ae135bbeed9676e894af85    baz.txt
040000 tree c68d233a33c5c06e0340e4c224f0afca87c8ce87    foo
```
The tree itself contains pointers to its contents, `baz.txt` (a blob) and foo (a tree). If we look at the contents addressed by the hash corresponding to `baz.txt` with `git cat-file -p 4448adbf7ecd394f42ae135bbeed9676e894af85`, we get the following:`git is wonderful`  
### References
Now, all snapshots can be identified by their SHA-1 hashes. That’s inconvenient, because humans aren’t good at remembering strings of 40 hexadecimal characters.  
Git’s solution to this problem is human-readable names for SHA-1 hashes, called “references”. References are pointers to commits. Unlike objects, which are immutable, references are mutable (can be updated to point to a new commit). For example, the **master** reference usually points to the latest commit in the main branch of development.
```
references = map<string, string>

def update_reference(name, id):
    references[name] = id

def read_reference(name):
    return references[name]

def load_reference(name_or_id):
    if name_or_id in references:
        return load(references[name_or_id])
    else:
        return load(name_or_id)
```
With this, Git can use human-readable names like “master” to refer to a particular snapshot in the history, instead of a long hexadecimal string.  
One detail is that we often want a notion of ***“where we currently are”*** in the history, so that when we take a new snapshot, we know what it is relative to (how we set the parents field of the commit). In Git, that “where we currently are” is a special reference called ***“HEAD”***.  
### Repositories
Finally, we can define what(roughly) is a Git repository: it is the data `objects` and `references`.  
on disk, all Git stores are objects and references: that's all there is to Git's data model. All `git` commands map to some manipulation of the commit DAG by adding objects and adding/updating references.  
Whenever you’re typing in any command, think about what manipulation the command is making to the underlying graph data structure. Conversely, if you’re trying to make a particular kind of change to the commit DAG, e.g. “discard uncommitted changes and make the ‘master’ ref point to commit 5d83f9e”, there’s probably a command to do it (e.g. in this case, git checkout master; git reset --hard 5d83f9e).
## Git command-line interface
### Basics
* `git help <command>`: get help for a git command
* `git init`: creates a new git repo, with data stored in the `.git` directory
* `git status`: tells you what's going on 
* `git add <filename>: adds files to staging area
* `git commit`: create a new commit
    * Write [good commit messages!](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
    * Even more reasons to write [good commit message](https://cbea.ms/git-commit/)
* `git log`: shows a fattened log of history
* `git log --all --graph --decorate`: visualizes history as a DAG
* `git diff <filename>`: show changes you made relative to the staging area
* `git diff <revision> <filename>`: shows differences in a file between snapshots
* `git checkout <revision>`: updates HEAD and current branch to the revision

### Branching and merging
* `git branch`: shows branches
* `git branch <name>: creates a branch
* `git checkout -b <name>: creates a branch and switches to it
    * same as `git branch <name>`;`git checkout <name>`

* `git merge <revision>`: merges into current branch
* `git mergetool`: use a fancy tool to help resolve merge conflicts
* `git rebase`: rebase set of patches onto a new base

### Remotes
* `git remote`: list remotes
* `git remote add <name> <url>`:add a remote
* `git push <remote> <local branch>:<remote branch>`:send objects to remote, and update remote reference
* `git branch --set-upstream-to=<remote>/<remote branch>`: set up correspondence between local and remote branch
* `git fetch`: retrieve objects/references from a remote
* `git pull`: same as `git fetch`;`git merge`
* `git clone`: download repository from remote

### Undo
* `git commit --amend`:edit a commit's contents/message
* `git reset HEAD <file>`: unstage a file
* `git checkout --<file>`: discard changes

### Advanced Git
* `git config`: Git is highly [customizable](https://git-scm.com/docs/git-config)
* ` git clone --depth=1`: shallow clone, without entire version history
* `git add -p`: interactive staging
* `git rebase -i`: interactive rebasing
* `git blame`: show who last edited which line
* `git stash`: temporarily remove modifications to working directory
* `git bisect`: binary search history(e.g. for regression)
* `.gitignore`: [specify](https://git-scm.com/docs/gitignore) intentionally untracked files to ignore
  
*** 

## Git Pro
[Git branching-basic branching and merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)  
[Git branching-remote branches](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)  
[Git branching-rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)
***