# 推拉屏控件（SlideScreenElement）

## 控件作用

监听推拉屏位置变化， 到达相应的位置后解发相应的事件

## 控件UI效果

## 配置文件样例
```
<SlideScreenElement Name="SlideScreen">
        <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
        <ClickEvent>PopupEvent?TargetPageName=CBPage&amp;TargetControlName=CBPop&amp;X=0&amp;Y=0&amp;Height=1920&amp;Width=1080&amp;EventID={$ScreenName}&amp;sheet={$sheet}&amp;weizhi={$weizhi}&amp;UriKind=Application&amp;EventPath=Shell\Pages\CBPage\PopItems</ClickEvent>
        <CustomerConfig>
            <SlideScreen Vendor="lasa">
                <Setting>
                    <IP>127.0.0.1</IP>
                    <Port>8002</Port>
                    <RecvPort>8888</RecvPort>
                    <Debug>true</Debug>

                    <!--判断移动误差-->
                    <Tolerance>0.01</Tolerance>
                    <!--每块屏的区间位置  -->
                    <ScreenPositions>
                        <ScreenPosition Rate="0" Index="0" Name="A"/>
                        <ScreenPosition Rate="0.25" Index="1" Name="B"/>
                        <ScreenPosition Rate="0.5" Index="2" Name="C"/>
                        <ScreenPosition Rate="0.75" Index="3" Name="D"/>
                        <ScreenPosition Rate="1" Index="4" Name="E"/>
                    </ScreenPositions>
                </Setting>
            </SlideScreen>
        </CustomerConfig>
    </SlideScreenElement>
```

## 上海手动推拉屏配置
```
<SlideScreenElement Name="SlideScreen">
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
    <ClickEvent>PopupEvent?TargetPageName=HomePage&amp;TargetControlName=HomePop&amp;X=0&amp;Y=0&amp;Height=1920&amp;Width=1080&amp;EventID={$ScreenName}Event&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\PopItems</ClickEvent>
    <CustomerConfig>
    <SlideScreen Vendor="shanghai">
        <Setting>
        <IP>127.0.0.1</IP>
        <RecvPort>6666</RecvPort>
        <Debug>false</Debug>
        <ScreenPositions>
            <ScreenPosition  Index="0" Name="A"/>
            <ScreenPosition  Index="1" Name="B"/>
            <ScreenPosition  Index="2" Name="C"/>
            <ScreenPosition  Index="3" Name="D"/>
            <ScreenPosition  Index="4" Name="E"/>
        </ScreenPositions>
        </Setting>
    </SlideScreen>
    </CustomerConfig>
</SlideScreenElement>
```

## 点击屏幕按钮发送移动指令
```
<!-- 下一页-->
<ImageButton>
    <UIDisplay Left="100" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
    <ImageSource UriKind="Application">Shell\Pages\Common\bg.png</ImageSource>
    <Content>
        <TextElement >
            <UIDisplay Left="0" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
            <TextSource ForegroundColor="#FFFF0000" Family="微软雅黑" Size="50" CultureInfo="zh-CN" Alignment="Center">下一页</TextSource>
        </TextElement>
    </Content>
    <ClickEvent>IndexChanged?TargetPageName=HomePage&amp;TargetControlName=SlideScreen&amp;IndexString=Next&amp;Index=-1</ClickEvent>
</ImageButton>
```

```
<!-- 上一页-->
<ImageButton>
    <UIDisplay Left="500" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
    <ImageSource UriKind="Application">Shell\Pages\Common\bg.png</ImageSource>
    <Content>
        <TextElement >
            <UIDisplay Left="0" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
            <TextSource ForegroundColor="#FFFF0000" Family="微软雅黑" Size="50" CultureInfo="zh-CN" Alignment="Center">上一页</TextSource>
        </TextElement>
    </Content>
    <ClickEvent>IndexChanged?TargetPageName=HomePage&amp;TargetControlName=SlideScreen&amp;IndexString=Pre&amp;Index=-1</ClickEvent>
</ImageButton>
```
## 配置说明
1. Vendor: 暂时只支持一种lasa和shanghai两种，lasa是电动屏,shanghai是手动屏
2. 事件：复用常规弹出框事件，其中 **{$ScreenName}** 对应ScreenPosition传入的Name，替换效果为：**EventID=AEvent**， **EventID=BEvent**


## 测试工具下载(解压双击运行)
[lasa 推拉屏服务测试](../../tools/slidescreen_test_server_lasa.zip)

[shanghai 推拉屏服务测试工具](../../tools/slidescreen_test_server_shanghai.zip)

[湖南滑轨测试工具](../../tools/hunan.zip)




