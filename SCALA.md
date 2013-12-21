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
  * [Course: Functional Programming Principles in Scala] (http://www.coursera.org/course/progfun)
  * [Course: Principles of Reactive Programming ]        (http://www.coursera.org/course/reactive)

## enum in scala

    sealed case class State(name: String)
    object begin       extends State("begin")
    object inTheMiddle extends State("in the middle")
    object end         extends State("end")

    object processor {
      def processState(state: State) {
        state match {
          case begin       => println(s"Great!    state: $begin")
          case end         => println(s"Was nice! state: $end")
          case inTheMiddle => println(s"Working!  state: $inTheMiddle")
        }
      }
    }

    processor.processState(begin)                   //> Great!    state: State(begin)
