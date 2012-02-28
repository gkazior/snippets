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

## timing for medium size project
very fast, init, checkout, branch