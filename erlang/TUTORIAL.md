# erlang 5 minutes tutorial

## Download an install

eclipse IDE: http://erlide.org/#installation
Update site: http://erlide.org/update

## Hello worldok

io:format("Hello world").

## first spawn

F = fun() -> 2 + 2 end.
spawn(F).
spawn(fun() -> io:format("~p~n",[2 + 2]) end).

G = fun(X) -> timer:sleep(10), io:format("~p~n", [X]) end.
[spawn(fun() -> G(X) end) || X <- lists:seq(1,10)].

## help and manuals

Getting started http://www.erlang.org/doc/getting_started/users_guide.html
Mnesia          http://www.erlang.org/doc/man/mnesia.html
documents       http://www.erlang.org/doc.html
Users guide     http://www.erlang.org/doc/apps/tools/users_guide.html
Tools           http://www.erlang.org/doc/apps/tools/index.html

## Books

Concurrent programming in erlang http://www.erlang.org/download/erlang-book-part1.pdf
