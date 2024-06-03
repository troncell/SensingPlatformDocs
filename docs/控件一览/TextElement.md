# 文字控件（TextElement）

## 控件作用

在页面或者弹出框中直接显示文字。

## 控件 UI 效果

![Placeholder](../images/TextElement.png)

## 配置文件样例

```xml
<TextElement Name="LogoText">
    <!--参考控件公用片段的讲解中UIDdisplay片段讲解-->
    <UIDisplay Left="800" Top="1000" Width="1100" Height="80" IsShow="True"  ZIndex="1" UsePercent="False"/>
    <!--文本的配置 ForegroundColor文字颜色，Family为字体，Size文字大小，CultureInfo语言，Alignment对齐方式, LineHeight每行的高度，VerticalAlignment垂直方向上的对齐方式-->
    <TextSource ForegroundColor="#FFFF0000" Family="微软雅黑" Size="50" CultureInfo="zh-CN" Alignment="Center" LineHeight="80" VerticalAlignment="Top">这里就是你放文字的地方</TextSource>
    <CustomerConfig>
        <!--Enable走马灯是否开启，Duration走一遍所花的时间，Direction走马灯的方向，分为顺时针Clockwise，和逆时针Counterclockwise-->
        <AutoMove Enable="True" Duration="00:00:20" Direction="Clockwise"/>
    </CustomerConfig>
</TextElement>
```

```
 <TextElement Name="名称">
                        <!--参考控件公用片段的讲解中UIDdisplay片段讲解-->
                        <UIDisplay Left="100" Top="52" Width="400" Height="180" IsShow="True" ZIndex="2" UsePercent="False" />
                        <!--文本的配置ForegroundColor文字颜色，Family为字体，Size文字大小，CultureInfo语言，Alignment对齐方式-->
                        <TextSource ForegroundColor="#FFFFFFFF" Family="黑体" Size="24"
                          CultureInfo="zh-CN" Alignment="Left">{$Name}</TextSource>
                      </TextElement>
```

## 配置说明

### 节点 TextSource

    需要显示的文字内容

    属性说明

    ForegroundColor：文字的颜色；
        Family：文字的样式；
        Size：文字的大小；
        CultureInfo：语言；
        Alignment：对齐方式。

### 节点 CustomerConfig

    此节点主要为了实现，文字的走马灯效果，不需要此效果的，此节点可以去掉
    AutoMove节点控制走马灯的具体效果

    属性说明

    Enable: 是否开启，True为开启，False不启用
        Duration：走一遍所花的时间,格式如下 "00:00:20"
        Direction：走马灯的方向，分为顺时针Clockwise，和逆时针Counterclockwise

# UIControlDict.xml 添加文字控件

如果使用文字控件则需要在 UIControlDict.xml 中添加文字控件

```
  <Element ViewType="TextElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.TextControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.TextElementViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
