Git Deploy
==========

Simple script for deploying a project from git's post-receive hook.

This post-receive hook allows developers to define a list of targets on the
server and then to be able to deploy to a specific target by adding a
[deploy-target] tag to the commit message that they want to deploy.

Requirements
------------

Currently git-deploy requires that you have your deploy targets on the same
file system that you are pushing your git commits to.

Installation
------------

These instructions assume that your targets are located at /var/www/beta-target
and /var/www/live-target and your git is located in your home at
~/gitrepo. It also assumes that you have created the /var/www/live-target and
/var/www/beta-target by simply cloning your ~/gitrepo directly.

Clone this project onto your server with

```shell
cd ~ && git clone https://github.com/ryakad/git-deploy
cd git-deploy
```

Copy the deploy script into your hooks folder.

> If you already have a post-receive hook in place you will want to either
> call this script from your existing hook or vise versa.

```shell
cp post-receive ~/gitrepo/hooks/post-receive
cd ~/gitrepo/hooks
chmod a+x post-receive
```

Now you need to add your targets to the file in the hooks dir.

```python
targets = {
    "live": "/var/www/live-target",
    "beta": "/var/www/beta-target"
}
```

Usage
-----

With everything in place running a deploy is as simple as adding [deploy-target]
anywhere in a commit message and pushing it to the server.

With the above configuration you would use [deploy-live] and [deploy-beta]
to update the respective target.
