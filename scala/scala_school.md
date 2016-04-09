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

