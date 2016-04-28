# git tutorial

## Documentation

* [Start here](http://git-scm.com/documentation)
* [Try git](http://try.github.com/)
* [Git reference](http://gitref.org/)
* [Cheatsheet](http://ndpsoftware.com/git-cheatsheet.html)
* [Pro Git book](http://progit.org/book/)
* [Everyday git](http://schacon.github.com/git/everyday.html)
* [Git for svn users](http://git-scm.com/course/svn.html)
* [Git magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/)
* [Subversion re-education (I know it is mercurial, but still nice to read the comparison)](http://hginit.com/00.html)
* [branching by gitguys]  (http://www.gitguys.com/topics/tracking-branches-and-remote-tracking-branches/)
* [nice page on git svn]  (http://trac.parrot.org/parrot/wiki/git-svn-tutorial)
* [another git svn page]  (http://git-scm.com/book/en/Git-and-Other-Systems-Git-and-Subversion)
* [Git wiki]              (https://git.wiki.kernel.org/index.php/Installation)
* [Git real game]         (http://gitreal.codeschool.com/levels/1)
* [Learn git branching]   (http://pcottle.github.io/learnGitBranching/)
* [Detached head]         (http://gitolite.com/detached-head.html)

## Semantic versioning must read

 * [http://semver.org/]
 * [http://nvie.com/posts/a-successful-git-branching-model/]

## Installation

[See help@github](https://help.github.com/articles/set-up-git)

## To start a project

	mkdir snippets
	cd snippets
	git init
	touch README
	git add README
	git commit -m 'first commit'
	git remote add origin git@github.com:gkazior/snippets.git
	git push -u origin master

## git config on startup

	git config --global user.email "gkazior@interia.pl"
	git config --global user.name "gkazior"
   	git config --global core.autocrlf false
	git config --global branch.autosetuprebase always
	git config --global push.default simple	

	git config --global --list

## git config

    # after http://stevenharman.net/git-pull-with-automatic-rebase
    git config branch.autosetuprebase always
    # in .gitconfig it is
    [branch]
      autosetuprebase = always

## Crlf: Which is better MS or UNIX?
By default git will replace EOL according to current env. To disable it call the following:

	git config core.autocrlf false

[more info here](http://stackoverflow.com/questions/1967370/git-replacing-lf-with-crlf)

## Git is fast: init, checkout, branch

	time git init
	Initialized empty Git repository in /big/home/kazior/DPS-dev/.git/
	real    0m0.003s
	user    0m0.001s
	sys     0m0.001s

	time git add *
	real    0m14.977s
	user    0m14.168s
	sys     0m0.671s

	time git commit -m  "initial commit from dev-12370"
	[...]
	real    0m0.433s
	user    0m0.276s
	sys     0m0.081s

	time git branch "dev/branches/TYTVI-12123_sqliteInOm"
	real    0m0.002s
	user    0m0.001s
	sys     0m0.001s


## ignored files .depend

Create a .gitignore file with content:

	cat .gitignore
	.depend

then commit the file.

## Undo last commit

Suppose the last commit was x.c

	# The following sequence changes nothing
	git reset --soft HEAD^
	git commit -m "nothing has changed"

	# The following sequence changes nothing
	git reset HEAD^
	git add x.c
	git commit -m "nothing has changed"


## Header is evil (not in git only)

	diff --git a/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp b/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp
	index 3aa4ba8..43ef7f2 100644
	--- a/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp
	+++ b/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp
	@@ -1,5 +1,5 @@
	-/* $Header:: /Tytan60/TSrc/DPS/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp 14 1.0.14 14.09.10 13:56 KJACEK                                      $ */
	-#define MHDR  "$Header:: /Tytan60/TSrc/DPS/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp 14 1.0.14 14.09.10 13:56 KJACEK                                      $"
	+/* $Header:: /Tytan60/TSrc-7.0/DPS/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp 14 1.0.14 14.09.10 13:56 KJACEK                                  $ */
	+#define MHDR  "$Header:: /Tytan60/TSrc-7.0/DPS/SRC/TOOLS/UPDATEFDB/UpdateFDB.cpp 14 1.0.14 14.09.10 13:56 KJACEK                                  $"
 	#define MREV  "$Revision:: 14     $"
 	#define MNAME "UPDATEFDB"
 	#define USE_FUNCTION_INSTEAD_OF_GLOBAL_VARIABLES /* with static compilation global variables from other units doesn't work in exec files */

To fix the evil:

	find -name '*.c*' -print -exec sed -i.bak 's/\/Tytan60\/TSrc\-7\.0\/DPS\/SRC\//\/Tytan60\/TSrc\/DPS\/SRC\//g' {} \;

However you may get again:

	--- a/SRC/PLUGINS/COMMON/CMPDAT/cmpdat.c
	+++ b/SRC/PLUGINS/COMMON/CMPDAT/cmpdat.c
	@@ -1,4 +1,4 @@
	-/*$Header:: /Tytan60/TSrc/DPS/SRC/PLUGINS/COMMON/CMPDAT/cmpdat.c 8 1.0.8 09.06.08 16:00 JASTRZEB                        $*/
	+/*$Header:: /Tytan60/TSrc/DPS/SRC/PLUGINS/COMMON/CMPDAT/cmpdat.c 8 1.0.8 09.06.08 16:00 JASTRZEB                            $*/
	#define MREV  "$Revision:: 8        $"
	#include "cmpdat.hxx"

Or a lot of changes to compare and merge.

## More commands

	git log --pretty=format:'%h : %s' --topo-order --graph
	git reset --hard HEAD
	git log --stat
	git log --pretty=oneline
	git log --pretty=format:'%h : %s' --graph
	git tag stable-1 1b2e1d63ff
	   # shows details about tags
 	git log --tags --show-notes --simplify-by-decoration --pretty="format:%ai %d %s"
 	   # shows list of branches with details
 	git branch -avv

## git diff

	git diff branch1 branch2 -- ./conf/application.conf
	git diff branch1:file1 branch2:file2
	git diff HEAD^ HEAD

## To make a change log

	git log --pretty=format:'%s' --graph         >> CHANGELOG.md
	git log --pretty=format:'%s' --graph |  uniq >> CHANGELOG.md

## Tagging

	git tag -l "v1.1*" # list of tags
	git tag -a v1.4 -m 'version 1.4 release'

## To see the date wise tag history

	git log --tags --simplify-by-decoration --pretty="format:%ai %d"
	git log --date-order --graph --tags --simplify-by-decoration --pretty=format:'%ai %h %d'
	git log --decorate=full --all --pretty=format:'%h %d %s %cr %ae' --abbrev-commit|grep 'refs/tags'

## To search through whole history (sources)

        git grep -e <theRegexpToMatchByGrep> $(git rev-list --all)
        git grep -e <theRegexpToMatchByGrep> $(git rev-list <revFrom>..<revTo>)
        git grep -e <theRegexpToMatchByGrep> [--or] -e <theRegexpToMatchByGrep2>
        [See here] (http://stackoverflow.com/questions/2928584/how-to-grep-search-committed-code-in-the-git-history)

## To search through commit messages

        git log -G <theRegexpToMatchByGrep>


## Interactive rebase

        git branch feature1    # work in branch
        git checkout master    # back to master
        git merge feature1     # merge changes
        git rebase -i HEAD~4   # possibly remove commits in the middle
        git branch -d feature1 # remove the branch when you do not need it

## Merge into one commit

        # after https://makandracards.com/makandra/527-squash-several-git-commits-into-a-single-commit
        # Switch to the master branch and make sure you are up to date.
        git checkout master
        git fetch # this may be necessary (depending on your git config) to receive updates on origin/master
        git pull

        # Merge the feature branch into the master branch.
        git merge feature_branch

        # Reset the master branch to origin's state.
        git reset origin/master

        # Git now considers all changes as unstaged changes.
        # We can add these changes as one commit.
        # Adding . will also add untracked files.
        git add --all
        git commit

       # or simply
       git checkout master
       git merge --squash branch -m "super commit"

## Refactoring

        git branch -m old_name new_name    # rename a branch

## Check status of branches - if update is needed

	git remote -v update

## Revert

	git revert HEAD
	git revert HEAD^

## scripting with git - get some interesting values

	git rev-parse HEAD                 # print the current hash (long)
	last_commit=$(git rev-parse HEAD)  # the same - set the variable

	git rev-parse --short=8 HEAD       # print the current hash (only 8 chars)
	git symbolic-ref -q --short HEAD   # print the current branch name

	git rev-parse HEAD~2               # print the hash of two commits back
	git reset --hard HEAD~2            # reset - go back two commits back

## to work with fork

        fork a repo ex. https://github.com/katsuyan/speak.js
        clone it
        add remote for pulls
        git remote add katsuyan https://github.com/katsuyan/speak.js

        git push origin master
        # Pushes commits to your remote repo stored on GitHub

        git push --tags
        # Pushes tags created by me

        git fetch upstream
        # Fetches any new changes from the original repo

        git merge upstream/master
        # Merges any changes fetched into your working files

## to work with feature branch

	git checkout master                # checkout the base version
	git branch -b TICKET-123_TheName   # create a branch and checkout
	# do the work, test, and finally
	git push origin TICKET-123_TheName # push the feature branch to perform continues integration

## push multiple branches at once

	# pushes all branches and updates tracking information
	git push --all origin -u

## clone svn repo

To checkout the last version (do not have history, commits, etc)

	git svn init https://pckazior:8443/svn/sandbox/tu-prolog/trunk

To migrate the repository this might be useful.

	git svn clone http://svn.foo.org/project -T trunk -b branches -t tags
	git svn clone http://svn.foo.org/project/trunk
	git svn clone --stdlayout https://pckazior:8443/svn/sandbox/joratest

See also the https://github.com/nirvdrum/svn2git

## To patch

Prepare a patch

	git format-patch -1

Apply it:

	git am 0001-manual-backport-of-dev-changes.patch

or apply with standard patch command:

	patch -b  -p1 < 0001-manual-backport-of-dev-changes.patch

## git grep


        git grep  'Tenant'  branchName --  '*.conf'
        git rev-list --all | (while read rev; do git grep -e <regexp> $rev; done)
        git branch --list | grep '7.1.9' | (while read rev; do git grep 'Tenant' $rev -- '*.conf'; done)
        git rev-list --grep='7.1.9.*' --branches | (while read rev; do git grep 'Tenant' $rev -- '*.conf'; done)
        git log --author=kazior --since=1.month

        [See also] (http://travisjeffery.com/b/2012/02/search-a-git-repo-like-a-ninja/)

## empty folders

Git cannot keep empty folders, if you still want to keep the folders, put the .gitkeep empty file into the folder.

	touch .gitkeep

## Other stuff

	To verify the connectivity and validity of the objects in the database
	git fsck


