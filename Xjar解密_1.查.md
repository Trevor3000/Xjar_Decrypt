Xjar解密
1.查找密码
利用下边的go代码编译出一个查找密码的文件

```
package main

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
}
```

go build decrypt.go

执行如下命令

```
./xjar ./decrypt java -jar xxxxx.jar
```

会得到加密方式，偏移地址，加密密码

```
AES/CBC/PKCS5Padding
128
128
password
```

2.编译解密程序
代码如下：HelloWorld.java

```
import io.xjar.XKit;
import io.xjar.key.XKey;
import io.xjar.jar.XJar;

public class HelloWorld{
  public static void main(String[] args)
    {
        if (args.length < 2) {
            return;
        }
        String password = "这里是上一步得到的密码";
        try {
            XKey xKey = XKit.key(password);
            try {
                XJar.decrypt(args[0], args[1], xKey);
            } catch(Exception e) {}
        } catch(Exception e) {}

    }
}
```

编译程序命令如下：

```
javac -cp ./commons-compress-1.25.0.jar:./xjar-4.0.2.jar:. HelloWorld.java
```

3.解密原jar包
命令如下：

```
java -cp ./xjar-4.0.2.jar:./commons-compress-1.25.0.jar:. HelloWorld 原文件.jar 解密后文件.jar
```
