---
title:      "vscode 插入时间"
cover:      "https://image.123m.me/images/2019/02/02/d4f7844b53674b9f9380b3c3a1d3a933.md.png"
date:       "2019-02-01 14:14:37"
tags:       
    - 开发工具
---


##### 在vscode中插入时间

1. 安装insert date string扩展
2. 使用:  
⇧+⌘+I (OS X) 或者 Ctrl+Shift+I (Windows and Linux).  
3. 配置:  
在用户设置中搜索"insertDateString.format": "YYYY-MM-DD hh:mm:ss"进行更改,还可以插入时间戳,只是没有分配快捷键,需要手动在快捷键管理页面进行设置.  
4. 在snippet中使用:  
```json
{
    "File header": {
        "prefix": "header",
        "body": [
            "title: ${title:Enter title}",
            "date: ${date:Insert datetime string (⇧⌘I or Ctrl+Shift+I)}"
        ]
    }
}
```

摘选自[stackoverflow](https://stackoverflow.com/questions/38780057/how-to-insert-current-date-time-in-vscode)及[vscode](https://marketplace.visualstudio.com/items?itemName=jsynowiec.vscode-insertdatestring).