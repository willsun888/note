## 系统剪贴板
### 查看是否支持clipboard：

```
vim --version | grep clipboard
-clipboard       +job             +path_extra      -toolbar
+ex_extra        -mouse_gpm       -sun_workshop    -xterm_clipboard
```
clipboard前面有一个小小的减号，说明不支持。

mac安装：brew install vim

### 使用系统剪贴板
"*y或"+y
:reg // 查看寄存器

## 移动

单词移动

```
W w            移动到下一个单词开头
E e            移动到下一个单词结尾
B b            倒退到上一个单词开头
1.E会忽略标点符号，如：I‘m，e会当成两个单词，E则不会
2.在命令前加上数字代表执行次数，如：2w，表示往下移动2个单词
```

滚屏

```
Ctrl+f            往前滚动一整屏
Ctrl+b            往后滚动一整屏
Ctrl+d            往前滚动半屏
Ctrl+u            往后滚动半屏
```

## 插件
### vimium
vimium chrome的vim插件
快捷键：
shift+tab：选择输入框
