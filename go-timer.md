###go创建定时器方法
```
package main

import (
	. "fmt"
	"math/rand"
	"time"
)

func main() {
	// 方法一：
	go selfTimer()
	//
	// 方法二：
	rand.Seed(time.Now().Unix())
	timerChan := time.Tick(time.Duration(10)*time.Second)
	for t := range timerChan {
		Println(t)
		Println("10S timer.....")
	}
}

func selfTimer() {
	Println("5S Timer...")
	time.AfterFunc(time.Duration(time.Second*5), func() {
		selfTimer()
	})
}
```

模块实现参考 [链接](http://studygolang.com/articles/3271)