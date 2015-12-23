[slide]
## ppt 


 * 基于GFM的markdown语法编写
 * 支持[html混排](#mixed-code)，再复杂的demo也可以做！
 * 支持多个皮肤：[colors]()-[moon]()-[blue]()-[dark]()-[green]()-[light]()
 * 实现watch功能`ppt start -w`
 * 支持[20种转场动画](#transition)，可以设置单页动画
 * 支持单页背景图片
 * 多种模式：overview模式，[双屏模式](#postmessage)，[socket远程控制](#socket)，摇一摇换页，使用ipad/iphone控制翻页更酷哦~
 * 可以使用画板，**双屏同步画板**内容！可以使用note做备注
 * 支持语法高亮，自由选择[highlight样式](https://highlightjs.org/)
 * 可以单页ppt内部动画，单步动画
 * [支持进入/退出回调](#callback)，做在线demo很方便
 * 支持事件update函数，
 * zoom.js：alt+click
 
 [slide]
 
### 使用举例

#### 示例1：进入页面如果触发翻页事件，就会当前执行做转场，做一些类似magicmove效果
```markdown
[slide data-on-build="globalCallbackName"]
```

```javascript
var count = 0;
function globalCallbackName(e){
    count++;
    if(count<2){
        //做一些页面动效，或者转场
        e.stop();//阻止默认事件，就不会跳转
    }
}
```


[slide]

#### 示例2：代理空格按键事件
```markdown
[slide data-on-keypress="globalCallbackName"]
```

```javascript
function globalCallbackName(e){
    if(e.keyCode==32){
        //play();//触发自定义的页面效果
        e.stop();//阻止默认事件，则不会触发ppt默认绑定的事件
    }
}
```


[slide]

## 安装

```bash
npm install -g plppt
```

## shell使用

### 启动

```bash
# 获取帮助
ppt start -h
# 绑定端口
ppt start -p <port>
```

```bash
ppt start -p 8090 -d path/for/ppts
# 绑定host，默认绑定0.0.0.0
ppt start -p 8080 -d path/for/ppts -H 127.0.0.1
# 使用socket通信（按Q键显示/关闭二维码，手机扫描，即可控制）
# socket须知：1、注意手机和pc要可以相互访问，2、防火墙，3、ip
```

[slide]

#### 启用socket控制

##### 方法一：使用url参数

```bash
http://127.0.0.1:8080/md/demo.md?controller=socket
```

在页面按键【Q】显示控制url的二维码和控制链接（需要隐身窗口打开），手机上可以使用左右touch滑动和摇一摇切换下一页

##### 方法二：使用`start`命令行

```bash
ppt start -c socket
```
在页面按键【Q】显示控制url的二维码和控制链接（需要隐身窗口打开），手机上可以使用左右touch滑动和摇一摇切换下一页

#### 启用postMessage控制
默认使用postMessage多窗口控制，打开方法：

```bash
http://127.0.0.1:8080/md/demo.md?_multiscreen=1

```



[slide]
#### 导处html

```bash
# 获取generate帮助
ppt generate -h
# 使用generate命令
ppt generate filepath
# 导出全部，包括ppt的js、img和css文件夹
# 默认导出在publish文件夹
ppt generate ./ppts/demo.md -a
# 指定导出文件夹
ppt generate ./ppts/demo.md output/path -a
```
导出目录下所有ppt，并且生成ppt list首页：

```bash
ppt path output/path -a
```



#### 单页ppt上下布局
```markdown
[slide]
## 主页面样式
### ----是上下分界线
----
ppt 是基于nodejs写的支持 **Markdown!** 语法的网页PPT

```


