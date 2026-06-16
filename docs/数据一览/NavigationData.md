# NavigationData 数据源

## 数据源用途

NavigationData 用于对接商场/楼宇导航数据接口，提供楼层（Floors）、房间（FloorRooms）、店铺（Stores）、停车位（Parking）等数据，支持室内路径规划。

## 数据源注册

在 `SysConfig/DataActivators.xml` 的 `DataSourceFactory` 节点中注册：

```xml
<Data ConfigType="NavigationData" AssemblyFile="Data.Navigation" TypeName="Data.Navigation.NavigationDataProvider, Data.Navigation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <ConfigModel AssemblyFile="Data.Navigation" TypeName="Data.Navigation.NavigationSourceModel, Data.Navigation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Data>
```

## 数据的配置

在 `Shell/Data/Data.xml` 里添加：

```xml
<NavigationData Name="BuildingData">
  <CustomerConfig>
    <WebApi>
      <ApiOptions BaseUrl="http://your-navigation-server/" ApiUrl="/api/buildingdata" />
      <CacheOptions IsCache="True" Directory="CacheData" JsonFile="navigation.json" />
    </WebApi>
    <MachineId>123</MachineId>
  </CustomerConfig>
</NavigationData>
```

## 配置讲解

### WebApi 节点

与 [WebAPIData](WebAPIData.md) 配置相同，用于指定导航数据接口地址和缓存选项。

### MachineId 节点

指定当前设备所在的房间/店铺 ID，用于路径规划的起点计算。

## 数据表名称

NavigationData 会自动生成以下数据表：

| 表名 | 说明 |
| --- | --- |
| `Floors` | 楼层数据，包含楼层 ID、名称、图片、Logo 等。 |
| `FloorRooms` | 房间/店铺数据，包含楼层 ID、房间 ID、位置坐标、店铺信息等。 |
| `Stores` | 店铺数据（内部使用）。 |
| `Parking` | 停车位数据。 |

## 常用字段

### Floors 表

| 字段 | 说明 |
| --- | --- |
| Id | 楼层 ID。 |
| BuildingId | 所属建筑 ID。 |
| Name | 楼层名称。 |
| ImageUrl | 楼层平面图 URL。 |
| LogoUrl | 楼层 Logo URL。 |
| ThumbnailImageUrl | 楼层缩略图 URL。 |
| Extends | 扩展信息。 |

### FloorRooms 表

| 字段 | 说明 |
| --- | --- |
| FloorId | 所属楼层 ID。 |
| RoomId | 房间 ID。 |
| RoomType | 房间类型。 |
| StoreId | 店铺 ID。 |
| LocationX / LocationY | 房间在楼层图上的坐标。 |
| StoreName | 店铺名称。 |
| Description | 店铺描述。 |
| StoreImageUrl | 店铺图片 URL。 |
| StoreLogoUrl | 店铺 Logo URL。 |
| StoreContent | 店铺详情。 |
| StoreShoppingHours | 营业时间。 |
| StoreContact | 联系方式。 |
| ParentLargeClassName | 大类名称。 |
| CategoryName | 分类名称。 |
| IsShowInMap | 是否在地图上显示。 |
| RoomName | 房间名称。 |

## 在页面中使用

```xml
<DataProvider>BuildingData?CSTable=Floors</DataProvider>
```

或：

```xml
<DataProvider>BuildingData?CSTable=FloorRooms</DataProvider>
```

## 注意事项

1. 导航数据依赖远程接口，首次加载需要联网。
2. 楼层图片、店铺 Logo 等资源会自动下载到本地缓存。
3. 路径规划功能由 `UI.NavigationControl` 控件消费，具体使用请参考该控件文档。
