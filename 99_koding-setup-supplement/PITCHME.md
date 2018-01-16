## Supplemental Material:
# Koding.com Setup

<!-- .slide: data-background="images/cloud_up_arrow.png" -->

---

## 1. Set up an account.

http://koding.com

Koding provides a Free Tier of account where you can (temporarily) operate one virtual machine instance (in Amazon's EC2 Cloud).  Your VM will be running a recent Ubuntu Linux.

You can fully customize your virtual machine.

Koding's web interface gives you an interactive terminal as well as a programmer's text editor.  It isn't the best, but it works.

---

## 2. Koding SSH Access

You will want to access your Koding VM via ssh.  You must set up public-key authentication to do so.

1. Create public key keypair<br />(see  https://help.github.com/articles/generating-ssh-keys/ )
2. Add the key to your local machine.
    * `ssh-add -k  your_key` if you are on Mac!
3. Add the key to Koding
    * Click up arrow next to your name.
    * Click "Account Settings"
    * Click SSH Keys - Add New Key.
    * Paste the text of your **public key** here.

---

## Apt Update

_Apt_ is a software package manager on some Linux platforms - Ubuntu is one of them.

To update your _list of available software_, do the following:

`sudo apt-get update`

Then, to actually perform updates, do this:

`sudo apt-get update`

The `sudo` part tells the OS that you need to perform this as `root` (the system Admin user).

---

## Install SQLite and PHP Adapter

Using Apt, you can install SQLite (a lightweight relational database management system (DBMS)):

`sudo apt-get install sqlite3`

And you will also want to install the adapter for SQLite into PHP:

`sudo apt-get install php5-sqlite`

After this operation, you should restart your virtual server<sup>*</sup>.

<small><sup>*</sup>(or, restart the apache2 server only)</small>

---

## Install Composer

Composer is a package manager specifically for PHP development.

`kpm install composer`  (only on Koding)

(Google for the install process if you are using a different server.)

---

## Git Repo on Koding

* Git is already installed.
* In order to do "push to update live app", follow steps here:
    - http://toroid.org/ams/git-website-howto
* Your apps should be in sub-direcotries of the _Applications_ directory.
* Use a symbolic link to link _Web_ to your _public_ directory.
    - Ex: `ln -fs ~/Applications/my_app/public ~/Web`
* Add the bare repo as a _Remote_ in your local Git repository.
* Push to the remote to push updates to the live site!


