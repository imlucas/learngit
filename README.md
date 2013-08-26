# git cheatsheet

these are notes and tricks i've collected over the years when teaching
people to use git for the first time or making them more productive.
git is a pretty serious tool that can make your day-to-day process
really smooth and simple if you know how to bend it in a few ways.

## setup

Open your `~/.gitconfig` file and add the following

    [github]
    	user = <your-github-username>
    [user]
    	name = <your-full-name>
    	email = <your-email-address>

    [color]
        ui = auto

    [color "branch"]
        current = yellow reverse
        local = yellow
        remote = green

    [color "diff"]
        meta = yellow bold
        frag = magenta bold
        old = red bold
        new = green bold
        whitespace = red reverse

    [color "status"]
        added = yellow
        changed = green
        untracked = cyan

    [core]
        whitespace=fix,-indent-with-non-tab,trailing-space,cr-at-eol

the settings above will give you a really nice start to using git effecitively.
git is extremely customizable.
you should definitely have a look of the
[config chapter in the git book](http://git-scm.com/book/en/Customizing-Git-Git-Configuration).

this is your global configuration file and will make sure you have sane
defaults everywhere.  i recommend setting your default's for name, username and
email to what you use when contributing to open source.  for work repos,
i recommend setting your information to be your work email either by editing
the `.git/config` to be

    [user]
        name = <your more official work name>
        email = <your work email address>

you can also just do that from the command line

    cd <my project dir>;
    git config <your more official work name>;
    git config <your work email address>;


in general, if you see a docs that say to use `git config --global` for something,
just don't.

## command line

copy and paste the below into your shell

    cd ~/;
    git clone git://gist.github.com/114160.git .githelper;
    echo "source ~/.githelper/gistfile1.sh" >> ~/.profile;
    source ~/.profile;

this will make your life better.  it adds several shortcuts to simplify the process as well as adding extra arguments to your
commands to remove some of the most common gotchas.  this script
will also add the current repo and branch to your command line
prompt.

 * `freebase`, `f`: fetch and rebase the current branch `== git pull --rebase`
 * `commit`, `c`: create a new commit of all changes files `== git commit -a`
 * `push`, `p`: push local commits to the remote repository `== git push origin <current_branch_name>`
 * `status`, `s`: `== git status`
 * `newbranch <name>`: create a new branch from current `== git pull --rebase && git checkout -t origin/<name>`
 * `deletebranch <name>`: delete a branch locallay.  don't worry, it will prompt you before actually deleting `== git branch -d <name>`

## gui's

### recommended

 * mac
    * [GitX](https://github.com/downloads/brotherbard/gitx/GitX%20Nov-17-2010.zip)
    * [GitHub](http://mac.github.com/)
 * windows
    * [GitHub](http://windows.github.com/)
 * nix
    * [gitg](http://github.com/jessevdk/gitg) GNOME/gtk+ clone of GitX
    * [gitk](http://stackoverflow.com/questions/1570535/guide-to-understanding-gitk)

### others
- [git-cola](http://cola.tuxfamily.org/): Really powerful, Linux only
- [SmartGit](http://www.syntevo.com/smartgit/index.html): Commercial, All Platforms
- [qgit](http://digilander.libero.it/mcostalba/): QT based, All Platforms
- [TortoiseGit](http://code.google.com/p/tortoisegit/) Just like TortoiseSVN, Windows
- [StupidGit](http://wiki.github.com/gyim/stupidgit/) Really strong submodule support, All Platforms

### diff tools

there are too many of these to list. [meld](http://meld.sourceforge.net) is great for unix.  [Kkleidoscope](http://www.kaleidoscopeapp.com/) for mac.

## day-to-day workflow
 * `f` to get any changes
    * got conflicts?
         - `git rebase --abort && git pull;`
    * still have conflicts?
         * resolve them in each file
         * run `add <file-path>` for each file that was in conflict
         * `c` to commit the resolved conflict state
         * `p` to push the changes to the remote
    * no conflicts?
         * you win.
         * almost always the case when several people aren't making big changes to the same code
 * do work
 * `a <path>` to add new files
 * `c` to save state locally
 * `f` to make sure nothing has changed on the remote before we push
 * `p` to send your changes to the remote

### a note on freebase vs pull
`git pull` is  `git fetch` and then `git merge` to apply the changes from the
remote.  `freebase` is `git fetch` and then
`git rebase remotes/origin/<branch-name>`.
freebase will interleave your changes with any remote changes.
pull will use merge to combine your local changes and the remote changes.
it is highly preferable to use `freebase` over `pull` as it makes the history
much cleaner and easier to visualize, but you can always just use `pull`.

## merging

### integration

say we want to merge `featureA` branch into `master`:

    checkout master;
    f;
    checkout featureA;
    f;
    git merge master;
    # resolve any conflicts
    p;
    checkout master;
    git merge featureA;
    p;

@todo (lucas) add integrate `<feature_branch>` into `<branch>` alias

### resolving merge conflicts

github has [great documentation for dealing with merge conflicts](https://help.github.com/articles/resolving-a-merge-conflict-from-the-command-line)
but in general the workflow goes like this

 * files in conflict will be shown by `status` in red and listed as both modified
 * resolve the conflicts in each file
 * `add <file-path>` for each file that was in conflict
 * `c` to commit the resolved conflict state
 * `p` to push the changes to the remote.

## synchronize view

if you are used to using the synchronize view in eclipse a lot, here's a simple
way to get the same info from the command line

 * `git fetch && gitk --all &`
 * `git fetch && gitx`
 * SmartGit: `git fetch` then `Query -> Log` from the file menu

## resources
 * [github flow](http://scottchacon.com/2011/08/31/github-flow.html) walkthrough of github's process
 * [gitflow](http://nvie.com/posts/a-successful-git-branching-model/)
 * [cheat git](http://cheat.errtheblog.com/s/git)
 * [Zack Rusin](www.cheat-sheets.org/saved-copy/git-cheat-sheet.pdf)
 * [Jan Krüger](http://jan-krueger.net/development/git-cheat-sheet-extended-edition)
 * [Windows 7 Gadget](http://github.com/Tigraine/git-cheatsheet-gadget)

[there are millions of these](http://www.google.com/search?q=git+cheatsheet).
find the style that fits your workflow best.
most are very good, except those that mention nothing about fetch and rebase.
