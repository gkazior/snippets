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
*  [Send email] (http://blog.knoldus.com/2014/03/15/adding-an-email-sending-functionality-in-play-using-scala/)

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




## pattern matching

### simple example

  val optionalValue = Some("Hello")

  optionalValue match {
    case None        => println("Nothing in the value")
    case Some(value) => println(s"I have found [$value]")
  }

### Simple case class

  sealed trait Breed
  object terrier extends Breed
  object spaniel extends Breed

  case class Dog(name: String, breed: Breed)

  val myDog = Dog("spider", terrier)

  def whenYouSee(dog: Dog) = {
    dog match {
      case myDog           =>
      case Dog("spider", )
    }
  }

### When I need a dog

  a @ (MyFirst | MySecond)
case x if f1(x)
