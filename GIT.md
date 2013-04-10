# git tutorial

## Documentation

* [Start here](http://git-scm.com/documentation)
* [Git reference](http://gitref.org/)
* [Pro Git book](http://progit.org/book/)
* [Everyday git](http://schacon.github.com/git/everyday.html)
* [Git for svn users](http://git-scm.com/course/svn.html)
* [Git magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/)
* [Subversion re-education (I know it is mercurial, but still nice to read the comparison)](http://hginit.com/00.html)
* [branching by gitguys] (http://www.gitguys.com/topics/tracking-branches-and-remote-tracking-branches/)

##To start a project

	mkdir snippets
	cd snippets
	git init
	touch README
	git add README
	git commit -m 'first commit'
	git remote add origin git@github.com:gkazior/snippets.git
	git push -u origin master

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

## To make a change log

	git log --pretty=format:'%s' --graph         >> CHANGELOG.md
	git log --pretty=format:'%s' --graph |  uniq >> CHANGELOG.md

## To search through whole history (sources)

        git grep -e <theRegexpToMatchByGrep> $(git rev-list --all)
        git grep -e <theRegexpToMatchByGrep> $(git rev-list <revFrom>..<revTo>)
        git grep -e <theRegexpToMatchByGrep> [--or] -e <theRegexpToMatchByGrep2>
        [See here] (http://stackoverflow.com/questions/2928584/how-to-grep-search-committed-code-in-the-git-history)

## To search through commit messages

        git log -G <theRegexpToMatchByGrep>

## Revert

	git revert HEAD
	git revert HEAD^


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

## Other stuff

	To verify the connectivity and validity of the objects in the database
	git fsck


