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

## Very fast, init, checkout, branch


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
