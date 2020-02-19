# vvtoolbox gui series

本软件是一款用于m3u8下载（支持AES解密、优酷普通DRM解密）、视频解析（后续增加）的工具，同时集成部分有关于vvtoolbox相关的功能，如下载视频弹幕（后续...）等。
![主界面截图](http://puui.qpic.cn/vshpic/0/qSVJ3paiJ1JDeLJ5z5oPysIIVz_k6HBtTDryZe-bgkepe3eV_0/0)

# 使用方式

## 相关输入框/选项说明

1. m3u8输入框。在这里支持粘贴/输入m3u8地址、拖入m3u8文件。
2. 输出文件名。最终合并输出的文件名，不含后缀，关于后缀可以在config/vvt.json中进行设定，包括音频、视频的后缀。
3. AES解密。依次是AES解密的key，iv/nonce，tag，解密模式，key长度。ECB模式不需要iv，常见的加密m3u8中的AES-128指CBC模式，key长度16字节，一般没有iv。对于优酷，填入key即可。不需要解密的请一定不要填入任何东西。
4. BASEURL。有的m3u8只有分段名，没有给头部的url路径，可以通过这里设置。
5. 自定义代理。一般填写形式 http://127.0.0.1:1080
6. 合并输出目录。合并文件最终的输出位置。
7. 临时下载目录。分段的下载目录，如果电脑有一个固态，一个机械，建议上一个选项设置成机械的路径，本选项设置为固态的路径。
8. 临时合并目录。由于ffmpeg命令行的限制，无法单次合并过多分段（大概在1000个分段左右，未验证），因此增加一个临时合并输出目录，通常情况下建议留空或与上一项保持一致（默认也是如此）。
9. 自定义aria2c参数。具体参见官方文档：http://aria2.github.io/manual/en/html/aria2c.html
10. 自定义ffmpeg参数。具体参见官方文档：http://www.ffmpeg.org/ffmpeg.html#toc-Main-options
11. aria2c相关参数略。
12. 仅合并视频/音频。对于需要解密的视频来说，即使选其一，依然需要完整解密。
13. 自动命名。指对输入优酷、腾讯等特定网站的m3u8时，自动获取设定文件名。
14. 仅解析m3u8。会保存一份m3u8的原始文件在本地。
15. 仅下载m3u8。指下载视频分段但不合并（也不解密）。
16. 尝试0day命名。指通过预设配置，在下载时自动命名文件为0day形式，目前尚未完成，功能暂不可用。
17. 不使用代理/使用系统代理/自定义代理。三者只能选其一，均为对请求m3u8的设定。如果想让aria2c走代理，请在自定义aria2c参数中设定。
18. 解密但不合并。字面意思，需要注意的是，此时即使勾选下载完成后自动合并，也不会合并。
19. 开始/暂停/重新开始/删除/仅删除任务。属于多任务管理中的选项，目前暂未完成设计，功能暂不可用。
20. Start!按钮。用于开始下载m3u8任务。

## 配置文件

- 没有填入m3u8地址/文件时，点击Start可以生成默认配置
- file_ext指合并文件后缀，audio_file_ext指音频文件合并后缀，video_file_ext指视频文件合并后缀
- workers指解密时的线程数量，默认值4
- once_max_files_to_concat指单次合并分段数，当分段数过多时，合并过程会分为多次合并进行

## 不支持的特性

- 不支持master类型的m3u8下载
- 不支持标准AES模式和优酷加密以外的解密方式
- 不支持m3u8文件批量下载（暂时）
- 不支持多任务管理（暂时）
- 不支持视频解析功能（暂时）

## 优酷视频key

获取key的js如下（请存书签使用）：
```JavaScript
javascript:prompt(videoPlayer.getData()._videoData.title + " key", btoa(String.fromCharCode.apply(null, new Uint8Array(____hexA))));
```

### 演示

1. 新建一个书签/收藏，标题随意，网址的地方填写上面的js代码。

![新建书签](http://puui.qpic.cn/vshpic/0/MVXduLh0WwyThtrGaViy3flMkaqKJ4gczVZtiiQpyOnvkRRh_0/0)

2. 打开加密的优酷视频页面，待视频加载后，点击该书签，此时弹出解密用的key。

![获取key](http://puui.qpic.cn/vshpic/0/qNk4W9hQSPZN7Od8nPl9MAQwJekoNQD8Bar7HMTNGzlhwkOi_0/0)

## 其他

- 支持m3u8文件拖入。
- 路径以及可执行程序（aria2c、ffmpeg）均支持拖入设定。
- 64位系统请手动替换aria2c为64位版本，否则在某些版本的系统上无法正常更新下载进度！

# 关于本软件

- 闭源
- 项目地址：https://github.com/xhlove/vvtoolbox-gui-series

# 更新日志

## 2020/2/20 v0.3.8

1. 不删除分段bug修复
2. 缩放显示问题修复（未验证）
3. 说明完善&优酷key获取js代码简化
4. 增加临时下载文件夹自动移除（合并成功时）
5. 使用公开渠道发布

## 2020/2/19 v0.3.7

1. 仅合并音频、视频错误修复
2. 自动删除分段逻辑改进（需要解密的情况下）
3. 全部黑窗隐藏
4. 解密不全bug修复
5. 合并进度异常调整
6. 默认解密模式更改为AES-YK，降低错误概率
7. 关于界面载入说明