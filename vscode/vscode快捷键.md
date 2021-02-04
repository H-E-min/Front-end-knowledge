## 一、编辑器使用

### 显示命令面板

```
Ctrl + Shift + P或者F1
```

### 快捷键列表查看「View Shortcut」

```
Ctrl + K，再按Ctrl + S
```

### 快速打开文件「Quick open」

```
ctrl + p
```

> 🌟小技巧
>
> - 输入`?`可以查看帮助文档
> - 如果想打开多个文件有两种方法：
>   - 打开新文件 `Alt` + `→`
>   - 多窗口打开`Ctrl` + `→`

### 编辑器命令「Command Palette」

```
ctrl + p 
// 在搜索加上 >前缀 就可以调用命令了。
```

### **拆分编辑器

```
ctrl + \

//拆分2个，3个……
ctrl + 2 
ctrl + 3
ctrl + ……
```

### 编辑器网格布局「Editor Grid Layout」

首先我们需要创建空的编辑器组：打开方式`查看（view）` > `编辑器布局（editor Layout）` > `2x2 网格(Grid 2x2)`

### 快速打开和关闭侧边栏「Opening and Closing the Sidebar」

```
Ctrl + B
```

### 快速打开集成终端「Open new Terminal」

```
ctrl + `
```

### 重新打开软件窗口

```
Ctrl + Shift + N
```

### 关闭当前打开的窗口

```
ctrl + shift + w
```

## 新建文件

```
ctrl + n
```

### 关闭当前文件

```
ctrl + w
```

## 二、辅助代码编写

### 合并行(`editor.action.joinLines`)

```
自定义的快捷键
ctrl + k
```

### 代码格式化

```
Shift + Alt + F
不过更推荐使用Prettier
```

### 清除多余空格

```
Ctrl + K，再按Ctrl + X
```

我们可以在`VSCode`的配置里面设置自动清除。下面教大家两种配置方式。

- 使用settings.json
  1. 打开`编辑器命令`（Mac：`Command`+`P`/Windows：`Ctrl`+`P`）
  2. 在搜索框输入`> Open Settings`，然后选择`首选项：打开设置(json)`
  3. 然后settings.confg中加入`"files.trimTrailingWhitespace": true`，如果已存在这个配置，确保值是`true`。
  4. 保存文件即可生效（如果没有马上生效，可以重启VSCode）

- 使用可视化（UI）设置

  1. 打开`编辑器命令`（Mac：`Command`+`P`/Windows：`Ctrl`+`P`）

  2. 在搜索框输入`> Open Settings`，然后选择`首选项：打开设置(ui)`

  3. 在`文本编辑器`>`文件`中找到`Trim Trailling Whitespace`并且勾上（我们也可以在搜索框直接输入`Trim Trailling Whitespace`快速找到这个配置的位置），可参考下面的截图。

     ![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91c2VyLWdvbGQtY2RuLnhpdHUuaW8vMjAyMC80LzEzLzE3MTZmNWM1NzljMTliZDE?x-oss-process=image/format,png)

### 折叠代码快捷键

```
Ctrl + Shift + [
```

### 展开代码快捷键

```
Ctrl + Shift + ]
```

### 往上/下复制行「Copy Line Up/Down」

```
Shift + Alt + ⬆️ / ⬇️
```

### 选择单词

```
//局部选择
Ctrl + D
//全部选择
Ctrl + Shift + L
```

### 跳转到特定行数「Navigate to a Specific Line」

```
Ctrl + G
也可以使用
Ctrl + P打开编辑器命令 然后输入: 再输入行数即可。
```

### 文件中跳转特定符号「Go to Symbol in File」

`符号`指的是什么，它就是在代码中的`方法`、`类`或者是`属性`

```
Ctrl + Shift + O
```

> 🌟小技巧
>
> 如果文件中的`符号`过多，我们可以在`@`后面加上`:`，就可以为所有符号分类让，我们更好找到需要的符号和位置。

### 项目中跳转特定符号 「Go to Symbol in Workspace」

这个快捷键与文件中跳转的雷同，唯一区别就是这个可以搜索出`整个项目中的方法`、`类`和`属性`，并且快速跳转到这些符号的位置。

```
Ctrl + T
```

### 删除整个单词「Delete Previous Word」

```
Ctrl + Backspace
```

### 按单词选择「Select by words」

```
Ctrl + Shift + ← / →
```

### 快速复制当前行「Duplicate Line」

```
shift + alt + ↓ / ↑
```

### 删除一行「Deleting a Line」

```
Ctrl + X
```

### 往上/下添加同时编辑「Add Cursor Above/Below」

```
Ctrl + Alt + ↑ / ↓
```

> 🌟小技巧
>
> 在属性的单词前添加好同时编辑鼠标点后，一下子即跳到所有属性名的最后面，我们只需要先在所有名字前面加入同时编辑鼠标然后用一下快捷键即可：
>
> Windows/Linux: `Ctrl` + `→`
>
> ![img](https://img-blog.csdnimg.cn/20200417224752297.gif#pic_center)

### 多行选中同时编辑 「Column Selection」

```
Shift + Alt + 鼠标操作
```

![img](https://img-blog.csdnimg.cn/20200417230233688.gif)

### 修改“符号” 「Rename Symbol」

`VSCode`默认支持`JavaScript`和`TypeScript`的`方法名`、`类名`和`属性名`等符号修改。在`修改后，文件下引用到这些符号的地方都会被自动的同时修改。`其他语言的支持需要插件。

```
F2
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041723052880.gif)

### 在单词之间移动光标

```
Ctrl + 左右方向键
```

### 将光标定位到当前行的最左侧

```
Fn + ←
```

### 将光标定位到当前行的最右侧

```
Fn + →
```

### **在当前行的下方新增一行，然后跳至该行

```
Ctrl + Enter
```

### 在当前行的上方新增一行，然后跳至该行

```
Ctrl+Shift+Enter
```

### **在连续的多列上，同时出现光标

```
Ctrl + Alt + 上下键	
```

### **在任意位置，同时出现光标

```
Alt + 鼠标点击任意位置
```

### **全局搜索代码

```
Ctrl + Shift +F
```

### 查找某个函数在哪些地方被调用了

在 `a.js` 文件里，选中`foo()`函数（或者将光标放置在`foo()`函数上），然后按住快捷键`「Shift + F12」`，就能看到 `foo()`函数在哪些地方被调用了，比较实用。

### 搜索图讲解

![img](http://img.smyhvae.com/20190415_2052.png)