###读取文件内容，每次读取一行
```
package main

import (
	"bufio"
	"bytes"
	"fmt"
	"os"
)

func main() {
	// 待读取的文件
	file, _ := os.OpenFile("t.log", os.O_RDONLY, 066)
	read := bufio.NewReader(file)
	
	// 方法1（逐行读取）
	l1, prefix, _ := read.ReadLine()
	fmt.Println(string(l1), prefix)
	l2, prefix, _ := read.ReadLine()
	fmt.Println(string(l2), prefix)
	
	// 方法2（根据换行符逐行读取）
	l3, _ := read.ReadBytes('\n')
	l3 = bytes.TrimRight(l3, "\r\n")
	fmt.Println(string(l3))
	
	// 方法3 （通过Scanner来处理）
	file.Seek(0, os.SEEK_SET)
	sf := bufio.NewScanner(file)
	sf.Split(bufio.ScanLines)
	for sf.Scan() {
		str := sf.Text()
		fmt.Println(str)
	}

	// 方法4(读取整个文件)
	fileInfo, err := ioutil.ReadFile("t.log")
}

```