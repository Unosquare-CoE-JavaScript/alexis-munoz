# Go For Javascript Developers

## Installation

- Got the offical golang page `golang.org/dl` and installe it.

- Add these to your `~/.bashrc` file:

```bash
export GOPATH=$HOME/go
export GOBIN=$GOPATH/bin
export PATH=$PATH:$GOBIN
```

### Know your version

`go version`

### Getting Started

### Output commands

The `fmt.Println()` command is used to print to the console.

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

The `fmt.Printf()` command is used to print to the console with a format.

```go
package main

import "fmt"

func main() {
    fmt.Printf("Hello, %s!", "Alexis")
}
```

### Variable declaration and Types

And Go has a lot of types.

```go
package main

    import "fmt"

    func main() {
        var x int = 1
        var y string = "Hello"
        var z bool = true
        var f float32 = 4.2

        fmt.Printf("%v\n", x)
        fmt.Printf("%v\n", y)
        fmt.Printf("%v\n", z)
        fmt.Printf("%v\n", f)
    }
```

We can check the varible type by using the `reflect` package.

```go
package main

    import "fmt"
    import "reflect"

    func main() {
        var x int = 1
        var y string = "Hello"
        var z bool = true
        var f float32 = 4.2

        fmt.Printf("%v\n", reflect.TypeOf(x))
        fmt.Printf("%v\n", reflect.TypeOf(y))
        fmt.Printf("%v\n", reflect.TypeOf(z))
        fmt.Printf("%v\n", reflect.TypeOf(f))
    }
```

### Declaring and initializing variables without using the `var` keyword and type

```go
package main

    import "fmt"

    func main() {
        x := 1
        y := "Hello"
        z := true
        f := 4.2

        fmt.Printf("%v\n", x)
        fmt.Printf("%v\n", y)
        fmt.Printf("%v\n", z)
        fmt.Printf("%v\n", f)
    }
```

### If else Statements

```go
package main

    import "fmt"

    func main() {
        x := 1
        y := 2

        if x < y {
            fmt.Printf("%v is less than %v\n", x, y)
        } 
        else if x > y {
            fmt.Printf("%v is greater than %v\n", x, y)
        } 
        else {
            fmt.Printf("%v is equal to %v\n", x, y)
        }
    }
```

### Switch Statements

```go
package main

    import "fmt"

    func main() {
        x := 1

        switch x {
            case 0:
                fmt.Printf("%v is equal to 0\n", x)
            case 1:
                fmt.Printf("%v is equal to 1\n", x)
            case 2:
                fmt.Printf("%v is equal to 2\n", x)
            default:
                fmt.Printf("%v is not equal to 0, 1, or 2\n", x)
        }
    }
```

### For Loops

```go
package main

    import "fmt"

    func main() {
        for i := 0; i < 10; i++ {
            fmt.Println(i)
        }
    }
```

#### The range keyword

```go
    package main

        import "fmt"

        func main() {
            x := []int{1, 2, 3, 4, 5}

            for i, v := range x {
                fmt.Println(i, v)
            }
        }
```

### Functions

The functions in go are declared with the `func` keyword.

```go
package main

    import "fmt"

    func main() {
        fmt.Println(add(1, 2))
    }

    func add(x int, y int) int {
        return x + y
    }
```

### Arrays

Arrays in go are declared with the `[]` keyword.

```go
package main

    import "fmt"

    func main() {
        x := [5]int{1, 2, 3, 4, 5}

        for i, v := range x {
            fmt.Println(i, v)
        }
    }
```

### Maps

Maps in go are declared with the `map` keyword

```go
package main

    import "fmt"

    func main() {
        x := map[string]int{
            "one": 1,
            "two": 2,
            "three": 3,
        }

        for k, v := range x {
            fmt.Println(k, v)
        }
    }
```

### Import files

utils/math.go

```go
package Utils

import (
    "fmt"
    "math"
)

Add(x int, y int) int {
    return x + y
}
```

main.go

```go
package main

import (
 "example-project-go/utils"
 "fmt"
)

func main() {
    fmt.Println(utils.Add(1, 2))
}
```

**Note:** The `example-project-go` folder is created in the `$GOPATH/src` folder.

### Testing

The `testing` package is used to test the code in go.

```go
package utils

    import (
    "testing"
    )

    func TestAdd(t *testing.T) {
    expected := 15
    actual := Add(1, 2, 3, 4, 5)
    if actual != expected {
    t.Errorf("Expected %d, got %d", expected, actual)
    }
}
```

### Testing with the `go test` command

The go test command is used to run the tests.

```go
go test
```

### Structs

The structs in go are declared with the `struct` keyword.

```go
package main

    import "fmt"

    type Person struct {
        Name string
        Age int
    }

    func main() {
        p := Person{
            Name: "Alexis",
            Age: 24,
        }

        fmt.Println(p)
    }
```

### Custom types

Custom types are declared with the `type` keyword.

```go
package main

    import "fmt"

    type Person struct {
        Name string
        Age int
    }

    func main() {
        p := Person{
            Name: "Alexis",
            Age: 24,
        }

        fmt.Println(p)
    }
```

### Pointers

The pointers in go are declared with the `*` symbol.

```go
package main

    import "fmt"

    var name string
    var namePointer *string

    func main() {

        namePointer = &name
        var nameValue =  *namePointer

        fmt.Println(name)

        fmt.Println(nameValue)
        fmt.Println(namePointer)
    }
```

### Error Handling

Error Handling in go is done with the `error` type.

```go
package main

    import (
    "fmt"
    "errors"
    )

    func main() {
        err := errors.New("This is an error")
        if err != nil {
            fmt.Println(err)
        }
    }
```

### Interfaces

Interfaces in go are declared with the `interface` keyword.

```go
 type Vehicle interface {
    drive()
    brake()
 }
```

### Web servers & Routes

The `net/http` package is used to create web servers.

```go
package main

import (
 "fmt"
 "net/http"
)

func main() {
 http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
  fmt.Fprintf(w, "Hello World")
 })
 http.ListenAndServe(":8080", nil)
}

```

### Concurrency

In go there are two types of concurrency: `goroutines` and channels. A `goroutine` is a lightweight thread of execution implemented by adding the go keyword before executing a function.
