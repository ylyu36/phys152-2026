# Repository for PHYS 152 (Physics and Machine Learning) at UCSC in Winter 2026

We will use the Git version control system to manage some of the course content, specifically lecture notebooks and homework assignments
You can viewing the notebooks directly on github, but you can't execute the cells, and not all of the graphics will render correctly.
To interact more fully with the content you can use JupyterLab locally or Google Colab remotely.
(Some people have had good experience with VS Code, too.)

For most people looking to access and run course content right away, Google Colab is the fastest approach, even if it takes a little bit of setup.

# Using Google Colab

You can access Google Colab here: (https://colab.research.google.com/).
Students have access to the Colab Pro version for free: (https://colab.research.google.com/signup).

Once there, click on "Github" on the left panel, and then put your github username in the top box.
Make sure "include private repos" is checked.
You may need to follow instructions to link your Colab account with your github account.
Once you do, you should be able to click on the box below "Repository" and see your fork of `phys152-2026`, and the available notebooks in the list at the bottom.

Work that you do in the Colab session will disappear the next time you open Colab unless you save it to your github repo.
Go to "File/Save" and make sure it says "Save in Github" at the top.
Enter an appropriate commit message and click "OK".
Note: after you do this, check your fork in github to see that the new content is there!
If not, of if there's a problem saving, then make sure to download  your content (assuming you want to keep it) so you don't lose your work.

# Using Jupyter

When using Jupyter, you'll first need to get the course content onto the filesystem of whatever computer you're using to run Jupyter.
The best way to do this is by using SSH keys to access your Jupyter fork.

## Generating SSH keys to work with github (for use in Jupyter servers or your laptop)

First, we'll generate ssh keys on our jupyter server.
(If you're using Colab, then you can open the notebooks directly from your Github repo!)
1. Sign in to the Jupyter server
2. Open a terminal
3. enter the command `ssh-keygen -t rsa`
4. press "enter" three times

Next, we'll get the public key we just generated and put it into Github:
1. from the Jupyter terminal, execute `cat ~/.ssh/id_rsa.pub`
2. copy the terminal output
3. now go to a Github browser tab.  Click on your avatar in gitlab, and select "Settings".
4. On the left sidebar, go to "SSH and GPG Keys"
5. Click on "New SSH key"
6. Paste the terminal output you copied before in the block that says "Key"
7. In the title, put whatever your hostname is, or whatever label you want to use for this server
8. Modify other settings as you like, then click "Add key" at the bottom-left.

## Creating your fork of the course repository

See HW0 for instruction on this.  

Once you've created your fork, you can get the files from that repository on Jupyter by running the following in a terminal (replace `<username>` with your own username, and if you called your fork something other than `phys152-2026` then you'll need to change that part of the string as well):

```
git clone git@github.com:<username>/phys152-2026.git
```

That will create a directory in your Jupyter area that has your fork.

### Getting changes from upstream

On the git web page for your fork, if you are missing updates from upstream then you should see a link called "Sync fork" to update your fork with the upstream changes.
You can follow that link to update from upstream.
You may see a message that says your fork is ahead of the upstream repository by some number of commits, but you should still be able to "Update branch" from upstream despite this warning.

However, that won't update your local cloned repository on your Jupyter server.
To do that, you will need to go into a terminal on the Jupyter server and run:

```
git pull
```

to get the changes from the server.
If you have changes that you've made to your own fork on your Jupyter server, then git may complain, in which case you should first clear the outputs from the Lecture notebooks and see if that helps.
If you have other changes even when the lecture notes changes are cleared, then commit them:

```
git add <file that changed>
git commit -m "some description of the changes"
```

and then try pulling again:

```
git pull
```

It's possible that at this point you'll see an error message like this:

```
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint: 
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

In that case, I'd recommend merging, rather than rebasing:

```
git config pull.rebase false
git pull
```

or, if you prefer to rebase this one time (reasonable people can disagree on the best approach here):

```
git pull --rebase
```

You should then see output like:

```
Successfully rebased and updated refs/heads/main.
```

### Commiting your changes
To commit your own code, e.g. if you want to commit an initial version of pset1:

```
git add Exercises/Homework-0.ipynb
git commit -m "adding some notes to problem set 0"
git push
```

The first command adds Homework-0 to the list of changes that git will track; the second command commits those changes to your local git database; the third command pushes all the queued changes in your local database to your repository on github.
