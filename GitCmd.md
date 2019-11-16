## Basic commands

1. Create a new repository on the command line

* ``echo "# xnotes" >> README.md``
* ``git init``
* ``git add README.md``
* ``git commit -m "first commit"``
* ``git remote add origin ``https://github.com/rollandxyz/xnotes.git``

2. Shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote
``
git remote -v
``

3. To add a new remote Git repository as a shortname you can reference easily
``
git remote add <shortname> <url>:
``

4. push an existing repository from the command line
* ``git remote add origin https://github.com/rollandxyz/xnotes.git``
* ``git push -u origin master ``

5. push your changes to remote master
``
git pull origin my_remote_branch
``
6. pull others' edits to remote master to local. it will automatically fetch and then merge that remote branch into your current branch
* ``git checkout my_local_branch ``
* `` git pull origin my_remote_branch ``

7. push any commits you’ve done back up to the server
``
git push origin master
``
This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime. If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You’ll have to fetch their work first and incorporate it into yours before you’ll be allowed to push.

8. pulls down all the data from that remote project that you don’t have yet. After you do this, you should have references to all the branches from that remote, which you can merge in or inspect at any time
``
git fetch <remote>
``
9. fetches any new work that has been pushed to that server since you cloned (or last fetched from)
``
git fetch origin
`` 

10. merging an upstream
https://help.github.com/articles/merging-an-upstream-repository-into-your-fork/



[A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)


https://github.com/Reactive-Extensions/Tx/blob/master/Doc/CONTRIBUTING.md


https://help.github.com/en/github/collaborating-with-issues-and-pull-requests



