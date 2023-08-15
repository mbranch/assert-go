# assert-go

[![Go Reference](https://pkg.go.dev/badge/github.com/mbranch/assert-go.svg)](https://pkg.go.dev/github.com/mbranch/assert-go)
[![Go Report Card](https://goreportcard.com/badge/github.com/mbranch/assert-go)](https://goreportcard.com/report/github.com/mbranch/assert-go)

Package assert simplifies writing test assertions[^1].

Output will contain a helpful diff rendered using as well as the source code of
the expression being tested. For example, if you call `assert.Equal(t, car.Name, "Porsche")`, the error message will include "car.Name".

Additional options and custom comparators can be registered using
`RegisterOptions`, or passed in as the last parameter to the function call. For
example, to indicate that unexported fields should be ignored on `MyType`, you
can use:

```go
assert.RegisterOptions(
  cmpopts.IgnoreUnexported(MyType{}),
)
```

See the [go-cmp docs](https://godoc.org/github.com/google/go-cmp/cmp) for more
options.

## Usage

```go
func Test(t *testing.T) {
    message := "foo"
    assert.Equal(t, message, "bar")
    // message (-got +want): {string}:
    //          -: "foo"
    //          +: "bar"

    p := Person{Name: "Alice"}
    assert.Equal(t, p, Person{Name: "Bob"})
    // p (-got +want): {domain_test.Person}.Name:
    //          -: "Alice"
    //          +: "Bob"
}
```

[^1]:
    This repo is a copy (not a fork) of [github.com/deliveroo/assert-go](https://github.com/deliveroo/assert-go) which was
    deleted. It will be maintained separately from the original repo.
