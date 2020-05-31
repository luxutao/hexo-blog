---
title:      "开发vscode插件"
cover:      "https://image.animekid.cn/images/2019/02/02/8d39e9ffb596153d4ae879af3e786d69.md.png"
date:       "2019-02-21 16:39:51"
tags:
    - 开发工具
---

#### 安装Yeoman 和 VS Code Extension Generator  
默认为已安装node.js和git(具体怎么安装请自行百度)
```bash
npm install -g yo generator-code
```
#### 生成一个新项目  
执行下列命令
```bash
bashyo code

# ? What type of extension do you want to create? New Extension (TypeScript)
# ? What's the name of your extension? HelloWorld
### Press <Enter> to choose default for all options below ###

# ? What's the identifier of your extension? helloworld
# ? What's the description of your extension? LEAVE BLANK
# ? Enable stricter TypeScript checking in 'tsconfig.json'? Yes
# ? Setup linting using 'tslint'? Yes
# ? Initialize a git repository? Yes
# ? Which package manager to use? npm

code ./helloworld

```
#### 生成的文件树  
这是生成项目后的文件目录结构
```bash
├── .vscode
│   ├── launch.json     // Config for launching and debugging the extension
│   └── tasks.json      // Config for build task that compiles TypeScript
├── .gitignore          // Ignore build output and node_modules
├── README.md           // Readable description of your extension's functionality
├── src
│   └── extension.ts    // Extension source code
├── package.json        // Extension manifest
├── tsconfig.json       // TypeScript configuration
```
#### 安装axios模块  
这个模块可以访问外部的接口，类似于jq的ajax
```bash
npm install axios
```
#### 在src目录中编写一个新的文件  
这个新的文件就是我们的主要文件，比如起名为 `getdata.ts`
```json
**这个是接口返回的数据格式**
{
    code: 200,
    msg: "success",
    data: {
        image_height: 1080,
        image_size: 110855,
        image_name: "42379afe80ac6aaafc55447ec2ddb5af",
        image_date: "2019-02-02 20:18:08",
        image_likes: 0,
        image_width: 1920,
        image_extension: "jpg",
        image_id: 435,
        image_date_gmt: "2019-02-02 12:18:08",
        image_album_id: 8,
        image_source: "https://image.demo.com/images/42379afe80ac6aaafc55447ec2ddb5af.jpg"
    },
}
```
```typescript
import { window } from 'vscode'; //引入vscode的window模块
import axios from 'axios'; //引入axios模块
// 获取数据
class GetApiData {
    /**
     * 获取imageurl
     */
    private getApiData() {
        //使用get方法
        axios.get(this.config.url)
        .then((response) => {
            if (response.data.code == 200) {
                // 调用写入函数，将得到的值写到编辑器里
                this.replaceEditorSelection(response.data.data.image_source);
            } else {
                // 如果发生错误，则显示右下角的消息提示
                window.showInformationMessage("发生意外错误，请查看接口访问状态.");
                return;
            }
        }).catch((error) => { 
            window.showInformationMessage(error);
            return;
        });
    }


    /**
     * 写入编辑器
     * @param text string
     */
    private replaceEditorSelection(text: string) {
        // 调用编辑器，这里遇到一个问题，当时没有判断editor这个变量，导致在vscode里一直提示对象是未定义的，然后没法进行打包，这个编辑器的值有或未定义的参数，所以加了一个判断
        const editor = window.activeTextEditor;
        if (editor) {
            const selections = editor.selections;
          
            editor.edit((editBuilder) => {
              selections.forEach((selection) => {
                editBuilder.replace(selection, '');
                editBuilder.insert(selection.active, text);
              });
            });
        }
    }

    // new一个默认的对象
    export default new GetApiData();
}
```
#### 注册命令  
修改`extension.ts`，注册一个新的命令(直接复制helloworld的就行)
```typescript
import apidata from './getdata'; // 顶部添加引入
let api = vscode.commands.registerCommand('extension.getApiData', () => {
    // The code you place here will be executed every time your command is executed

    // Display a message box to the user
    apidata.getApiData();
});

context.subscriptions.push(api);
```
#### 快捷键的绑定  
修改`package.json`，添加命令的键绑定
```json
"contributes": {
    "commands": [
        {
            "command": "extension.getApiData",
            "title": "Insert API data"
        }
    ],
    "keybindings": [
        {
            "command": "extension.getApiData",
            "key": "ctrl+p ctrl+i",
            "mac": "cmd+p cmd+i",
            "when": "editorTextFocus"
        }
    ]
},
```
F5启动调试，会另外打开一个vscode窗口，直接在窗口输入快捷键即可自动将内容插入。  
#### 打包扩展
**安装打包模块**
```bash
npm install -g vsce
```
**打包成vsix**
```bash
cd myExtension
vsce package
# myExtension.vsix generated
```
至于发布扩展，因为我觉得太麻烦，还要注册账号，所以放弃了，如果你们需要可以访问 [Publishing Extension | Visual Studio Code Extension API](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)