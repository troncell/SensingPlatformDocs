# 公用内容讲解（CommonElement）

Troncell 平台上的所有可交互点都可以分解为 Troncell 的功能控件，所有的 Troncell 控件如果想在页面中体现出来都必须将控件的配置放在 page 配置文档中的相应位置

## UIDisplay 片段讲解

描述：UIDisplay 是用于控件定位使用的，是框架的配置配置节点之一，务必记清楚其属性的含义。

Left :为距左边框距离

Top :距上边框距离

Width :宽度

Height :高度

IsShow 是否显示值为 True 表示显示 False 表示不显示

ZIndex 表示所在的层级，值为 1 表示层级最低在最底层

UsePercent 是否根据页面的比例配置，如果值为 True 则是按照比例配置，若为 False 则不是按照比例配置，是按照页面的实际像素大小

Opcity 设置透明度 1 为全不透 0 为全透

IsHitTestVisible 是否可穿透它，点击层级低一点的控件，True 为可穿透，False 为不可穿透

IsUseCache 控件是否缓存 True 是缓存，False 为不缓存

其中很多为可选项，如 Opcity，IsHitTestVisible，IsUseCache 等。

示例：

```
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True"/>
```

## ImageSource、FileSource 片段讲解

示例：

相对于整个 demo 的路径:

```
<ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
</ImageElement>
```

相对于当前 xml 文件所在的相对路径下的文件夹，此文件是与当前 xml 文件同级文件夹下:

```
<ImageSource UriKind="Relative"> lianliankan.png</ImageSource>
```

描述：

1. ImageSource 配置是 FileSource 配置的扩展，其含义和 FileSource 的配置含义完全一样，仅名字不一样。
2. ImageSource 中 UrlKind 是配置路径的类型

   Relative 是相对于当前 xml 的位置

   Application 是相对于整个 demo 的位置

   Absolute 是真实的物理路径，如 c:\Images\

   Project 是去掉 shell 的路径

## DataProvider 连接数据库配置片段讲解

描述：

DataProvider 是用于连接数据库，从数据库中动态提取信息，具体如何进行连接数据库配置，请参照文档《Data 配置》。

DataProvider 片段在页面中相当于把前台的页面和后台数据库的配置关联在一起，格式为：FishEyeData?CSTable=FishEye

FishEyeData 为数据库名称既 Data.xml 配置中 `<ExcelData Name="FishEyeData">`中 Name 的值

CSTable 为所使用的是表的形式，一般是固定格式不需要更改

FishEye 为表名称即 Data.xml 配置中 `<Table Name="FishEye">`

示例：

```
<DataProvider>FishEyeData?CSTable=FishEye</DataProvider>
```

## Items 片段讲解

描述：

Items 是相当于一个容器，可以包含一些简单的控件,如 ImageElement、ImageButton、TextElement 等

一般在 Items 下会有如下四中配置方式 :

1：放置多个 Item 节点，通常在 Items 中列举出有多少个子项目就配置多少个 Item 节点，相当于一个子级别的容器，里面也可以含有一个或多个简单的控件，如
ImageElement、ImageButton、TextElement 等

```
<!--放置Item-->
<Items>
<Item>
<!--放置简单的控件ImageButton，如何配置控件请参考基本控件配置中ImageButton控件的
配置方法-->

<ImageButton>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">Shell \FishEyes\KPIRedA.png</ImageSource>
<ClickEvent>Navigate?Page=HomePage&Args=imageButton</ClickEvent>
</ImageButton>
</Item>
</Items>
```

2：放置多个 Template，用于使用进行动态的配置，显示出不同的效果，相当于一个子级别的容器，若用户指定节点个数而不是从数据库中动态查询节点个数,则不需要配置此项，里面也可以含有一个或多个简单的控件，如 ImageElement、ImageButton、TextElement 等

```
<!--放置Template-->
<Items>
<Template>
<!--放置简单的控件ImageElement，如何配置控件请参考基本控件配置中ImageElement控件
的配置方法-->

<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">{$IconPath}</ImageSource>
<ClickEvent>{$EventAction}?Page={$NavigatePage}&Args=imageButton</ClickEvent>
</ImageElement>
</Template>
</Items>
```

3：直接将一些简单的控件配置在 Items 下，如可以将 ImageElement、ImageButton、TextElement 等控件

```
<!--放置简单的控件ImageElement，如何配置控件请参考基本控件配置中ImageElement控件
的配置方法-->
<Items>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">Shell\ FishEyeData\ KPIRedA.png</ImageSource>
</ImageElement>
</Items>
```

4：在 Items 下可以任意搭配以上三种配置节点

```
<Items>
<Template>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">{$IconPath}</ImageSource>
<ClickEvent>{$EventAction}?Page={$NavigatePage}&Args=imageButton</ClickEvent>
</ImageElement>
</Template>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">Shell\Data\ KPIRedA.png</ImageSource>
</ImageElement>
</Items>
```
