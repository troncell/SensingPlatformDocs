# WebAPIData 数据源

## 数据源用途

WebAPIData 用于通过 HTTP 接口获取远程数据，并将返回的 JSON 数据转换为 DataTable，供 UI 控件绑定使用。常用于对接第三方业务系统或 SensingPlatform 后端服务。

支持两种数据形态：

- **JObjectDataWebApi**：返回单个 JSON 对象。
- **JArrayDataWebApi**：返回 JSON 数组。

## 数据源注册

在 `SysConfig/DataActivators.xml` 的 `DataSourceFactory` 节点中注册：

```xml
<!-- 单个 JSON 对象 -->
<Data ConfigType="JObjectDataWebApi" AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.JObjectWebApiDataProvider, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <ConfigModel AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Data>

<!-- JSON 数组 -->
<Data ConfigType="JArrayDataWebApi" AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.JArrayWebApiDataProvider, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <ConfigModel AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Data>
```

## 数据的配置

在 `Shell/Data/Data.xml` 里添加：

```xml
<JArrayDataWebApi Name="ProductsData">
  <CustomerConfig>
    <WebApi>
      <ApiOptions BaseUrl="http://58.214.31.206:9300/" ApiUrl="/api/getmessage" />
      <CacheOptions IsCache="True" Directory="CacheData" JsonFile="message.json">
        <ResourceColumns>ImageUrl,ThumbnailUrl</ResourceColumns>
      </CacheOptions>
      <AutoFreshData Enable="False" FreshTime="00:00:00" />
    </WebApi>
  </CustomerConfig>
</JArrayDataWebApi>
```

## 配置讲解

### ApiOptions 节点

| 属性 | 说明 |
| --- | --- |
| BaseUrl | 接口根地址。 |
| ApiUrl | 接口路径，可包含占位符，如 `/api/products/{$ID}`。 |

### CacheOptions 节点

| 属性 | 说明 |
| --- | --- |
| IsCache | 是否缓存远程数据到本地。 |
| Directory | 缓存文件存放目录。 |
| JsonFile | 缓存的 JSON 文件名。 |
| IsLocalOnly | 是否仅使用本地缓存，为 `True` 时不请求网络（本地不存在仍会请求）。 |
| UseTempCachedFolder | 是否使用临时缓存目录。 |
| ResourceColumns | 需要下载到本地的资源字段，多个字段用逗号分隔。 |

### AutoFreshData 节点

| 属性 | 说明 |
| --- | --- |
| Enable | 是否启用定时刷新。 |
| FreshTime | 刷新间隔，格式 `hh:MM:ss`。 |

## 数据表名称

- `JArrayDataWebApi` 默认生成的数据表名为 `JTable`。
- `JObjectDataWebApi` 默认生成的数据表名为 `JObject`。

在 `DataProvider` 中通过 `CSTable=JTable` 或 `CSTable=JObject` 引用。

## 在页面中使用

```xml
<FlipViewElement Name="flipView">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
  <DataProvider>ProductsData?CSTable=JTable</DataProvider>
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

1. 网络请求超时时间为 15 秒，请求失败会自动回退到本地缓存（如果 `IsLocalOnly=False` 且存在缓存）。
2. `ResourceColumns` 中配置的字段会被识别为资源链接，自动下载到本地缓存目录。
3. JSON 字段名会直接映射为 DataTable 的列名。
4. 如果 JSON 数组对象中没有 `TemplateID` 字段，系统会自动添加默认值为 `Image` 的 `TemplateID` 列。
