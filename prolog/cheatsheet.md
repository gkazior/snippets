# prolog cheatsheet


## Code standard

    %% predicate_name(+InputArg, ?IntermediateArg, -OutputArg)
    %
    %     description for the predicate should follow its name
    %
    % +InputArg        - instantiated input argument always on the left of argument list
    % ?IntermediateArg - instantiaded ot not intermediate arguments in the middle
    % -OutputArg       - var on entry output argument at the end
    %
    % [Note 1] Long comment about how pred/n depends on subgoal/k...
    % ...
    predicate_name([], Value, Value).
    predicate_name([InputHead|InputTail], Value, OutputValue) :-
       subgoal(InputHead, Value),                                              % See [Note 1] above.
       last_subgoal(Value, OutputValue).

  * after (http://arxiv.org/pdf/0911.2899v3.pdf)


## Tests


# Links

## General
 * (http://arxiv.org/pdf/0911.2899v3.pdf) code style
 * (http://kti.mff.cuni.cz/~bartak/prolog/learning.html)
 * (http://www.pathwayslms.com/swipltuts/) Real World Programming in SWI-Prolog
 * (http://lpn.swi-prolog.org/lpnpage.php?pageid=online) Learn Prolog Now

## DCG

 * (http://www.metalevel.at/dcg.html)
 * (http://www.pathwayslms.com/swipltuts/dcg/)

## CLP

 * (http://www.pathwayslms.com/swipltuts/clpfd/clpfd.html) CLP(FD) Constraint Logic Programming over Finite Domains
