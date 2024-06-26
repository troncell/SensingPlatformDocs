# 长图文滑块控件（PagerElement）

## 控件作用

长图文上下滑动且左右切换上下一张

## 控件 UI 效果

![Placeholder](../images/PagerElement.png)
![Placeholder](../images/PagerElement.gif)

## 配置文件样例

```
<PagerElement Name="resource">
    <UIDisplay Left="125" Top="258" Width="829" Height="1372" IsShow="True" ZIndex="3" UsePercent="False" />
    <DataProvider>CartoonData?CSTable=深交所</DataProvider>
    <Items IsCacheUI="True">
        <Template Left="0" Top="0" Width="829" Height="1381" TemplateID="10001">
            <XYContainerElement>
                <UIDisplay Left="0" Top="0" Width="829" Height="1381" IsShow="True"  ZIndex="3" UsePercent="False"/>
                <Controls>
                    <ScrollViewerElement>
                        <UIDisplay Left="0" Top="0" Width="829" Height="1381" IsShow="True" ZIndex="4" UsePercent="False" />
                        <Items>
                            <Item>
                                <ImageElement Name="resource">
                                    <UIDisplay Left="0" Top="0" Width="829" Height="8000" IsShow="True" ZIndex="3" UsePercent="False" Opacity="1" IsUseCache="True" />
                                    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\证券基础知识\衍生品\漫画\{$Pic}</ImageSource>
                                    <CustomerConfig>
                                        <Image AutoHeight="True"/>
                                    </CustomerConfig>
                                </ImageElement>
                            </Item>
                        </Items>
                        <CustomerConfig>
                            <ScrollView />
                            <!-- <ThumbImage UriKind="Application" Width="33" Height="38">Shell\Pages\HomePage\resource\thumb.png</ThumbImage> -->
                        </CustomerConfig>
                    </ScrollViewerElement>
                </Controls>
            </XYContainerElement>
        </Template>
    </Items>
    <CustomerConfig>
        <PagerIndex VerticalAlignment="Top" Offset="-33" PageIndexColor="#" PageIndexSelectedColor="RED"  />
    </CustomerConfig>
</PagerElement>
```

## 配置说明

1. 节点 VerticalAlignment:；

2. 节点 Offset:配置左右滑动圆点的位置；

3. 节点 PageIndexColor:配置长图文滑块中，左右滑动到该长图文时，其它图标的颜色；

4. 节点 PageIndexSelectedColor: 配置长图文滑块中，左右滑动到该长图文时，该图标的颜色。

# UIControlDict.xml 添加长图文滑块控件

如果使用长图文滑块控件则需要在 UIControlDict.xml 中添加长图文滑块控件

```
  <Element ViewType="PagerElement" AssemblyFile="UI.FlipView.dll" TypeName="UI.FlipView.PagerView, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.FlipView.dll" TypeName="UI.FlipView.PagerViewModel, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
