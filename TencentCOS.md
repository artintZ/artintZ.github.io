# 腾讯云 COS 图床 + VSCode 插件一键获取外链

## 一、概述

我们知道博客文章经常需要插入一些图片，若是插入本地图片，在图片删除后文章也就无法显示该图片了，所以免费稳定的图床和获取外链的快捷工具显得尤为重要。之所以选择腾讯云对象存储 COS 来作为图床，是因为在 VSCode 上有个插件`vscode-upload-tencentCOS`，当然还有七牛云和阿里云的插件，但是该插件有如下几个优点：

- 相比于七牛图床，COS 的域名不会过期。在七牛云你需要绑定自己的域名并且域名要备案，否则使用临时域名一个月后会过期失效。

- 相比于阿里云的 OSS，COS 是有免费空间额度的，足够一般写博客使用。

使用这个插件可以很方便的上传本地或在线图片到 COS 并自动返回图片外链到 md 文档。

## 二、腾讯云注册

注册很简单，就不多说了。官网：[腾讯云](https://cloud.tencent.com/)

## 三、新建存储桶

在`云产品>存储>对象存储`中新建一个存储桶，其中权限要选`公有读私有写`，如下图：

![新建存储桶](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/新建存储桶-f843e1a9-1e15-4783-afa2-607016f3b468.png)

存储桶的`名称`和`所属地域`要记录一下，也可在基本设置中查看

![存储桶信息-c4f3acee-0918-4bc3-bd28-c8527c2b93e9](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/存储桶信息-c4f3acee-0918-4bc3-bd28-c8527c2b93e9.png)

## 四、创建子用户

1. 在`对象存储`中点`密钥管理`，前往`云 API 密钥`页面，会收到提示新建子用户（图示因为我已经建立了子用户），为了安全性考虑创建子用户
![新建子用户](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/新建子用户-dc82325b-205a-4068-a7bd-dfabff0e22fc.png)

2. 接着依次选择`子用户>自定义创建`，完善用户信息，其中`编程访问`要打勾
![子用户信息-1c7bd14e-2f1e-45a0-9103-aa7d065fbfcd](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/子用户信息-1c7bd14e-2f1e-45a0-9103-aa7d065fbfcd.png)

3. 接着设置用户权限，在搜索框中搜索 COS，找到`对象存储（COS）全读写访问权限`选中，然后下一步
![子用户策略-efa1c36c-fabb-48fe-a53b-e086f00f974e](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/子用户策略-efa1c36c-fabb-48fe-a53b-e086f00f974e.png)

4. 点完成后就创建成功了，务必记录下 secret id 和secret key，配置插件时要用到
![子用户密钥-fe0a6f7e-e322-4395-b07a-05fa6a6bbec2](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/子用户密钥-fe0a6f7e-e322-4395-b07a-05fa6a6bbec2.png)

## 五、`vscode-upload-tencentCOS`插件配置

在 VSCode 插件商店中安装该插件并重新加载，打开设置(`文件>首选项>设置`)，搜索tencentcos，根据前文提到的信息填写完整即可

![插件配置-c2382391-784d-4489-81db-67d93bfabaa5](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/插件配置-c2382391-784d-4489-81db-67d93bfabaa5.png)

## 六、`vscode-upload-tencentCOS`使用方法

- 在 markdown 文档中，将光标放在需要插入图片的位置，按快捷键`Alt + Y`，在弹出的命令框中粘贴图片的绝对路径/相对路径，或者在线地址，然后回车键即可；
- 或者按快捷键`Alt + U`直接选择本地图片。

## 七、结语

使用此插件在VScode上写博客文章简直不要太方便！但是这个插件作者开发了没多久，很多地方并不完善，比如我这种小白在使用这个插件的时候就走了很多弯路，研究了好久。希望完善用户配置说明及使用方法，添加拦截剪切板图片的功能，还有上传cos图片的命名规则等。

附插件作者GitHub地址：[https://github.com/Sean10/vscode-upload-tencentCOS](https://github.com/Sean10/vscode-upload-tencentCOS)