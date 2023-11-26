# Xjar_Decrypt
Xjar解密</br>
1.查找密码</br>
<code>package main

import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	input := bufio.NewScanner(os.Stdin) //初始化一个扫表对象
	for input.Scan() {                  //扫描输入内容
		line := input.Text() //把输入内容转换为字符串
		fmt.Println(line)    //输出到标准输出
	}
}</code>
