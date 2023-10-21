# 安卓逆向合集
> 此项目为安卓逆向实战合集以及部分笔记
>
> 仅作学习分析以及学习记录，__禁止商用__，如遇__侵权__请联系删除
>
> 本项目将持续更新

## 环境篇
众所周知，安卓逆向首先需要一个安卓环境，有两种方案，第一是模拟器，第二是真机

### 模拟器
市面上有很多模拟器可以用，up选择的是夜神模拟器，在官网下载好模拟器后，我们需要改一些配置

第一，抓包配置 --> 配置WIFI的IP以及按照你的抓包工具进行配置。

第二，开root，很简单

> 但是会出现抓包抓不到的情况，这种是由于在java层配置了不走系统代理，所以我们需要别的工具：
>
> 1. drony(不推荐)，有时会导致无法上网，不稳定
> 2. SocksDroid(推荐)，开启工具时记得删除系统代理

> 注: 夜神模拟器默认的端口是62025, 所以我们需要连接这个端口(不一定，我的电脑是这个端口)

### 反编译工具

1. jadx(java层)
2. jeb(java层)
3. ida(so层，c语言层)

### 查壳脱壳工具

按照自己的喜好即可，网上有很多

### 获取apk途径

百度搜索即可

## 实战篇

> 更多的笔记见其他文件。

| 项目 | 难度 |
| ---- | ---- |
| 豆瓣 | 简单 |
| 某物 | 中等 |

### 豆瓣

想必大家爬虫梦的开始就是豆瓣250吧，那么我们安卓逆向的开始也从豆瓣开始吧~

分析过程:

1. 首先抓包分析，确认接口，确认加密参数名: _sig
2. 全局搜索，确认加密位置
3. hook加密函数，分析加密流程
4. 用python改写，实现发包

总结算法： 豆瓣的_sig是由请求方式以及url的path和时间戳以&相连，进行一次hmacsha1，然后将结果转化为base64的格式

### 某物

第二个案例首先更新第一部分，newSign的获取。得物前几个版本比较简单，但是新版本有些内容不太一样

第一，newSign放到so层添加，并且是VMP的so文件，在这里我们不分析这个so文件，在全局搜索其他部分，找到加密位置

分析过程:
1. 首先抓包分析，需要分析参数: newSign
2. 全局搜索其他关键字
3. hook函数，然后去so层分析
4. 用python改写

总结: 这个算法是将params添加四个额外的内容，排序，然后用aes加密之后在加密md5得到newSign

之后更新搜索接口的加密以及解密...
