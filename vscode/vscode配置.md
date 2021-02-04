```
{
	//是否显示缩略图
    "editor.minimap.enabled": false,
    //代码缩进
    "editor.tabSize": 4,
    //保存时修复错误
    "eslint.autoFixOnSave": true,
    //粘贴时格式化
    "editor.formatOnPaste": true,
    //自动换行
    "editor.wordWrap": "wordWrapColumn",
    //每行120字符自动换行
    "editor.wordWrapColumn": 120,
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    //检测空格还是制表符
    "editor.detectIndentation": false,
    //渲染控制字符？
    "editor.renderControlCharacters": true,
    //是否显示面包屑
    "breadcrumbs.enabled": true,
    //js每句结束自动加分号；
    "prettier.semi": true,
    // 缩进字节数
    "prettier.tabWidth": 4,
    // 使用单引号代替双引号
    "prettier.singleQuote": true,
    // 在对象，数组括号与文字之间加空格 "{ foo: bar }"
    "prettier.bracketSpacing": false,
    // 超过最大值换行
    "prettier.printWidth": 120,
    // 因为使用了一些折行敏感型的渲染器（如GitHub comment）而按照markdown文本样式进行折行
    "prettier.proseWrap": "always",
    //eslint验证
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        {
            "language": "html",
            "autoFix": true
        },
        {"language": "vue", "autoFix": true}
    ],
    "eslint.options": {
        "plugins": ["html"]
    },
    "vetur.format.defaultFormatterOptions": {
        "prettier": {
            "singleQuote": true,
            "semi": true,
            "printWidth": 120,
            "proseWrap": "always"
        }
    },
    "[jsonc]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "vetur.format.options.tabSize": 4,
    "diffEditor.ignoreTrimWhitespace": false,
    //字体大小
    "editor.fontSize": 16,
    //文件头插件设置
    "fileheader.configObj": {
        "createFileTime": true,
        "language": {
            "languagetest": {
                "head": "/$$",
                "middle": " $ @",
                "end": " $/"
            }
        },
        "autoAdd": false,
        "autoAlready": true,
        "annotationStr": {
            "head": "/*",
            "middle": " * @",
            "end": " */",
            "use": false
        },
        "headInsertLine": {
            "php": 2
        },
        "beforeAnnotation": {},
        "afterAnnotation": {},
        "specialOptions": {},
        "switch": {
            "newlineAddAnnotation": true
        },
        "config": {
            "dateFormat": "YYYY-MM-DD HH:mm:ss",
            "prohibitAutoAdd": ["json"],
            "moveCursor": true
        }
    },
    "fileheader.cursorMode":{//函数注释配置（需手动配置快捷键，可参考插件文档）
        "description": "",//函数功能描述
        "@param {type}" :""//参数描述
    },
    "fileheader.customMade": {//文件头注释配置（需手动配置快捷键，可参考插件文档）
        "Author": "myname",//作者名
        "Date": "Do not edit",//当前编辑日期，默认生成
        "LastEditors": "Do not edit",//上个编辑作者（当上个编辑作者下载korofileheader插件时可自动更新），默认生成
        "LastEditTime": "Do not edit"//上次编辑事件，默认生成
    },
    "terminal.integrated.copyOnSelection": true,
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe",
    "editor.formatOnSave": true//保存时自动格式化
}
```

## prettier格式化规则：

