# FolderData 数据源

## 数据源用途

SensingData 用于对接 SensingStore 云端数据接口，获取云端配置的广告（Ads）、商品（Products）、应用（Apps）、元数据（Metas）、员工（Staffs）、SKU（Skus）等数据。

主要用于AppPod中的数据作为数据源，这种方式简单明了，比较直观。同时监听文件夹内的文件变化也可以拿到动态的文件，本配置用于文件夹的数据显示。

## 前置依赖

使用 SensingData 前，需要确保：

1. `Data.Sensing.dll` 存在于应用目录中。
2. `Data.Sensing.dll.config` 中配置了正确的云端地址和订阅密钥：

```xml
<appSettings>
  <add key="Addr" value="http://your-sensing-server/" />
  <add key="Subkey" value="your-subkey" />
</appSettings>
```

## 数据的配置

在文件 Data.xml 里添加，添加后同时需要在 Data 文件夹下有对应文件夹和子文件夹

```xml
<SensingData Name="SensingData">
    <CustomerConfig>
      <Tables>
        <Table Name = "Ads" Type = "Ads">
          <Sql Value="SkuId=[]" />
        </Table>
        <Table Name="Products" Type ="Products">
          <Sql Value="CategoryIds=[17295];" />
        </Table>
      </Tables>
    </CustomerConfig>
  </SensingData>
```

## 配置讲解

### Tables 配置

1. `Name`：数据表名称，供 `DataProvider` 的 `CSTable` 使用。
2. `Type`：数据类型，目前支持 `Ads`、`Products`、`Apps`、`Metas`、`Staffs`、`Skus`。

### 数据字段

不同 Type 返回的字段不同，常见字段包括：

- `Id`：数据唯一标识。
- `Name`：名称。
- `ImageUrl` / `FileUrl`：图片或文件地址。
- `Description`：描述。
- `TemplateID`：模板 ID（部分数据会自动添加）。

## 在页面中使用

```xml
<FlipViewElement Name="flipView">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
  <DataProvider>SensingData?CSTable=Products</DataProvider>
  <Items IsCacheUI="True">
    <Template Left="0" Top="0" Width="1920" Height="1080" TemplateID="10001">
      <ImageElement Name="resource">
        <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" Opacity="1" IsUseCache="True" />
        <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\{$ImageUrl}</ImageSource>
      </ImageElement>
    </Template>
  </Items>
</FlipViewElement>
```

## 注意事项

1. SensingData 依赖云端服务，首次启动时需要联网下载数据。
2. 图片等资源会自动下载到本地缓存。
3. 如果云端数据更新，需要重启应用或触发 `LoadData` 事件重新加载数据源。
