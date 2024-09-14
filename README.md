# Go compendium
Go language compendium

---
### Why Go?

- **Built-in Concurrency Mechanism** that was **designed to run on multiple cores** and to support concurrency.
- **Concurrency is cheap and easy** compared to other languages like C++ or Java.
- For **Performant** applications and running on **scaled, distributed systems**.
- E.g. *Docker and K8s* are written in GO.
- Faster than interpreted languages like Python. 


---
### Why Go Modules Replace GOPATH:

Go modules use the `go.mod` file to manage dependencies for each project, and you can create Go projects anywhere in your file system, not just within the `GOPATH` directory.
Each project is self-contained, meaning that each project has its own module file (`go.mod`) to manage its dependencies independently of other projects.

*By default, `GOPATH` is set to `~/go`, but this is only relevant if you're using legacy projects that rely on the `GOPATH` structure*.
For modern Go development using modules, there's no need to manually manage `GOPATH` unless you're working on older projects.

Only need to set `GOPATH` in the following cases:
- You're working on older Go projects that still rely on the `GOPATH` workspace model.
- You prefer to have a central location where Go binaries (go install) and packages are installed, *but even this is optional since modules handle dependencies locally*.


---
### Go Commands summary:

| **Command**           | **Usage**                          | **Description**                                                                 | **Example**                                                                 |
|-----------------------|------------------------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| `go mod init`         | `go mod init module-name`           | Initializes a new Go module. Creates a `go.mod` file for dependency management. | `go mod init github.com/yourusername/gocomp`                                |
| `go mod tidy`         | `go mod tidy`                       | Cleans up `go.mod` and `go.sum` by removing unused dependencies and adding missing ones. | `go mod tidy`                                                               |
| `go build`            | `go build [package]`                | Compiles Go source code into an executable binary.                              | `go build` (builds the project in the current directory)                    |
| `go run`              | `go run file.go`                    | Compiles and runs the specified Go source file(s).                              | `go run main.go`                                                            |
| `go test`             | `go test [package]`                 | Runs tests in the specified package or directory.                               | `go test ./...` (runs all tests in the current directory and subdirectories)|
| `go fmt`              | `go fmt [files or packages]`        | Formats Go source code according to the standard Go style.                       | `go fmt ./...` (formats all Go files in the current directory and subdirectories) |
| `go get`              | `go get package`                    | Downloads and installs the specified package along with its dependencies.       | `go get github.com/some/package`                                            |
| `go install`          | `go install package`                | Compiles and installs the specified Go package.                                 | `go install github.com/yourusername/gocomp` (installs the `gocomp` package) |
| `go list`             | `go list [package]`                 | Lists Go packages, including their module path and metadata.                    | `go list github.com/yourusername/gocomp`                                    |
| `go mod edit`         | `go mod edit -require=module@version` | Edits the `go.mod` file to add or remove dependencies.                          | `go mod edit -require=github.com/some/package@v1.2.3`                      |
| `go env`              | `go env`                            | Displays Go environment variables and configuration.                            | `go env`                                                                     |
| `go doc`              | `go doc [package]`                  | Displays documentation for the specified package or symbol.                     | `go doc github.com/yourusername/gocomp`                                     |
| `go version`          | `go version`                        | Shows the installed Go version.                                                  | `go version`                                                                 |
| `go mod why`          | `go mod why package`                | Explains why a specific module is needed by your module.                        | `go mod why github.com/some/package`                                        |
| `go mod vendor`       | `go mod vendor`                     | Creates a `vendor` directory with copies of all dependencies for offline builds. | `go mod vendor`                                                              |


---
### Module paths for downloadable packages

If you’re creating a project which can be downloaded and used by other people and programs, then it’s good practice for your module path to equal the location that the code can be downloaded from.

For instance, if your package is hosted at https://github.com/foo/bar then the module path for the project should be github.com/foo/bar.


---
### Packages, Variables, and Constants:

