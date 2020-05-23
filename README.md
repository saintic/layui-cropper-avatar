# layui-cropper-avatar

Layui头像裁剪组件

## 说明

这是一款适用于Layui的[微改整合]第三方组件，仅实现图片裁剪功能，基于[cropper 3.1.3](https://github.com/fengyuanchen/cropper)。

社区组件平台已经有一个[cropper 图片截取（剪裁）上传组件](https://fly.layui.com/extend/croppers/)，可惜我测试中有点问题并不如意，所以就把之前用的[jquery插件](http://www.jq22.com/jquery-info18167)改成layui组件，两者很相像，毕竟都是基于cropper.js(一个3.0.0，一个3.1.3)。

## 使用

使用`git clone`、`svn checkout`或直接下载压缩包等方式获取仓库代码，将static中的css和mod的js模块复制到你的项目相关目录。

代码目录结构：

```
├── index.html
└── static
    ├── css
    │   ├── ImgCropping.css //avatar裁剪框样式
    │   └── cropper.min.css //cropper样式
    └── mod
        ├── avatar.js    //依赖cropper模块
        └── cropper.js   //cropper封装的layui模块
```

模块使用(请先阅读[Layui文档](https://www.layui.com/doc/)对其模块化有一定了解)：

```
layui.config({
    base: '/static/mod/' //mod所在目录
}).use('avatar', function () {
    var avatar = layui.avatar;
    avatar.render({
        success: function (base64, size) {
            console.log(base64);
            console.log(size);
            //ajax upload
        }
    });
});
```

----

avatar模块定义了两个函数：render、base64ToBlob

请用render初始化，base64ToBlob用来把base64图片转为二进制，基本是用不到。

render函数接收object对象完成一些参数设置：

- elem {string}

  绑定上传元素的ID，点击弹出图片裁剪框，默认是 **#uploadAvatar** ，所以可以放置一个按钮，设置id=uploadAvatar。

- imgWidth {Number}

  裁剪图片的宽度（像素）

- success {Function}

  用户点击 **确认裁剪并上传头像** 按钮的回调，但注意avatar本身不上传，所以需要在success中上传。
  
  success传递两个参数：裁剪后的图片的base64(image/png)、base64的大小（单位Kb）

## Demo

index.html是示例，不能直接运行它，用nginx或者python启动一个web服务：

```
python2 -m SimpleHTTPServer 5000
```

访问`127.0.0.1:5000`效果大概是这样的：

![](https://static.saintic.com/picbed/staugur/2020/05/24/1590253806414.png)

### ps

如果你要更新cropper.js版本，在上面找到其仓库，下载dist中cropper.js(UMD)，参考Layui第三方组件规范改造UMD（$固定为layui.jquery即可）
