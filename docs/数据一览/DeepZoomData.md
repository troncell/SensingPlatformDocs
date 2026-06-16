# DeepZoomData 数据源

## 数据源用途

DeepZoomData 用于 DeepZoom 高清大图展示控件，存储热点（Hotspot）数据。每个热点定义了在特定缩放层级上的点击区域和对应的事件，用于实现大图上的交互点。

## 数据源注册

在 `SysConfig/DataActivators.xml` 的 `DataSourceFactory` 节点中注册：

```xml
<Data ConfigType="DeepZoomData" AssemblyFile="Data.DeepZoom" TypeName="Data.DeepZoom.DeepZoomDataProvider, Data.DeepZoom, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Data>
```

## 数据的配置

在 `Shell/Data/Data.xml` 里添加：

```xml
<DeepZoomData Name="DeepZoomData">
  <CustomerConfig>
    <Tables>
      <Table Name="Hotspots" IsRealtimeLoad="True">
        <DataQuery Value="select * from HotspotDatas order by DeepZoomLevel, Hotspot_Left, Hotspot_Top"></DataQuery>
      </Table>
    </Tables>
    <DbConnection>
      <ConnectionString Value="Data Source={$BasePath}\DeepZoomData.db3;Version=3;Pooling=True;Max Pool Size=100;"></ConnectionString>
      <DbType>System.Data.SQLite.EF6</DbType>
    </DbConnection>
  </CustomerConfig>
</DeepZoomData>
```

## 配置讲解

DeepZoomData 的配置与 [DbData](DbData.md) 类似，通过 `Tables` 和 `DbConnection` 配置数据表和数据库连接。

### 热点数据表字段

| 字段 | 说明 |
| --- | --- |
| DeepZoomLevel | 热点所在的缩放层级。 |
| Hotspot_Left / Hotspot_Top | 热点区域左上角坐标。 |
| Hotspot_Right / Hotspot_Bottom | 热点区域右下角坐标。 |
| EventType | 事件类型。 |
| EventParam | 事件参数。 |
| EventPath | 事件路径。 |
| EventID | 事件 ID。 |

## 在页面中使用

```xml
<DeepZoomElement Name="DeepZoom">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
  <DataProvider>DeepZoomData?CSTable=Hotspots</DataProvider>
  <CustomerConfig>
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\bigmap.dzi</ImageSource>
  </CustomerConfig>
</DeepZoomElement>
```

## 注意事项

1. DeepZoomData 依赖 SQLite 数据库，需要提前准备好 `DeepZoomData.db3`。
2. 热点坐标需要与 DeepZoom 图片的坐标系对应。
3. 不同缩放层级可以配置不同密度的热点。
4. 详细的 DeepZoom 控件使用请参考 [控件一览/DeepZoomElement.md](../控件一览/DeepZoomElement.md)。