```
{
    // 使能每一种语言默认格式化规则
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[css]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[less]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    
    /*  prettier的配置 */
    "prettier.printWidth": 100, // 超过最大值换行
    "prettier.tabWidth": 4, // 缩进字节数
    "prettier.useTabs": false, // 缩进不使用tab，使用空格
    "prettier.semi": true, // 句尾添加分号
    "prettier.singleQuote": true, // 使用单引号代替双引号
    "prettier.proseWrap": "preserve", // 默认值。因为使用了一些折行敏感型的渲染器（如GitHub comment）而按照markdown文本样式进行折行
    "prettier.arrowParens": "avoid", //  (x) => {} 箭头函数参数只有一个时是否要有小括号。avoid：省略括号
    "prettier.bracketSpacing": true, // 在对象，数组括号与文字之间加空格 "{ foo: bar }"
    "prettier.disableLanguages": ["vue"], // 不格式化vue文件，vue文件的格式化单独设置
    "prettier.endOfLine": "auto", // 结尾是 \n \r \n\r auto
    "prettier.eslintIntegration": false, //不让prettier使用eslint的代码格式进行校验
    "prettier.htmlWhitespaceSensitivity": "ignore",
    "prettier.ignorePath": ".prettierignore", // 不使用prettier格式化的文件填写在项目的.prettierignore文件中
    "prettier.jsxBracketSameLine": false, // 在jsx中把'>' 是否单独放一行
    "prettier.jsxSingleQuote": false, // 在jsx中使用单引号代替双引号
    "prettier.parser": "babylon", // 格式化的解析器，默认是babylon
    "prettier.requireConfig": false, // Require a 'prettierconfig' to format prettier
    "prettier.stylelintIntegration": false, //不让prettier使用stylelint的代码格式进行校验
    "prettier.trailingComma": "es5", // 在对象或数组最后一个元素后面是否加逗号（在ES5中加尾逗号）
    "prettier.tslintIntegration": false // 不让prettier使用tslint的代码格式进行校验
}

```

### 另一种配置

```
{
  "window.zoomLevel": 0, // 调整窗口的缩放级别
  "search.followSymlinks": false, // 关闭rg.exe进程 用cnpm导致会出现rg.exe占用内存很高
  "workbench.settings.openDefaultSettings": true, // 总是默认打开settings.json文件
  "javascript.updateImportsOnFileMove.enabled": "always", // import路径移动或者重命名时
  /////////// 注释配置 以下包含两种插件 自行搜索//////////
  "fileheader.Author": "xxx",
  "fileheader.LastModifiedBy": "xxx",
  "fileheader.customMade": {
    "Description": "In User Settings Edit",
    "Author": "xxx",
    "Date": "Do not edit",
    "LastEditors": "xxx",
    "LastEditTime": "Do not edit"
  },
  /////////// vscode配置 //////////
  "editor.tabSize": 2, // 缩进字符
  "editor.formatOnSave": true, // 自动保存格式化
  "editor.renderWhitespace": "boundary", // 缩进空白样式 
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[vue]": {
    "editor.defaultFormatter": "octref.vetur"
  },
  /////////// prettier单独配置 //////////
  "prettier.printWidth": 70, // 超过最大值换行
  "prettier.tabWidth": 2, // 缩进字节数
  "prettier.useTabs": false, // 缩进使用tab
  "prettier.semi": false, // 句尾添加分号
  "prettier.singleQuote": true, // 使用单引号代替双引号
  "prettier.proseWrap": "preserve", // 默认值。因为使用了一些折行敏感型的渲染器（如GitHub comment）而按照markdown文本样式进行折行
  "prettier.arrowParens": "avoid", //  (x) => {} 箭头函数参数只有一个时是否要有小括号。avoid：省略括号
  "prettier.bracketSpacing": true, // 在对象，数组括号与文字之间加空格 "{ foo: bar }"
  "prettier.disableLanguages": [
    "vue"
  ], // 不格式化vue文件，vue文件的格式化单独设置 如果装了vetur设置了也不起作用 需要单独对vetur的prettier配置
  "prettier.endOfLine": "auto", // 结尾是 \n \r \n\r auto
  "prettier.htmlWhitespaceSensitivity": "ignore",
  "prettier.ignorePath": ".prettierignore", // 不使用prettier格式化的文件填写在项目的.prettierignore文件中
  "prettier.jsxBracketSameLine": false, // 在jsx中把'>' 是否单独放一行
  "prettier.jsxSingleQuote": false, // 在jsx中使用单引号代替双引号
  ////////// prettier针对于vetur的配置 //////////
  "vetur.format.defaultFormatter.html": "prettier",
  "vetur.format.defaultFormatter.js": "prettier",
  "vetur.format.defaultFormatter.less": "prettier",
  "vetur.format.defaultFormatterOptions": {
    "prettier": {
      "tabWidth": 2,
      "printWidth": 70,
      "semi": false,
      "singleQuote": true,
      "bracketSpacing": true,
      "arrowParens": "avoid"
    }
  },
  ////////// eslint单独配置 //////////
  "eslint.enable": true,
  "eslint.autoFixOnSave": true,
  "eslint.run": "onType",
  "eslint.options": {
    "extensions": [
      ".js",
      ".vue"
    ]
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "vue",
      "autoFix": true
    },
    "html",
    {
      "language": "html",
      "autoFix": true
    },
    "css",
    {
      "language": "css",
      "autoFix": true
    }
  ],
  "workbench.colorTheme": "One Dark Pro",
  "workbench.iconTheme": "material-icon-theme"
}
```

