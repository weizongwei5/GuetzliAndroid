# GuetzliAndroid


 - [x] 已经导入 libpng libjpeg 依赖并编译通过。
 - [x] 测试压缩png可用。
 - [x] 把一些无法压缩的原因，在日志中显示出来。
 - [x] libgpng代码修改使ndk可以编译出arm64-v8a的包。


如你所见，Guetzli目前处于第一版发布，性能并不好。但是未来它可能会成为一个跨平台的最好的图片压缩工具。

当前库内存消耗都在native内存区，不再JVM堆栈中，所以不用担心OOM，跟android平台使用官方纯JAVA代码的话，一个像素就2/4个字节的高内存压缩方案比起来是高端很多。
无损压缩，超高的压缩比，超轻的文件大小。
对于android平台有些机器app只能申请64M内存的情况下，这个库还是显得尤为重要。



目前我修改的这个库存在的问题：

1.不能压缩BMP，BMP格式比较特殊，请查阅BMP这个格式的文档，这个格式肯定不可被压缩。以后也不会被压缩。

2.部分图片因为色彩，或者不遵守规范等等其他原因，无法压缩，经过测试在官方发布的打包好的x64的版本也无法被压缩。

3.压缩耗时太长了，这个问题，我经过测试，我拿官方代码不做修改，直接在树莓派这个arm64机器上编译运行测试，结果一样的，耗时也很久，大图一般都要3分钟以上。


综上，目前跑我这个代码遇到的一些问题，不是我改出来的，官方代码同样存在的。
所以，如果您遇到类似问题不要急着提issues，先build一下官方的版本。


## 期待
谷歌既然发布了1.0版本，后面肯定会修复杂七杂八的问题，我们期待，未来，这个库可以很低的出错率，那么就会很好的移植到移动平台。


[https://github.com/google/guetzli/releases](https://github.com/google/guetzli/releases)



## 性能和内存问题的折中方案

Guetzli的设计是不考虑CPU性能,尽可能得保证图片的高压和高质，所以：它更适合放在一个服务器上。
如果你非要放到移动端：推荐我的另外一个仓库：[OperatingImageBypassDalvik](https://github.com/weizongwei5/OperatingImageBypassDalvik)，这个库会同时顾及OOM问题和CPU耗时问题。