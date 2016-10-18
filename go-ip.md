###go IP整型与字符串转换
```
package main

import (
	"errors"
	"fmt"
	"strconv"
	"strings"
)

type IP struct {
	ip    string
	intIp int
}

func main() {
	var x *IP = &IP{ip: "192.168.163.184", intIp: 3232277432}
	i, _ := x.toString()
	fmt.Println(i)
}

func (self *IP) toInt() (int, error) {
	ipSplit := strings.Split(self.ip, ".")
	if len(ipSplit) != 4 {
		return 0, errors.New("IP格式错误。")
	}
	var intIp int
	for key, value := range ipSplit {
		i, err := strconv.Atoi(value)
		if err != nil || i > 255 {
			return 0, errors.New("IP格式错误。")
		}
		intIp = intIp | i<<uint((3-key)*8)
	}
	self.intIp = intIp
	return intIp, nil
}

func (self *IP) toString() (string, error) {
	ip4 := self.intIp >> 0 & 255
	ip3 := self.intIp >> 8 & 255
	ip2 := self.intIp >> 16 & 255
	ip1 := self.intIp >> 24 & 255
	if ip1 > 255 || ip2 > 255 || ip3 > 255 || ip4 > 255 {
		return "", errors.New("不是一个整型的IP数据")
	}
	ipstring := fmt.Sprintf("%d.%d.%d.%d", ip1, ip2, ip3, ip4)
	self.ip = ipstring
	return ipstring, nil
}
```