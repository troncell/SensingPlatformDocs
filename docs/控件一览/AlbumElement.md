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
    <DataContext AssemblyFile="UI.Album.dll" TypeName="UI.Album.AlbumControlViewModel, UI.Album, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.AlbumLibrary  END-->
```

## 系统DLL配置，文件UI.Album.dll.config
```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <appSettings>
    <add key="Fold" value="Resources"/>
    <!--1左移2右移-->
    <add key="Direction" value="2"/>
    <!--摆动幅度-->
    <add key="SwingAngle" value="0"/>
    <!--摆动角度最大速度(0.1~1)-->
    <add key="SwingAngleMaxSpeed" value="0.0"/>
    <!--滑动速度-->
    <add key="SweepSpeed" value="1"/>
    <!--滑动频率毫秒-->
    <add key="SweepInterval" value="1"/>
    <!--是否随机显示-->
    <add key="RandomShow" value="true"/>
    <!--自动关闭弹出窗口时间，整数s-->
    <add key="AutoClostInterval" value="3"/>
    <!--本地web资源文件夹-->
    <add key="LocalWebPath" value="WebResources\LocalWebs"/>
    <!--ie图标文件夹-->
    <add key="IEImages" value="WebResources\IEImages"/>
    <!--签名对应名称-->
    <add key="SignMark" value="Sign"/>
    <!--背景类型（1：picture,2:video,3:web）#后面加bg文件夹下的资源,web例子：3#XXX.htm-->
    <add key="BgType" value="1#bg.png"/>
    <!--选择保存路径，0：temp文件夹；1：领导文件夹-->
    <add key="SavePath" value="0"/>
    <add key="KeepAngle" value="True"/>
    <!-- 随机摆动范围 -->
    <add key="ROTATESCROPE" value="0"/>
  </appSettings>
</configuration>
```