## 另外一种配置

```
{
 2  "window.zoomLevel": 1,
 3  "git.ignoreMissingGitWarning": true, // 忽略“缺失git”的警告
 4  "files.autoSave": "onFocusChange", // 离开页面自动保存
 5  "workbench.colorTheme": "Default Light+", // 配色
 6  "editor.tabSize": 2, // 缩进，tab格数
 7  "editor.fontSize": 14, // 字号
 8  // 文本头
 9  "fileheader.Author": "@Guojufeng",
10  "fileheader.LastModifiedBy": "@Guojufeng",
11  // 快捷浏览html页面
12  "view-in-browser.customBrowser": "chrome",
13  "open-in-browser.default": "chrome",
14  "explorer.confirmDragAndDrop": false,
15  "files.associations": {
16    "*.cjson": "jsonc",
17    "*.wxss": "css",
18    "*.wxs": "javascript"
19  },
20  "minapp-vscode.disableAutoConfig": true,
21  // 显示编辑时的控制字符（markdown中删除不干净出现的“s”）
22  "editor.renderControlCharacters": true,
23  "explorer.confirmDelete": false,
24  "git.confirmSync": false,
25  "git.autofetch": true,
26  "git.enableSmartCommit": true,
27  "python.jediEnabled": false,
28  "breadcrumbs.enabled": true,
29  // 每次保存的时候自动格式化
30  // "editor.formatOnType": true,
31  "editor.formatOnSave": true,
32  // 在保存时运行的代码操作类型。
33  "editor.codeActionsOnSave": {
34    "source.fixAll.eslint": true
35  },
36  // 自动美化
37  "beautify.language": {
38    "js": {
39      "type": ["javascript", "json"],
40      "filename": [".eslintrc", ".jsbeautify"]
41    },
42    "css": ["css", "scss"],
43    "html": ["htm", "html", "vue"]
44  },
45  // 去掉代码结尾的分号
46  "prettier.semi": false,
47  // 单引号，而不是双引号
48  "prettier.jsxSingleQuote": true,
49  "prettier.singleQuote": true,
50  // prettier使用eslint格式校验
51  "prettier.eslintIntegration": true,
52  // #让函数(名)和后面的括号之间加个空格
53  "typescript.format.insertSpaceBeforeFunctionParenthesis": true,
54  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
55  // 每次保存的时候将代码按eslint格式进行修复
56  "eslint.autoFixOnSave": true,
57  // eslint添加 vue 支持
58  "eslint.validate": [
59    "javascript",
60    "javascriptreact",
61    {
62      "language": "html",
63      "autoFix": true
64    },
65    {
66      "language": "vue",
67      "autoFix": true
68    }
69  ],
70  // jsx中使用emmet自动补全代码
71  "emmet.triggerExpansionOnTab": true,
72  // 扩展emmet的支持
73  "emmet.includeLanguages": {
74    "wxml": "html",
75    "javascript": "javascriptreact"
76  },
77  // 让vue中的js按编辑器自带的ts格式进行格式化
78  // "vetur.format.defaultFormatter.js": "prettier",
79  "vetur.format.defaultFormatter.js": "vscode-typescript",
80  "vetur.format.defaultFormatterOptions": {
81    "js-beautify-html": {
82      "wrap_attributes": "force-aligned"
83    },
84    // vue文件转换单引号、去掉分号
85    "prettier": {
86      "semi": false,
87      "singleQuote": true
88    }
89  }
90}
```

