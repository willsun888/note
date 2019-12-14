## 软件
### brew

- brew install xxxx // install xxxx
- brew cask: 
is an extension to brew that allows management of graphical applications through the Cask project.
brew cask install foo 等同于 brew install caskroom/cask/foo
- brew tap: 展示brew安装的repo
- 设置代理：brew是通过curl去下载包的，所以设置curl的代理就可以。在~/.curlrc中添加"proxy =<proxy_host>:<proxy_port>"
- 无更新formula的install：HOMEBREW_NO_AUTO_UPDATE=1 brew install ...



### whistle
[whistle](https://github.com/avwo/whistle/blob/master/README-zh_CN.md)是开源抓包软件，用whistle编写。比起收费的Charles或者在MAC支持不好的fiddler，更倾向于使用whistle

```
1.安装nodejs和whistle

2.安装根证书

3.设置代理(MAC机器)
networksetup -setwebproxy "Wi-fi" 127.0.0.1 8899
networksetup -setsecurewebproxy "Wi-fi" 127.0.0.1 8899
附关闭和查看命令：
networksetup -setwebproxystate "Wi-fi" off
networksetup -setsecurewebproxystate "Wi-fi" off
networksetup -getwebproxy "Wi-fi"
networksetup -getsecurewebproxy "Wi-fi"

4.启动: w2 start，访问http://local.whistlejs.com/
```

### pandoc
将markdown转为pdf

```
brew install pandoc
brea install pdflatex
pandoc xx.md -o xx.html
然后使用浏览器打开xx.html，另存为PDF
```

### mysql
```
brew install mysql
// 安装后，配置在/usr/local/etc/my.cnf

// 启动mysql
mysql.server start

// 执行如下命令，登录mysql。默认没有密码
mysql -uroot -p

// 设置密码
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('root');

```

### sublime text
**1. Preferences > Key Bindings -> User**

 ```
 	{ "keys": ["super+alt+o"], "command": "open_dir", "args": {"dir": "$file_path", "file":"$file_name"}},
	{ "keys": ["super+right"], "command": "next_view" },
	{ "keys": ["super+left"], "command": "prev_view" },

	// 设置vim方式操作目录树(sidebar)
    { "keys": ["h"], "command": "move", "args": {"by": "characters", "forward": false}, "context":
    [ {"key": "control", "operand": "sidebar_tree"} ] },
{ "keys": ["j"], "command": "move", "args": {"by": "lines", "forward": true}, "context":
    [ {"key": "control", "operand": "sidebar_tree"} ] },
{ "keys": ["k"], "command": "move", "args": {"by": "lines", "forward": false}, "context":
    [ {"key": "control", "operand": "sidebar_tree"} ] },
{ "keys": ["l"], "command": "move", "args": {"by": "characters", "forward": true}, "context":
    [ {"key": "control", "operand": "sidebar_tree"} ] }
 ```
 
 **2. Preferences > Settings -> User**
 
 ```
 {
    "update_check":false,
	"debug": true,
	"font_size": 16,
	"ignored_packages":
	[
	],
	"tab_completion": false,
	"theme": "Default.sublime-theme",
	"tab_size":4,
	"translate_tabs_to_spaces":true,
	"word_wrap": "true",
}
 ```

**3. Sublime启动卡死**

```
删除如下目录的内容：
/Users/[HOME]/Library/Application Support/Sublime Text 3/Local
```

**4. 安装sublimerge**

```
参考：https://www.sublimerge.com/sm3/docs/quick-start.html#installation

1. Download Package: Sublimerge 3.sublime-package
2. Go to Preferences > Browse Packages...
3. Go one folder up
4. Go to Installed Packages
5. Copy the package to that directory
6. Restart Sublime Text
```

### graphviz
```
brew install graphviz
```

### 其他软件
- [tomighty](http://tomighty.org/)：番茄时钟
- pandoc: markdown文件格式处理工具

## 键盘
1.去除caplock的延迟生效

```
系统设置->键盘->输入法->使用中英键切换ABC输入模式
```

## 文件夹
1.复制文件完整的路径

```
鼠标右键点击文件，会出现菜单。然后点击option，"拷贝xxx"会变为"将xxx拷贝为路径名称"
```

2.terminal到finder切换

```
输入: open . 就可以了
```