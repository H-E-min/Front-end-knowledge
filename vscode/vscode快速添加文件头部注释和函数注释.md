## `vscode`快速添加文件头部注释和函数注释

1. 安装插件并配置

   `vscode`安装`koroFileHeader`插件，`ctrl+shift+p` 搜索setting，然后搜索`FileHeader`点击并且进入setting界面。

   添加以下配置项：

   ```json
   //快速添加文件头部注释和函数注释
       "fileheader.configObj": {
           "createFileTime": true, //设置为true则为文件新建时候作为date，否则注释生成时间为date
           "autoAdd": true, //自动生成注释
           "annotationStr": {
               "head": "/*",
               "middle": " * @",
               "end": " */",
               "use": true //设置自定义注释可用
           },
       },
       "fileheader.cursorMode": {
           "description": "",
           "param ": "",
           "return": ""
       },
       "fileheader.customMade": {
           "Description": "", //文件内容描述
           "Author": "hm", //编辑人
           "Date": "Do not edit", //时间
           "LastEditTime": "Do not edit",
           "LastEditors": "hm",
           "Reference": ""
       },
   ```

   2. 文件头部添加注释快捷键：

      ```
      windows：ctrl+alt+i
      mac：ctrl+cmd+i
      ```

      在光标处添加函数注释快捷键：

      ```
      window：ctrl+alt+t
      mac：ctrl+cmd+t
      ```

      