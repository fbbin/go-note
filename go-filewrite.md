###go写文件方法
```
package main

import (
	"bufio"
	"fmt"
	"io"
	"io/ioutil"
	"os"
	"strings"
)

func main() {
	// 写文件
	file, err := os.OpenFile("./test.txt", os.O_RDWR|os.O_APPEND, 0666)
	if err != nil {
		file, _ = os.Create("./test.txt")
	}
	// 方法1
	writer := bufio.NewWriter(file)
	str := strings.NewReader("JUST TEST WRITE FILE ONE\n")
	size, err := writer.ReadFrom(str)
	length, err := writer.WriteString("JUST TEST WRITE FILE TWO\n")
	writer.Flush()

	fmt.Println(size, length, err)

	// 方法2
	file.WriteString("fbbin1681")

	// 方法3
	io.WriteString(file, "fbbin1682")

	// 方法4（清空重新写）
	ioutil.WriteFile("t.txt", []byte("fbbin1684"), 0666)

	file.Close()
}

```