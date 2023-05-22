# 楼层Map控件（MapElement）

## 控件作用

楼层Map

## 控件UI效果
![Placeholder](../images/.png)



## 配置文件样例
```
<MapElement Name="map">
      <UIDisplay Left="376" Top="0" Width="1540" Height="1080" IsShow="True" ZIndex="2"
        UsePercent="False" />
      <DataProvider>wyfData?CSTable=FloorRooms</DataProvider>
      <Items>
        <Template TemplateSelection="RoomType=Store">
          <XYContainerElement>
            <UIDisplay Left="20" Top="100" Width="245" Height="205" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <Controls>
              <ImageElement>
                <UIDisplay Left="0" Top="0" Width="245" Height="205" IsShow="True" ZIndex="1"
                  UsePercent="False" />
                <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\logoImg_bg.png</ImageSource>
              </ImageElement>
              <ImageButton>
                <UIDisplay Left="0" Top="0" Width="245" Height="205" IsShow="True" ZIndex="1"
                  UsePercent="False" />
                <ImageSource UriKind="Application">Shell\Data\wyfData\CacheData\{$StoreLogoUrl}</ImageSource>
                <ClickEvent>
                  PopupEvent?TargetPageName=HomePage&amp;TargetControlName=BrandIntroPop&amp;EffectName=ScaleClose&amp;EventID=BrandIntroduce&amp;UriKind=Application&amp;EventPath=Shell\Pages\Common&amp;Tittle={$StoreName}&amp;StoreLogoUrl={$StoreLogoUrl}&amp;ShowImage={$StoreImageUrl}&amp;StoreContent={$StoreContent}&amp;StoreId={$StoreId}&amp;StoreShoppingHours={$StoreShoppingHours}&amp;StoreContact={$StoreContact}&amp;StoreFloorString={$StoreFloorString}&amp;ParentLargeClassName={$ParentLargeClassName}&amp;CategoryName={$CategoryName}&amp;TargetStoreId={$StoreId}</ClickEvent>
              </ImageButton>
            </Controls>
          </XYContainerElement>
        </Template>
        <Template TemplateSelection="RoomType=Toilet">
          <ImageButton>
            <UIDisplay Left="0" Top="170" Width="150" Height="150" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\公共设施图标png\洗手间.png</ImageSource>
            <ClickEvent>
              PopupEvent?TargetPageName=HomePage&amp;TargetControlName=BrandIntroPop&amp;EventID=Navigation&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\CategoryPopItems&amp;TargetRoomId={$RoomId}</ClickEvent>
          </ImageButton>
        </Template>
        <Template TemplateSelection="RoomType=Elevator">
          <ImageElement>
            <UIDisplay Left="0" Top="200" Width="150" Height="150" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\公共设施图标png\直梯.png</ImageSource>
            <ClickEvent>
              PopupEvent?TargetPageName=HomePage&amp;TargetControlName=BrandIntroPop&amp;EventID=Navigation&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\CategoryPopItems&amp;TargetRoomId={$RoomId}</ClickEvent>
          </ImageElement>
        </Template>
        <Template TemplateSelection="RoomType=Ladder">
          <ImageElement>
            <UIDisplay Left="0" Top="200" Width="150" Height="150" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\公共设施图标png\扶梯.png</ImageSource>
            <ClickEvent>
              PopupEvent?TargetPageName=HomePage&amp;TargetControlName=BrandIntroPop&amp;EventID=Navigation&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\CategoryPopItems&amp;TargetRoomId={$RoomId}</ClickEvent>
          </ImageElement>
        </Template>
        <Template TemplateSelection="RoomType=VerticalLadder">
          <ImageElement>
            <UIDisplay Left="0" Top="200" Width="150" Height="150" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\公共设施图标png\直梯.png</ImageSource>
            <ClickEvent>
              PopupEvent?TargetPageName=HomePage&amp;TargetControlName=BrandIntroPop&amp;EventID=Navigation&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\CategoryPopItems&amp;TargetRoomId={$RoomId}</ClickEvent>
          </ImageElement>
        </Template>
        <Template TemplateSelection="RoomId=7">
          <CustomerElement>
            <UIDisplay Left="0" Top="0" Width="300" Height="300" IsShow="True" ZIndex="3"
              UsePercent="False" />
            <Activator AssemblyFile="weizhi" TypeName="weizhi.UserControl1" />
            <CustomerConfig>
              <Customer Scale="2"></Customer>
            </CustomerConfig>
          </CustomerElement>

        </Template>
      </Items>
      <CustomerConfig>
        <IconShell ShellWidth="128" ShellHeight="220"
          ShellImage="Shell\Pages\HomePage\resource\Kong.png" />
        <Map Width="6000" Height="2591" DefaultScale="0.25" MapLeft="0" MapTop="50"
          ShowAllIconScale="0.01" />
      </CustomerConfig>
    </MapElement>
```


## 配置说明






