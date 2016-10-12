###go生成随机数
```
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func randGenerator() chan int {
	out := make(chan int)
	go func() {
		for {
			rand.Seed(time.Now().Unix())
			out <- rand.Intn(100)
		}
	}()
	return out
}

func main() {
	randServiceHandler := randGenerator()
	fmt.Printf("%d\n", <-randServiceHandler)
}
```