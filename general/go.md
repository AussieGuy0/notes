# Go

## Setup

### Installation
Ubuntu 20.04+

`sudo apt install golang`

### Usage
To compile and run program:

`go run program.go`

## Hello World
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello world!")
}
```

## Imports
Single Import

```go
import "fmt"
```

Multiple imports

```go
import (
    "fmt"
    "math/rand"
)
```

## Exports
A name (Note: does this mean functions, types, variables?) is exported if it
begins with a capital letter.

## Functions
Types come after the variable name

```go
func add(x int, y int) int {
    return x + y
}
```

Consecutive parameters with same type can be shortened like this:

```go
func add(x, y int) int {
    return x + y
}
```

Functions can return multiple results

```go
func swap(x, y string) (string, string) {
    return y, x
}

a, b := swap("hello", "world")
// a == "world"
// b == "hello"
```

You can also have 'named return variables' (aka naked return). However, they are
discouraged for longer functions

```go
func rand2() (x, y int) {
   x = rand.Intn(10)
   y = rand.Intn(10)
   return
}

// equivalent to
func rand2() (int, int) {
   x := rand.Intn(10)
   y := rand.Intn(10)
   return x, y
}
```

## Variables
```go
var x = 72

func main() {
    var i, j int = 1, 2
    k := 3
    c, python, java := true, false, "no!"
    fmt.Println(i, j, k, c, python, java)
}
```

## Loops
There is only the `for` loop in go. This is like the standard for loop in java,
javascript, etc.

```go
sum := 0
for i := 0; i < 10; i++ {
    sum += i
}
```

init and post statements are optional
```go
sum := 0
for ; sum < 10; {
    sum += sum
}

// Equivalent to

sum := 0
for sum < 10 { // Dropped the semi-colons
    sum += sum
}
```

Infinite loops
```go
for {
}
```

## Switch
Switches are similar to Java/Javscript. A thing to note is that there is a
implicit break statement after each case statement.

```go
a := getInput()
switch a {
    case 1:
        fmt.Println("Option 1")
    case 2:
        fmt.Println("Option 2")
    default:
        fmt.Println("Default Option")
}
```


## Links
- [Tour of Go](https://tour.golang.org/)
- [Effective Go](https://golang.org/doc/effective_go.html#introduction)
