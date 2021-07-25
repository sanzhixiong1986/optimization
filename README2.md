# optimization
cocos drawcall优化

------

### 要点

- 什么是drawcall
- 为什么要减少drawcall
- 动态合图

------

### 什么事drawcall

DrawCall 是绘图指令

cpu调用图形api，命令cpu进行绘图渲染

------

### 为什么要减少DrawCall？

原因：cpu每一次内存读取，数据处理和状态切换都会带来时间上的消耗。大量DrawCall会让cpu自顾不暇，但是gpu大部分时间都在摸鱼，是导致性能下降的主要原因。所以DrawCall越少越好。

------

### 静态合图

1. 尽量把一个模块下的图片打包到一个图集上，这样在使用的时候就会让drawcall变少
2. 使用label的时候尽量使用BMfont模式，这样可以使用这个模块下的打包图集也是减少drawcall的一个方式
3. 图集不要超过2048*2048大小，否则可能会有问题。
4. 使用TexturePacker 进行图集进行打包。

------

### 字体

label的渲染：使用图片对文字进行渲染，所以每次渲染都很耗

label尽量使用BMFont来代替TTF的方式，这样可以减少一些drawcall

使用 cache model选项来解决ttf字体的性能问题（这种方式只适用于不修改的文字，俗称的静态文本）

#### char模式

作用：将label出现的所有字符都缓冲到一张图中，相当于bmfont的使用方式，这个对于频繁更换操作是有利的。

如果开启上面的操作的话，就需要把label放在一起，图片放在一起

如果是大量的文本可以使用这种模式。

------

参考资料：https://www.twblogs.net/a/5efe7c0f9644181341a14f54

官网资料：https://docs.cocos.com/creator/manual/zh/components/label.html#%E6%96%87%E6%9C%AC%E7%BC%93%E5%AD%98%E7%B1%BB%E5%9E%8B%EF%BC%88cache-mode%EF%BC%89
