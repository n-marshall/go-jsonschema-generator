go-jsonschema-generator [![Build Status](https://travis-ci.org/mcuadros/go-jsonschema-generator.png?branch=master)](https://travis-ci.org/mcuadros/go-jsonschema-generator) [![GoDoc](http://godoc.org/github.com/mcuadros/go-jsonschema-generator?status.png)](http://godoc.org/github.com/mcuadros/go-jsonschema-generator)
==============================

Basic [json-schema](http://json-schema.org/) generator based on Go types, for easy interchange of Go strcutures across languages.


Installation
------------

The recommended way to install go-jsonschema-generator

```
go get github.com/mcuadros/go-jsonschema-generator
```

Examples
--------

A basic example:

```go
package main

import (
  "fmt"
  "github.com/mcuadros/go-jsonschema-generator"
)

type ExampleBasic struct {
  Foo bool   `json:"foo"`
  Bar string `json:",omitempty"`
  Qux int8
  Baz []string
}

func main() {
  s := &jsonschema.Schema{}
  s.Read(&ExampleBasic{})
  fmt.Println(s)
}
```

```json
{
    "$schema": "http://json-schema.org/schema#",
    "type": "object",
    "properties": {
        "Bar": {
            "type": "string"
        },
        "Baz": {
            "type": "array",
            "items": {
                "type": "string"
            }
        },
        "Qux": {
            "type": "integer"
        },
        "foo": {
            "type": "bool"
        }
    },
    "required": [
        "foo",
        "Qux",
        "Baz"
    ]
}
```

License
-------

MIT, see [LICENSE](LICENSE)
