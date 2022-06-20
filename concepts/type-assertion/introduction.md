# Introduction to Type Assertions

Interfaces in Go can introduce ambiguity about the underlying type.
A type assertion allows us to extract the interface value's underlying concrete value using this syntax: `interfaceVariable.(concreteType)`.

For example:

```go
var thing interface{} = 12
number := thing.(int)
```

NOTE: this will cause a panic if the interface variable does not hold a value of the concrete type.

We can test whether an interface value holds a specific concrete type by making use of both return values of the type assertion: the underlying value and a boolean value that reports whether the assertion succeeded.
For example:

```go
str, ok := thing.(string) // no panic if thing is not a string
```

If `thing` holds a `string`, then `str` will be the underlying value and `ok` will be true.
If `thing` does not hold a `string`, then `str` will be the zero value of type `string` (ie. `""` - the empty string) and `ok` will be false.
No panic occurs in any case.

## Type Switches

A **type switch** can perform several type assertions in series.
It has the same syntax as a type assertion (`interfaceVariable.(concreteType)`), but the `concreteType` is replaced with the keyword `type`.
Here is an example:

```go
var thing interface{} = 12 // try: 12.3, true, int64(12), []int{}, map[string]int{}

switch v := thing.(type) {
case int:
    fmt.Printf("the integer %d\n", v)
case string:
    fmt.Printf("the string %q\n", v)
default:
    fmt.Printf("type, %T, not handled explicitly: %#v\n", v, v)
}
```
