# Scala Tutorial

## Tuple
a tuple datastructure
```
var hostPort = ("localhost", 80)
// equal as the following
var hostPort = "localhost" -> 80
```

matching in tuple
```
hostPort match {
  case ("localhost", 80) => "Match1"
  case ("localhost", 8080) => "Match2"
  case _ => "match default then"
  
}
```

## Map
```
Map(1 -> 2)
Map("foo" -> "bar")
```
or we can use unfixed number of parameters
```
Map(1->"one", 2->"two")
```

How to use it?
```
Map("one"->1) .get("one")
```
## Option
Option refers to a container that maybe contain the values.
The interface of option is as the following.
```
trait Option[T] {
  def isDefined: Boolean
  def get: T
  def getorElse(t: T): T
}
```

```
scala> var numbers = Map("one"->1, "two"->2)
numbers: scala.collection.immutable.Map[String,Int] = Map(one -> 1, two -> 2)

scala> numbers.get("two")
res31: Option[Int] = Some(2)

scala> numbers.get("three")
res32: Option[Int] = None
```

to continue the above

```
var resThree = numbers.get("three")
// Now the resThree should be None
// How to get its values

// way 1
var result = if (resThree.isDefined) {
  resThree * 2
} else {
  0
}

// way 2
var result = resThree.getorElse(0) * 2 // if resThree is None, then return 0 * 2; otherwise return real value * 2

// way 3
var result = resThree match {
  case Some(n) => n * 2
  case None => 0 * 2
}
```

## Function Combinators
The function combinators are the stuff that can combine a function to the vector/collection, commonly including `map`, `foreach`, `filter`, `zip`, `partition`, etc.

### map
```
scala> var numbers = List(1,2,3)
numbers: List[Int] = List(1, 2, 3)

// apply anonymous functions
scala> numbers.map( (i:Int) => i*i )
res42: List[Int] = List(1, 4, 9)

scala> numbers.map( { i:Int => i*i } )
res43: List[Int] = List(1, 4, 9)

```

instead of using the anonymous functions, you can also use the pre-defined functions, ;)
```
scala> def timesTwo(i:Int) = i*2
timesTwo: (i: Int)Int

scala> numbers.map(timesTwo)
res44: List[Int] = List(2, 4, 6)

scala> def timesThree(i:Int):Int = i*3
timesThree: (i: Int)Int

scala> numbers.map(timesThree _)
res45: List[Int] = List(3, 6, 9)
```
