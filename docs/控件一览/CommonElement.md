# 公用内容讲解（CommonElement）

## UIDisplay片段讲解

示例：
```
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True"/>
```


描述：

1. UIDisplay是用于控件定位使用的，是框架的配置配置节点之一，务必记清楚其属性的含义。Left为距左边框距离 Top距上边框距离 Width宽度 Height高度
2. IsShow是否显示值为True表示显示False表示不显示 
3. ZIndex表示所在的层级，值为1表示层级最低在最底层 
4. UsePercent是否根据页面的比例配置，如果值为True则是按照比例配置，若为False则不是按照比例配置，是按照页面的实际像素大小
5. Opcity设置透明度1为全不透0为全透
6. IsHitTestVisible是否可穿透它，点击层级低一点的控件，True为可穿透，False为不可穿透
7. IsUseCache控件是否缓存True是缓存，False为不缓存
   
**其中很多为可选项，如Opcity，IsHitTestVisible，IsUseCache等**


## ImageSource、FileSource片段讲解

示例：

相对于整个demo的路径:
```
<ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
</ImageElement>
```

相对于当前xml文件所在的相对路径下的文件夹，此文件是与当前xml文件同级文件夹下:
```
<ImageSource UriKind="Relative"> lianliankan.png</ImageSource>
```

描述：

1. ImageSource配置是FileSource配置的扩展，其含义和FileSource的配置含义完全一样，仅名字不一样。

2. ImageSource中UrlKind是配置路径的类型

   Relative是相对于当前xml的位置
   Application是相对于整个demo的位置
   Absolute是真实的物理路径，如c:\Images\
   Project是去掉shell的路径
  


## DataProvider连接数据库配置片段讲解

示例：
```
<DataProvider>FishEyeData?CSTable=FishEye</DataProvider>
```

描述：

1. DataProvider是用于连接数据库，从数据库中动态提取信息，具体如何进行连接数据库配置请参照文档《Data配置》
2. DataProvider片段在页面中相当于把前台的页面和后台数据库的配置关联在一起
格式为：FishEyeData?CSTable=FishEye
3. FishEyeData为数据库名称既Data.xml配置中```<DbData Name="FishEyeData">```中Name的值
4. CSTable为所使用的是表的形式，一般是固定格式不需要更改
5. FishEye为表名称即Data.xml配置中 ```<Table Name="FishEye">```



## Items片段讲解

```
示例：


<!--放置Template-->
<Items>
<Template>
<!--放置简单的控件ImageElement，如何配置控件请参考基本控件配置中ImageElement控件的配置方法-->

<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True"  ZIndex="1" UsePercent="False"/>
<ImageSource UriKind="Application">{$IconPath}</ImageSource>            <ClickEvent>{$EventAction}?Page={$NavigatePage}&amp;Args=imageButton</ClickEvent>
</ImageElement>
</Template>
</Items>

<!--放置简单的控件ImageElement，如何配置控件请参考基本控件配置中ImageElement控件的配置方法-->
<Items>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True"  ZIndex="1" UsePercent="False"/>
<ImageSource UriKind="Application">Shell\ FishEyeData\ KPIRedA.png</ImageSource>
</ImageElement>
</Items>


<!--放置Item-->
<Items>
<Item>
<!--放置简单的控件ImageButton，如何配置控件请参考基本控件配置中ImageButton控件的配置方法-->

<ImageButton>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True"  ZIndex="1" UsePercent="False"/>
<ImageSource UriKind="Application">Shell \FishEyes\KPIRedA.png</ImageSource>
<ClickEvent>Navigate?Page=HomePage&amp;Args=imageButton</ClickEvent>
</ImageButton>
</Item>
</Items>



<!--混合放置-->

<Items>
<Template>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True"  ZIndex="1" UsePercent="False"/>
<ImageSource UriKind="Application">{$IconPath}</ImageSource>
<ClickEvent>{$EventAction}?Page={$NavigatePage}&amp;Args=imageButton</ClickEvent>
</ImageElement>
</Template>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True"  ZIndex="1" UsePercent="False"/>
<ImageSource UriKind="Application">Shell\Data\ KPIRedA.png</ImageSource>
</ImageElement>
</Items>
```

描述：

Items是相当于一个容器，可以包含一些简单的控件,如ImageElement、ImageButton、TextElement等
一般在Items下会有如下四中配置方式
1. 放置多个Item节点，通常在Items中列举出有多少个子项目就配置多少个Item节点，相当于一个子级别的容器，里面也可以含有一个或多个简单的控件，如ImageElement、ImageButton、TextElement等

2. 放置多个Template，用于使用进行动态的配置，显示出不同的效果，相当于一个子级别的容器，若用户指定节点个数而不是从数据库中动态查询节点个数则不需要配置此项，里面也可以含有一个或多个简单的控件，如ImageElement、ImageButton、TextElement等

3. 直接将一些简单的控件配置在Items下，如可以将ImageElement、ImageButton、TextElement等控件

4. 在Items下可以任意搭配以上三种配置节点

