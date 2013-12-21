# Scala tutorial

## Documentation

* [Tutorials](http://docs.scala-lang.org/tutorials/)
* [Cheat sheet](http://docs.scala-lang.org/cheatsheets/)
* [Glossary] (http://docs.scala-lang.org/glossary/)
* [Case classes] (http://docs.scala-lang.org/tutorials/tour/case-classes.html)

## Play documentation

*  [Newest version docs](http://www.playframework.com/documentation)

## Nice to look at

*  [Coursera] (http://www.coursera.org/)

** [Course: Functional Programming Principles in Scala] (http://www.coursera.org/course/progfun)
** [Course: Principles of Reactive Programming ]        (http://www.coursera.org/course/reactive)

## enum in scala

        sealed case class State(name: String)
        object begin       = State("begin")
        object inTheMiddle = State("in the middle")
        object end         = State("end")

        object Processor {
           def processState
        }
