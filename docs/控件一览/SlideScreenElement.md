# 推拉屏控件（SlideScreenElement）

## 控件作用

监听推拉屏位置变化， 到达相应的位置后解发相应的事件

## 控件UI效果


## 配置文件样例
```
<SlideScreenElement>
    <UIDisplay Left="0" Top="600" Width="1920" Height="400" IsShow="True" ZIndex="1" UsePercent="False" />
    <ClickEvent>PopupEvent?TargetPageName=CBPage{$ScreenIndex}&amp;TargetControlName=CBPop&amp;X=0&amp;Y=0&amp;Height=1920&amp;Width=1080&amp;EventID=CBShow&amp;&amp;UriKind=Application&amp;EventPath=Shell\Pages\CBPage\PopItems</ClickEvent>
    <CustomerConfig>
        <SlideScreen Vendor="互动滑轨系统"/>
    </CustomerConfig>
</SlideScreenElement>
```


## 配置说明
1. Vendor: 暂时只支持一种
2. 事件：复用常规弹出框事件，其中 **{$ScreenIndex}** 为传入相应的屏的编号（从1开始）





