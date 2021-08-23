# 文字控件（TextElement）

## 控件作用

在页面或者弹出框中直接显示文字。

## 控件UI效果

![Placeholder](../../images/TextElement.png)

## 配置文件样例

```
<TextElement Name="LogoText">
    <!--参考控件公用片段的讲解中UIDdisplay片段讲解-->
    <UIDisplay Left="800" Top="1000" Width="1100" Height="80" IsShow="True"  ZIndex="1" UsePercent="False"/>
    <!--文本的配置 ForegroundColor文字颜色，Family为字体，Size文字大小，CultureInfo语言，Alignment对齐方式-->
    <TextSource ForegroundColor="#FFFF0000" Family="微软雅黑" Size="50" CultureInfo="zh-CN" Alignment="Center">这里就是你放文字的地方</TextSource>
</TextElement>
```
## 配置说明

### 节点TextSource

    需要显示的文字内容

    属性说明

        ForegroundColor：文字的颜色；

        Family：文字的样式；

        Size：文字的大小；

        CultureInfo：语言；

        Alignment：对齐方式。


