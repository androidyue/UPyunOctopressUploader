# Upyun_Uploader
An Uploading Tool for Uploading Files to upyun, especially for Octopress

## 安装
```
gem install inifile
gem install upyun
```

## 功能描述
  * 暂时只支持对文件的上传和更新，不含删除和下载功能
  * 尤其适合于Octopress网站

## 使用
### 创建授权信息文件
其中access_key填写内容管理者的用户名，secrect_key填写该管理者的密码
```
[auth]
access_key = ""
secret_key = ""
```
将上述内容保存成文件`.upyun.ini` 放在同步脚本的祖先目录上即可，也可以放在家目录。

举个例子，比如你的同步脚本放在`~/tools/notes/sync_dir/`下，你的配置文件，可以放在`~/`,`~/tools/`以及`~/tools/notes/`。

注意，必要将上述文件放同步脚本目录，以免信息泄露。

### 同步
使用方法如下，很简单，需要传入同步文件夹路径和bucket名称

```java
ruby push2QUpyun.rb dir_to_sync bucket
```

## 实现原理
实现原理很简单，基本如下
  
  * 新文件 直接上传
  * 已存在的文件，如果lastModified没有变化，不上传
  * 已存在的文件，如果lastModified有变化，检测文件内容md5，如果和上一次不同，则上传，否则不上传。

