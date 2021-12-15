# Scala tutorial

## Documentation general

* [Tutorials](http://docs.scala-lang.org/tutorials/)
* [Cheat sheet](http://docs.scala-lang.org/cheatsheets/)
* [Glossary] (http://docs.scala-lang.org/glossary/)
* [Case classes] (http://docs.scala-lang.org/tutorials/tour/case-classes.html)

## Libraries

* [Collections] (http://docs.scala-lang.org/overviews/collections/sets.html)
* [Akka]        (http://doc.akka.io/docs/akka/2.1.4/)

## Testing

* [Scalatest](http://www.scalatest.org/)

## Play documentation

*  [Newest version docs](http://www.playframework.com/documentation)
*  [ScoopIt](http://www.scoop.it/t/playframework)
*  [Send email in play] (http://blog.knoldus.com/2014/03/15/adding-an-email-sending-functionality-in-play-using-scala/)

## Scala collections

*  [docs](https://docs.scala-lang.org/overviews/core/architecture-of-scala-collections.html)
*  [so cheatsheet](https://stackoverflow.com/questions/1722137/scala-2-8-collections-design-tutorial)
*  [Odersky art](https://www.scala-lang.org/old/sites/default/files/sids/admin/Tue,%202010-07-20,%2010:39/collections.pdf)

## Scala and JVM options
* [StandardScalaSettings.scala]  (https://github.com/scala/scala/blob/2f1b5259188698501dbc8430f63972bf7bc68154/src/compiler/scala/tools/nsc/settings/StandardScalaSettings.scala)
* [AllSettings.scala]  (https://github.com/scala/scala/blob/2f1b5259188698501dbc8430f63972bf7bc68154/src/compiler/scala/tools/nsc/settings/ScalaSettings.scala)
* [JVM options] (http://www.oracle.com/technetwork/articles/java/vmoptions-jsp-140102.html)
* [Troubleshooting] (http://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/index.html)
* [Postmortem] (http://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr023.html#BABEFHCI)
* [jmap] (http://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr014.html#BABGAFEG)
* [jstack] (http://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr016.html#BABFCHDE)

## Nice to look at

* [Coursera] (http://www.coursera.org/)
 * [Course: Functional Programming Principles in Scala] (http://www.coursera.org/course/progfun)
 * [Course: Principles of Reactive Programming ]        (http://www.coursera.org/course/reactive)

## sbt spells

    # To enable debugging: enable java debug on standard IntelliJ Idea port
    set SBT_OPTS=-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005
    sbt run

    # to enable offline mode in interactive mode
    # more on: http://alvinalexander.com/scala/setting-putting-sbt-into-offline-mode-no-wifi
    set offline := true

    # to start sbt in offline mode
    sbt "set offline := true" run
    
    # to generate maven pom
    # see the generated pom in the target 
    sbt make-pom    
    
    # to re-run with -deprecation for detail
    sbt -mem 2048
    set scalacOptions in ThisBuild ++= Seq("-unchecked", "-deprecation", "-feature")
    compile

## Command line spells

    # command line for running remote JVM
    -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005

## Exceptions

  * To catch or not to catch (https://www.sumologic.com/2014/05/05/why-you-should-never-catch-throwable-in-scala/)
  * To catch or not to catch (https://tersesystems.com/2012/12/27/error-handling-in-scala/)

## enum in scala

    sealed trait State

    object State {
      sealed protected abstract class StateImpl(name: String) extends State {
          override def toString = s"State($name)"
      }      
      case object Begin extends StateImpl("begin")
      case object InTheMiddle extends StateImpl("in the middle")
      case object End extends StateImpl("end")
      
      def values = Seq(Begin, InTheMiddle, End)
    }


    object Processor {
      def processState(state: State) {
        state match {
          case State.Begin => println(s"Great!    state: $State.Begin")
          case State.End => println(s"Was nice! state: $State.End")
          case State.InTheMiddle => println(s"Working!  state: $State.InTheMiddle")
        }
      }
      def main(args: Array[String]) {
        Processor.processState(State.Begin)
        Processor.processState(State.End)
        
        State.values foreach println
      }
    }


## Pattern matching

### simple example


    val optionalValue = Some("Hello")
    optionalValue match {
     case None        => println("Nothing in the value")
     case Some(value) => println(s"I have found [$value]")
    }

## Code style

  * Documentation (https://gist.github.com/gkazior/dc1e8f48282afdad4e24)


## Iteration

### over list

    val l = List("a","b","c")
    l foreach {println(_)}
    l map     {println(_)}

### for int
    for (i <- 0 to 5) {println(i)}


## Futures

*  [Future basics in my gist] (https://gist.github.com/gkazior/a97b47dc5dc081e483a5)



