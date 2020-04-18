# go-snowflake

A Go version of Twitter snowflake ID generator.

## Installation

```
go get github.com/mooncool/go-snowflake
```

## Example

```
package main

import (
	"fmt"
	"sync"

	"github.com/mooncool/go-snowflake"
)

func main() {
	idGen, err := snowflake.NewIDGenerator(1, 2)
	if err != nil {
		panic(err)
	}

	// asynchronized generate
	wg := new(sync.WaitGroup)
	for i := 0; i < 10; i++ {
		wg.Add(1)
		go func() {
			id, _ := idGen.NextID()
			fmt.Println(id, idGen.ExplainID(id))
			wg.Done()
		}()
	}
	wg.Wait()

	// batch generate
	fmt.Println(idGen.NextIDs(6))
}
```
