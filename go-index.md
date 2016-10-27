###返回unicode 字符的位置
```
package main

import (
	"fmt"
	"strings"
)

func main() {
	// 返回2
	fmt.Println(Utf8Index("爱中华fbbin", "华"))
}

func Utf8Index(str, substr string) int {
    asciiPos := strings.Index(str, substr)
    if asciiPos == -1 || asciiPos == 0 {
        return asciiPos
    }
    pos := 0
    totalSize := 0
    reader := strings.NewReader(str)
    for _, size, err := reader.ReadRune(); err == nil; _, size, err = reader.ReadRune() {
        totalSize += size
        pos++
        // 匹配到
        if totalSize == asciiPos {
            return pos
        }
    }
    return pos
}
```