### Gemfile管理多版本CocoaPods

#### Q：

多人协同开发同一项目时，每个人电脑上的`CocoaPods` 版本可能不同，这样当某人重新执行`pod install` 操作后，有可能导致其他人打开项目时报错。对于这种问题我们有解决办法吗？

#### A：

有， `Gemfile`可以帮我们以非常简单的方式解决这个问题。

---

#### Gemfile Usage

先贴一下官方链接 [Using a Gemfile](https://guides.cocoapods.org/using/a-gemfile.html) 

##### 大致用法：

1. 进入到工程目录下，调用`bundle init`命令，会创建一个`Gemfile`文件，此操作类似于`pod init`;

2. 编辑刚才创建的`Gemfile`文件，在里面添加`gem "cocoapods", '1.5.0'`，这样就指定了`CocoaPods`的版本了；

3. 最后执行`bundle exec pod update` 或者`bundle exec pod install`命令即可，这样就会使用`Gemfile`内的版本安装了，不受你电脑上的`cocoapods`版本影响，比如你电脑上是`1.5.0`版本的，也可以用`1.4.0`版本的`pod`安装；这里需要说明的一点是，如果你直接调用`pod install` 或者 `pod uodate`，则默认使用的还是你本机上的`cocoapods`版本。

为了方便使用，可以把以上命令封装到一个脚本中：

```shell
#!bin/sh
rm -rf Podfile.lock
rm -rf Pods

bundle install
bundle exec pod update --no-repo-update
```

以上脚本可以根据需要自行修改。
