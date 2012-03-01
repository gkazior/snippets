# git tutorial

##start a project

	mkdir snippets
	cd snippets
	git init
	touch README
	git add README
	git commit -m 'first commit'
	git remote add origin git@github.com:gkazior/snippets.git
	git push -u origin master

## crlf
use
	git config core.autocrlf false
[more info on](http://stackoverflow.com/questions/1967370/git-replacing-lf-with-crlf)

## Fast init, checkout, branch


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


## ignore .depend
Create a .gitignore file with content:
	cat .gitignore
	.depend

then commit the file.


## header is evil (not in git only)
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

## more commands
	git log --pretty=format:'%h : %s' --topo-order --graph
	git reset --hard HEAD
	git log --stat
	git log --pretty=oneline
	git log --pretty=format:'%h : %s' --graph
	git tag stable-1 1b2e1d63ff
	git revert HEAD
	git revert HEAD^

## patch
	git format-patch -1
	git am 0001-manual-backport-of-dev-changes.patch
	patch -b  -p1 < 0001-manual-backport-of-dev-changes.patch

## stashing

## gc

## git fsck


