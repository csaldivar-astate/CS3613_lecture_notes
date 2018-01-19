<!-- .slide: data-background="assets/images/git-icon.svg" class="bg-box" -->
# Git
## Supplement

---

<!-- .slide: data-background="assets/images/git_logo_on_screen.png" class="bg-box" -->
## Resources

https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf

https://git-scm.com/docs

http://gitref.org/

https://www.digitalocean.com/community/tutorials/how-to-use-git-effectively

https://github.com/blog/2019-how-to-undo-almost-anything-with-git

(video) https://yow.eventer.com/yow-2014-1222/how-to-undo-almost-anything-with-git-by-peter-bell-1688

---

## Initial Setup

Before using git, you should set up your name and email address, as well as choosing your default editor for commit messages:
```bash
git config --global user.name "Your Name"
git config --global user.email  your.email@smail.astate.edu
git config --global core.editor vim
```
(Of course you can choose whatever editor you like; `vim` shown as a suggestion.)

To create a new repository, make sure you are in the top-level directory of your project and run:
```bash
git init
```

---

## Stage and Commit

Git requires that you _stage_ changes that you make in your working copy (choosing the ones you want to keep), then _commit_ those staged changes to make them part of the permanent record.

**`git add`**: Adds new files or stages changes to a particular file, files, or directory.

**`git commit`**: Commit your changes into the current local repository.  If you use the `-a` option, all changed files will be automatically staged prior to the commit (saves you a step).  Use `-m` to supply the commit message directly (otherwise an editor is opened for you).

---

## Integration with Phabricator

For the CS Phabricator server (phab.cs.astate.edu):

1. Set up a VCS Password in Phabricator.
    * Click Account Settings (the "wrench" in upper-right) then VCS Password under "Authentication".
2. Create your repository in Phabricator - Diffusion.
3. Get a copy of the phabricator site's SSL certificate (you can save it from your browser's security dialog).
4. Upload the certificate to the machine you are working on (i.e. Koding).
5. Tell git about the certificate: <small style="font-size: 100%; min-width:34em;">
```bash
git config --global http."https://phab.cs.astate.edu".sslCAInfo /PATH/TO/CERT/FILE
```
</small>

---

## Clone, Push, Pull, Fetch

**`git clone`** : Used to clone a repository; this is great to start working on a different machine.

**`git push`** : Used to _push_ local changes back to a remote repository (you must _commit_ all local changes first).

**`git pull`** : Used to _pull_ remote changes back into your local machine (bringing you up to date with changes made elsewhere).

**`git fetch`** : Gets remote changes without also merging them into your local working copy -- useful (safer) if you aren't sure what changes have been made remotely.

---

## Deploy to Website Automatically

https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps

http://toroid.org/git-website-howto

---

## Git Clients

https://git-scm.com/download/gui/linux

I recommend _SourceTree_ on Windows and Mac.  There isn't a really comparable tool on Linux for free, but _gitg_ is worth looking at; _SmartGit_ is pretty close, but has some license restrictions.