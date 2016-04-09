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
Option refers to a container that maybe include some numeric values.
The interface of option is as the following.
```
trait Option[T] {
  def isDefined: Boolean
  def get: T
  def getorElse(t: T): T
}
```
