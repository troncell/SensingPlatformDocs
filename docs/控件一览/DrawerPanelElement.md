# 抽屉控件（DrawerPanelElement）

## 控件作用

抽屉控件以抽屉的效果显示图片，可以拉出和推进图片。

## 控件 UI 效果

![Placeholder](../images/DrawerPanelElement.gif)

## 配置文件样例

```xml
<DrawerPanelElement>
    <UIDisplay Left="2" Top="575" Width="681" Height="380" IsShow="True" ZIndex="2" UsePercent="False" />
        <Controls>
            <XYContainerElement>
                <UIDisplay Left="0" Top="0" Width="681" Height="380" IsShow="True" ZIndex="1" UsePercent="False" />
                <Controls>
                    <ImageElement>
                     <UIDisplay Left="0" Top="0" Width="681" Height="380" IsShow="True"
                          ZIndex="1" UsePercent="False" />
                    <ImageSource UriKind="Application">
                          Shell\Pages\choutiPage\resource\drawerbg2.png</ImageSource>
                    </ImageElement>
                    <ImageElement name="introduce">
                    <UIDisplay Left="0" Top="0" Width="684" Height="148" IsShow="True"
                          ZIndex="1" UsePercent="False" />
                    <ImageSource UriKind="Application">
                          Shell\Pages\choutiPage\resource\introduce1.png</ImageSource>
                    </ImageElement>
                </Controls>
            </XYContainerElement>
        </Controls>
    <CustomerConfig>
        <DrawerPanel CollapseHeight="140" IsCollapse="True"></DrawerPanel>
    </CustomerConfig>
</DrawerPanelElement>

```

## 配置说明

### 节点 CustomerConfig

#### 属性说明

      CollapseHeight:  抽屉在未拉出状态时，显示的长度；

      IsCollapse ：抽屉效果的触发状态，True为抽屉未拉出，可以拉出，False为抽屉已拉出，可以推进；

# UIControlDict.xml 添加抽屉控件

如果使用抽屉控件则需要在 UIControlDict.xml 中添加抽屉控件

```
  <!--UI.DrawerPanel控件包-->
<Element ViewType="DrawerPanelElement" AssemblyFile="UI.DrawerPanel.dll" TypeName="UI.DrawerPanel.DrawerPanelControl, UI.DrawerPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.DrawerPanel.dll" TypeName="UI.DrawerPanel.DrawerPanelControlViewModel, UI.DrawerPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
<!--UI.DrawerPanel End-->
```
