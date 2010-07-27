# Cheatsheet

## Setup
Open your `~/.gitconfig` file and add the following:

    [github]
    	user = <your-github-username>
    	token = <your-github-api-token>
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

### GUI's
- [SmartGit](http://www.syntevo.com/smartgit/index.html): Commercial, All Platforms
- [GitX](http://github.com/downloads/brotherbard/gitx/GitX%207-5-2010.zip): OSX only
- [gitg](http://github.com/jessevdk/gitg): GNOME/gtk+ clone of GitX
- [git-cola](http://cola.tuxfamily.org/): Really powerful, Linux only
- [qgit](http://digilander.libero.it/mcostalba/): QT based, All Platforms
- [TortoiseGit](http://code.google.com/p/tortoisegit/) Just like TortoiseSVN, Windows
- [StupidGit](http://wiki.github.com/gyim/stupidgit/) Really strong submodule support, All Platforms


## Synchronize View
- `git fetch && gitk --all &`
- `git fetch && gitx`
- SmartGit: `git fetch` then `Query -> Log` from the file menu

## Bash Aliases
Copy and paste the below into your shell.

    cd ~/ && git clone git://gist.github.com/114160.git .githelper && echo "# Add me to your .profile or .bash_profile.  Save the file, open a new terminal, and you'll have all of this." && echo "" && echo "source ~/.githelper/gistfile1.sh"

## Resources
- [cheat git](http://cheat.errtheblog.com/s/git)
- [Zack Rusin](www.cheat-sheets.org/saved-copy/git-cheat-sheet.pdf)
- [Jan Krüger](http://jan-krueger.net/development/git-cheat-sheet-extended-edition)
- [Windows 7 Gadget](http://github.com/Tigraine/git-cheatsheet-gadget)

[There are millions of these](http://www.google.com/search?q=git+cheatsheet).  Find the style that fits your workflow best.  Most are very good, except those that mention nothing about fetch and rebase.
