---
title:      "VsCode中设置golang的自动补全功能"
cover:      "https://image.123m.me/images/2019/02/02/73474c12d8b341d76b9efee6fc2af1dd.png"
date:       "2020-09-15 15:42:03"
tags:
    - vscode
    - go
---

1. 打开vscode扩展管理，安装go扩展。  
2. 新建测试代码。
```golang
package main

import "fmt"

func main() {
	fmt.Print("Hello World")
}

```
3. 运行代码，右下角提示安装gocode等插件，选择`Install All`，不出意外是安装不上的，原因你懂得。  
4. 可以选择去github下载然后放到对应的目录或者使用代理方式下载，这里选择设置代理。
```shell
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.io,direct
```
5. 关闭vscode重新打开，再次点击`Install All`，安装成功，这次就可以使用自动补全和代码提示的功能啦。