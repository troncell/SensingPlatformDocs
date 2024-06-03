# 飞图控件（AlbumElement）

## 控件作用

飞图控件以自动浮动的交互方式展示一系列图片或视频，它的特点是更换资料非常方便，只要更换文件夹里面的图片即可。

## 控件 UI 效果

![Placeholder](../images/album_1.png)

## 配置文件样例

```xml
<AlbumElement>
<!--参考控件公用片段CommonElement.md讲解中UIDisplay片段讲解-->
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="false" />
    <CustomerConfig>
        <BgType Type="1" UriKind="Application">Shell\Pages\PhotoPage\resource\bg\bg.png</BgType>
        <Fold UriKind="Application">Shell\Pages\PhotoPage\resource</Fold>
        <IsFoldBarVisible>False</IsFoldBarVisible>
    </CustomerConfig>
</AlbumElement>
```

## 配置说明

1.节点 BgType:

Type:是否配置背景，1 为显示，0 为不显示，然后配置背景图片所在的位置即可；

2.节点 Fold:配置资源文件夹所在的路径；

3.节点 IsFoldBarVisible False 表示下方分类文件夹是否显示，False 表示不显示，True 则表示显示。

## UIControlDict.xml 添加飞图控件

如果使用飞图控件则需要在 UIControlDict.xml 中添加飞图控件

```
 <!--UI.AlbumLibrary 控件包-->
  <Element ViewType="AlbumElement" AssemblyFile="UI.Album.dll" TypeName="UI.Album.AlbumControl, UI.Album, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.CoverFlow.dll" TypeName="UI.AlbumLibrary.AlbumControlViewModel, UI.Album, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.AlbumLibrary  END-->
```
