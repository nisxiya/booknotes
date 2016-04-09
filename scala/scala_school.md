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

### foreach
`foreach` is very like `map`, except that `foreach` does not return the values.

```
scala> var ret = numbers.foreach( {i:Int => i*2} )
ret: Unit = ()
```
NOTE: `Unit` just means `void`

### filter
`filter` will filter out any elements that does fit from the input list

```
scala> var numbers = List(1,2,3,4,5,6,7,8,9)
numbers: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9)

scala> numbers.filter( (i:Int) => i%2==0 )
res47: List[Int] = List(2, 4, 6, 8)

scala> def isEven = (i:Int) => i%2 == 0
isEven: Int => Boolean

scala> numbers.filter(isEven)
res48: List[Int] = List(2, 4, 6, 8)
```

### zip
zip will combile two lists into one
```
scala> List(1,2,3).zip(List("a", "b", "c"))
res49: List[(Int, String)] = List((1,a), (2,b), (3,c))

// Now each element in the new list is a tuple
```

### partition
`partition` will split the list into two sub lists, with a given function which returns boolean.
```
scala> numbers.partition(isEven)
res58: (List[Int], List[Int]) = (List(2, 4, 6, 8),List(1, 3, 5, 7, 9))
```

### find
`find` will try to find the first matched element, and return it.
```

scala> numbers
res60: List[Int] = List(1, 2, 3, 4, 5, 6, 7, 8, 9)

scala> numbers.find(isEven)
res61: Option[Int] = Some(2)
```

### flatten
flatten will flatten an nested list
```
scala> List(List(1,2), List(2,3))
res62: List[List[Int]] = List(List(1, 2), List(2, 3))

scala> List(List(1,2), List(2,3)).flatten
res63: List[Int] = List(1, 2, 2, 3)
```

### flatMap
As for a nested List, first do the mapping, and then do the flatten
```

scala> var nestedNumbers = List(List(1,2), List(2,3))
nestedNumbers: List[List[Int]] = List(List(1, 2), List(2, 3))

scala> nestedNumbers.flatMap(x => x.map( (i:Int)=>i*2 ))
res64: List[Int] = List(2, 4, 4, 6)
```
It is the same as
```
scala> nestedNumbers.map((x: List[Int]) => x.map(_ * 2)).flatten
```

## Map
All function combinators can be applied to Map. Map can be treated as a list of Two-element Tuple.
```
scala> var extensions = Map("a"->100, "b"->200, "c"->300, "d"->400)
extensions: scala.collection.immutable.Map[String,Int] = Map(a -> 100, b -> 200, c -> 300, d -> 400)

scala> extensions.filter( (entry:(String,Int)) => entry._2 > 200)
res70: scala.collection.immutable.Map[String,Int] = Map(c -> 300, d -> 400)
```


## compose

`compose` will compose two function together, to make a more complex function
```
scala> def f(s:String) = "f(" + s + ")"
f: (s: String)String

scala> def g(s:String) = "g(" + s + ")"
g: (s: String)String

scala> var fComposeG = f _ compose g _
fComposeG: String => String = <function1>

scala> fComposeG ("yay")
res76: String = f(g(yay))
```

## andThen
`andThen` looks very similar to `compose`. 
```
scala> var fAndThenG = f _ andThen g _
fAndThenG: String => String = <function1>

scala> fAndThenG("yay")
res77: String = g(f(yay))
```


## partial function

```

scala> var one:PartialFunction[Int,String] = { case 1 => "one" }
one: PartialFunction[Int,String] = <function1>

scala> one.isDefinedAt(1)
res78: Boolean = true

scala> one.isDefinedAt(2)
res79: Boolean = false

scala> one(1)
res80: String = one

scala> one(2)
scala.MatchError: 2 (of class java.lang.Integer)
  at scala.PartialFunction$$anon$1.apply(PartialFunction.scala:253)
    at scala.PartialFunction$$anon$1.apply(PartialFunction.scala:251)
      at $anonfun$1.applyOrElse(<console>:10)
        at $anonfun$1.applyOrElse(<console>:10)
          at scala.runtime.AbstractPartialFunction.apply(AbstractPartialFunction.scala:36)
            ... 33 elided
            
scala> var two:PartialFunction[Int,String] = { case 2 => "two" }
two: PartialFunction[Int,String] = <function1>

scala> var three: PartialFunction[Int, String] =  { case 3 => "three" }
three: PartialFunction[Int,String] = <function1>

scala> var wildcard: PartialFunction[Int,String] = { case _ => "soemthing else" }
wildcard: PartialFunction[Int,String] = <function1>

scala> var partial = one orElse two orElse three orElse wildcard
partial: PartialFunction[Int,String] = <function1>

scala> partial(1)
res82: String = one

scala> partial(2)
res83: String = two

scala> partial(4)
res84: String = soemthing else
```

## Static Type

Type checking ensures that every wrong program wont pass the compiling. But it does not guarantee
all the right programs will pass.

### parameters polymorphism

### implicit type convert
```
scala> implicit def strToInt(x:String) = x.toInt
warning: there was one feature warning; re-run with -feature for details
strToInt: (x: String)Int

scala> "123"
res92: String = 123

scala> val y:Int = "123"
y: Int = 123

scala> math.max("123", 111)
res93: Int = 123
```
