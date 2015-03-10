# Clojure tutorial

## Language

        ;; one line comment

        ;; list
        (1 2 3)

        ;; map
        {1 "one", 2 "two", 3 "three"}

        ;; vector
        [1 2 3]


## Map operations

        (get {1 "one", 2 "two"} 1)                       ;; one
        (assoc {1 "one", 2 "two"} 1 "odin")              ;; {1 "odin", 2 "two"}

        (assoc {1 "one", 2 "two"} 3 "three")             ;; {3 "three", 1 "one", 2 "two"}
        (dissoc {1 "one", 2 "two", 3 "three"} 3)         ;; -> {1 "one", 2 "two"}

        (conj {1 "one", 2 "two"} {3 "three"})            ;; {3 "three", 1 "one", 2 "two"}


        (merge {1 "one", 2 "two"} {1 "one", 3 "three"})  ;; {3 "three", 1 "one", 2 "two"}

        (keys {1 "one", 2 "two"})                        ;; (1 2)
        (vals {1 "one", 2 "two"})                        ;; (one two)

## Extending the syntax

        (defn fun [a] (print (str "hello" " " a)))
        (fun "world")

        (def message "hello man")

## partials

        (def add2 (partial + 2))

## functions returning functions

        (defn get-add-n [n] (fn [x] (+ n x)))
        (def fn-add2 (get-add-n 2))
        (fn-add2 4)

## More function syntax


## Basic list functions

        (apply + (1 2 3))


### Strings

        (str  "First " " then " " second")        ;; concatenation
        (subs "String" 1 3) ;; tr
        (subs "String" 1)   ;; tring


### Patterns java.util.regex!

        (re-pattern "[a-zA-Z]*")
        (re-matches #"(\\w)*" "test two words")


### Structs

        (defstruct person :first-name :last-name)
        (def person1 (struct-map person :first-name "John" :last-name "Smith"))
        (person1 :first-name)

        ;; this one should be fastest
        (def get-first-name (accessor person :first-name))

### Refs

        (def my-ref (ref 4))
        (print my-ref)                        ;; #<Ref@1f2cea2: 4>
        (+ 2 @my-ref)                         ;; 6
        (ref-set my-ref 6)                    ;; IllegalStateException No transaction running  clojure.lang.LockingTransaction.getEx
        (dosync (ref-set my-ref 6))           ;; works fine
        (dosync (alter my-ref + 4))           ;; sets to 10 and return 10
        (dosync (commute my-ref + 10))        ;; commuttative will not lock


### TODO

        sequences: lazy, take, iterate
        protocols
        actors