- All code must belong to **packages**, i.e. all code is organized in **packages**. The first statement in a file should be a package declaration. **A package is a set of related source files** with their functions, e.g. [`fmt`](https://pkg.go.dev/fmt) and its functions to print in different formats like `Println` or `Printf` using printing verbs like `%v`, `%s`, `%d`, `%t`, etc.
- **Variables** are used to store values and reuse/update values like *containers*. Variables are declared with the `var` keyword.
- **Go Compile Errors to enforce better code quality**, e.g. leaving a `var` without a call/usage highlights an error (variables must be used) or trying to update a `const` value from 50 to 30. 
- **Go is a Statically Typed** language, i.e. Go Compiler will throw an error if a variable is not declared with a type, this is called **Type Checking**, unless the type of the variable could be inferred from its assigned value during the declaration, e.g. `a := 10`, `var a = 10`, `var a int = 10` are valid declarations in Go but `var a // declaration without assignment and after few lines of code being assigned with a = 10` is an error. 
**Type Inference** is when Go compiler infers the type of variable based on the assigned value. *Note `:=` can only be used in variables and NO to `const`*


---
### Data Types:

| Data Type   | Description                                  | Example                                  |
|-------------|----------------------------------------------|------------------------------------------|
| **bool**    | Represents a Boolean value (true or false).  | `var isActive bool = true`               |
| **string**  | Sequence of characters.                      | `var name string = "GoLang"`             |
| **int**     | Signed integer (size depends on platform).   | `var age int = 30`                       |
| **int8**    | 8-bit signed integer (-128 to 127).          | `var smallNum int8 = -10`                |
| **int16**   | 16-bit signed integer (-32,768 to 32,767).   | `var mediumNum int16 = 300`              |
| **int32**   | 32-bit signed integer (-2^31 to 2^31-1).     | `var largeNum int32 = 100000`            |
| **int64**   | 64-bit signed integer (-2^63 to 2^63-1).     | `var bigNum int64 = 100000000000`        |
| **uint**    | Unsigned integer (size depends on platform). | `var index uint = 10`                    |
| **uint8**   | 8-bit unsigned integer (0 to 255).           | `var byteVal uint8 = 255`                |
| **uint16**  | 16-bit unsigned integer (0 to 65,535).       | `var smallIndex uint16 = 500`            |
| **uint32**  | 32-bit unsigned integer (0 to 4,294,967,295).| `var mediumIndex uint32 = 100000`        |
| **uint64**  | 64-bit unsigned integer (0 to 2^64-1).       | `var largeIndex uint64 = 1000000000`     |
| **float32** | 32-bit floating-point number.                | `var price float32 = 9.99`               |
| **float64** | 64-bit floating-point number.                | `var pi float64 = 3.14159`               |
| **complex64** | Complex number with float32 real and imaginary parts. | `var c complex64 = 2 + 3i`      |
| **complex128**| Complex number with float64 real and imaginary parts. | `var c complex128 = 2 + 3i`   |
| **byte**    | Alias for `uint8`, represents a byte.        | `var b byte = 255`                       |
| **rune**    | Alias for `int32`, represents a Unicode character. | `var char rune = 'A'`               |
| **array**   | Fixed-size sequence of elements of the same type. | `var nums [3]int = [3]int{1, 2, 3}`   |
| **slice**   | Dynamic-size sequence of elements of the same type. | `var nums []int = []int{1, 2, 3}`   |
| **map**     | Key-value pairs, where keys and values can be of any type. | `var dict map[string]int = map[string]int{"a": 1}` |
| **struct**  | Collection of fields.                        | `type Person struct { Name string; Age int }` |
| **pointer** | Holds the memory address of a value.         | `var ptr *int = &age`                    |
| **interface** | Abstract type to represent any type.       | `var i interface{} = "hello"`            |
| **function** | A function signature with parameters and return values. | `func add(a int, b int) int { return a + b }` |


---
### Pointers:

Variables are stored in memory but when we reference a variable we are actually pointing to its memory address, i.e.
**a Pointer is a Variable that points to the Memory Address of another Variable** -*special variable* that holds the memory address of the other variable, e.g. printing a pointer returns the memory address of the variable pointed while printing a variable returns the actual value.

![Pointer](./img/0-pointer.png?raw=true)

```go
fmt.Println("Pointer of soldTickets is", &soldTickets, "and its Variable value", soldTickets)	
```	
```text
// output console
Pointer of soldTickets is 0xc0000ac00b and its Variable value 20
```


---
### Arrays and Slices:

**Arrays and Slices** are data structures to **store collections of elements in a Single Variable**.

- **An Array has a Fixed size**, i.e. how many elements the array can hold, 
e.g. `var nums [3]int`, `var nums = [3]int{1, 2, 3}`, `var nums = [3]int{1}` and `var nums = [3]int{}` are valid declarations.
**Arrays are indexed starting from 0**, e.g. `nums[0] = 1` and `nums[1] = 10`. Examples of updating an array inside a function: 
```go
func main() {
    var conferenceName = "Go Conference"
    const totalTickets uint8 = 50
    var remainingTickets uint8 = 30
    soldTickets := calculateSoldTickets(remainingTickets, totalTickets)
    var bookings [totalTickets]string
    initBookings(totalTickets, soldTickets, &bookings)
    // ... more code here
}

// Must pass booking Pointer otherwise array will be passed by copy and original array values won't be updated.
// An alternative approach is to return the copy of the bookings array and then replacing the original after the function is called.
func initBookings(totalTickets uint8, soldTickets uint8, bookings *[50]string) {
    for i := 0; i < int(totalTickets); i++ {
        if i < int(soldTickets) {
            // must update the actual array value not the pointer, i.e. doing dereference:
            (*bookings)[i] = "SOLD"
        } else {
            // Go has syntactic sugar that simplifies working with pointers to arrays.
            // When you use bookings[i], Go automatically dereferences the pointer for you to access the array element,
            // so you don’t need to explicitly write (*bookings)[i].
            bookings[i] = "AVAILABLE"
        }
    }
}
```

- **Slice is an abstraction of Array that has Dynamic size**, more flexible and powerful, i.e. slices are also **index-based** and **have a size, but is Resized when Needed**. More flexible and powerful than arrays, i.e. **Variable-length** or get a sub-array of its own.     

⚠️ **Note passing a Slice as a parameter is different from passing an Array as a parameter as GO passes Slices by Reference and Arrays by Value**, i.e.:

**1. Slices Are Passed by Reference**
**A slice in Go is a descriptor** that contains:
- **A pointer to the underlying array**.
- A length (the number of elements in the slice).
- A capacity (the size of the underlying array).

When you pass a slice to a function, Go passes this descriptor (which includes the pointer to the underlying array). This means:
- **Modifications to the slice elements inside the function** will affect the original slice since it references the same underlying array.
- The slice header (pointer, length, capacity) itself is passed by value, but the pointer still points to the same underlying array, allowing shared access to the elements.

Example:
```go
func modifySlice(s []int) {
    s[0] = 100 // This modifies the original array
}

func main() {
    numbers := []int{1, 2, 3}
    modifySlice(numbers) // Modifies the original slice
    fmt.Println(numbers) // Output: [100 2 3]
}
```

**2. Arrays Are Passed by Value**
In contrast, when you pass an array to a function, Go passes **a copy** of the entire array. This means:
- Modifications to the array inside the function will not affect the original array outside the function because the function is working with a **copy** of the original array.
- **Arrays are fixed in size and passing them can be inefficient for large arrays since the entire array is copied**.

Example:
```go
func modifyArray(a [3]int) {
    a[0] = 100 // Modifies only the copy of the array
}

func main() {
    numbers := [3]int{1, 2, 3}
    modifyArray(numbers) // Passes a copy of the array
    fmt.Println(numbers) // Output: [1 2 3] - Original array is unchanged
}
```

**Key Differences Between Array and Slice in General:**

| Aspect               | Slice                                      | Array                                       |
|----------------------|--------------------------------------------|---------------------------------------------|
| **Passing Behavior**  | Passed by reference (pointer to array)     | Passed by value (entire array is copied)    |
| **Size**              | Dynamic, can change size (flexible length) | Fixed size (defined at declaration)         |
| **Modification**      | Changes inside the function affect original | Changes inside the function affect only the copy |
| **Efficiency**        | More efficient for large data since only the descriptor is passed | Less efficient for large arrays as the entire array is copied |
| **Underlying Data**   | Slices reference an underlying array       | Arrays do not have a separate underlying structure |
| **Use Case**          | Preferred when working with collections of unknown or variable size | Used for fixed-size collections              |

**Key Differences Between Array and Slice 'Length':**

| Aspect              | Array                                        | Slice                                      |
|---------------------|----------------------------------------------|--------------------------------------------|
| **Size**            | Fixed size, set at declaration.              | Dynamic size, can grow or shrink.          |
| **`len()` Result**  | Always returns the fixed size of the array.  | Returns the current number of elements.    |
| **Mutability**      | The length cannot be changed after creation. | The length can change as elements are added or removed. |
| **Capacity**        | The length is equals to the Capacity, as it's a fixed size.| Capacity is separate from length and can be larger than the length. |
