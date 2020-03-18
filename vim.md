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
## 删除
```
:n1,n2 d			删除n1-n2行(包括n1,n2)行

// 在一行中："$"表示行尾, "^"表示行头
// 在文件中："$"表示末行, "."表示当前行，"%"表示整个文件
: .,$ s/str1/str2/g 	用str2替换正文当前行到末尾所有出现的str1
:1,$ s/str1/str2/g		用str2替换正文中所有出现的str1
:1,$ s/^str1/str2/g 	用str2替换正文中所有出现的,每行以str1开头的字符串
:g/str1/s//str2/g 		功能同上
:%s/str1/str2/g			功能同上
:g/foobar/s/bar/baz/g 	首先搜寻foobar,然后把它变成foobaz
:%s/str1/str2/gc 		替换全文所有符合的单词并让用户确认
:%s/str1/str2/gi 		用str2替换正文中所有出现的str1, 在查找时不区分大小写
:10,20s/^/str/			将第10行至第20行的最前面插入str
:%s/$/str/g				在整个文件每一行的行尾添加str
:0,$d					删除所有内容
:%s/\s\+$//				删除行尾多余的空格, "\s\+$"表示行末($)一个或者多个(\+)空格(\s)
```

有些字符域使用得很频繁，vim为这些字符域提供了预定义域：
```
\d 数字 [0-9]
\D 非数字 [^0-9]
\x 十六进制数字 [0-9a-fA-F]
\X 非十六进制数字 [^0-9a-fA-F]
\s 空白字符 [ ] ( 和 )
\S 非空白字符 [^ ] (非 和 )
\l 小写字母 [a-z]
\L 非小写字母 [^a-z]
\u 大写字母 [A-Z]
\U 非大写字母 [^A-Z]
```

## 重定义命令
```
nnoremap J <C-d>  #将ctrl+d重定义为J
nnoremap K <C-u>  #将ctrl+u重定义为K
```

## 插件
### vimium
vimium chrome的vim插件
快捷键：
shift+tab：选择输入框
