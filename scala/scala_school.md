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
