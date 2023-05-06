# 楼层Floors控件（FloorsElement）

## 控件作用

楼层Floors

## 控件UI效果
![Placeholder](../images/.png)



## 配置文件样例
```
<FloorsElement Name="floors">
      <UIDisplay Left="570" Top="1005" Width="1203" Height="85" IsShow="True" ZIndex="2"
        UsePercent="False" />
      <DataProvider>wyfData?CSTable=Floors</DataProvider>
      <Items>
        <Template Left="0" Top="20" Width="146" Height="58" TemplateID="11001">
          <ToggleButton>
            <UIDisplay Left="0" Top="0" Width="146" Height="58" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <CustomerConfig>
              <ImageSource UriKind="Application">Shell\Data\wyfData\CacheData\{$Extends}</ImageSource>
              <ImageSourceChecked UriKind="Application">
                Shell\Data\wyfData\CacheData\{$ThumbnailImageUrl}</ImageSourceChecked>
              <CheckedEvent>
                <Event>
                  FloorIndexChangedEvent?TargetPageName=HomePage&amp;TargetControlName=map&amp;FloorId={$Id}</Event>
                <Event>ResetEvent?TargetPageName=HomePage&amp;TargetControlName=ScaleBar</Event>
              </CheckedEvent>
              <GroupName>AAA</GroupName>
              <IsChecked>False</IsChecked>
            </CustomerConfig>
          </ToggleButton>
        </Template>
      </Items>
      <CustomerConfig>
        <Floors Orientation="horizontal" />
      </CustomerConfig>
    </FloorsElement>
```


## 配置说明






