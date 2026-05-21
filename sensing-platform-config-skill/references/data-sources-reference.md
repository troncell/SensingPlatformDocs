# Data Sources Reference

## Data source types

All data source types must be registered once in `SysConfig/DataActivators.xml`:

```xml
<DataSourceFactory>
  <Data ConfigType="DbData" AssemblyFile="Data.Common"
    TypeName="Data.Common.CommonDbDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="ExcelData" AssemblyFile="Data.Common"
    TypeName="Data.Common.ExcelDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.ExcelDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="FolderData" AssemblyFile="Data.Common"
    TypeName="Data.Common.FolderDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.FolderDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="XmlData" AssemblyFile="Data.Common"
    TypeName="Data.Common.CommonXmlDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.XmlDataSouceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="TimeLineData" AssemblyFile="UI.SweepPanel"
    TypeName="UI.SweepPanel.CollapsibleContentDataProvider, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="ExcelTimeLineData" AssemblyFile="UI.SweepPanel"
    TypeName="UI.SweepPanel.ExcelCollapsibleContentDataProvider, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.ExcelDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="DeepZoomData" AssemblyFile="Data.DeepZoom"
    TypeName="Data.DeepZoom.DeepZoomDataProvider, Data.DeepZoom, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common"
      TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="JObjectDataWebApi" AssemblyFile="Data.WebAPI"
    TypeName="Data.WebAPI.JObjectWebApiDataProvider, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.WebAPI"
      TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="JArrayDataWebApi" AssemblyFile="Data.WebAPI"
    TypeName="Data.WebAPI.JArrayWebApiDataProvider, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.WebAPI"
      TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="ActivityDataWebApi" AssemblyFile="Data.ExtendsWebApi"
    TypeName="Data.ExtendsWebApi.CategoryWebApiDataProvider, Data.ExtendsWebApi, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.WebAPI"
      TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
  <Data ConfigType="NavigationData" AssemblyFile="Data.Navigation"
    TypeName="Data.Navigation.NavigationDataProvider, Data.Navigation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Navigation"
      TypeName="Data.Navigation.NavigationSourceModel, Data.Navigation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
</DataSourceFactory>
```

## Per-app data source definition

Each data source is defined in `Shell/Data/Data.xml`:

```xml
<DataConfig>
  <DbData Name="BrandSqliteData">
    <AutoFreshData Enable="true" IntervalTime="00:00:20" />
    <CustomerConfig>
      <Tables>
        <Table Name="BehaviorUsers" IsRealtimeLoad="True">
          <DataQuery Value="select * from BehaviorUser" />
        </Table>
      </Tables>
      <DbConnection>
        <ConnectionString Value="Data Source={$BasePath}\BehaviorTarget.db3;Version=3;Pooling=True;Max Pool Size=100;" />
        <DbType>System.Data.SQLite.EF6</DbType>
      </DbConnection>
    </CustomerConfig>
  </DbData>

  <FolderData Name="FolderData">
    <CustomerConfig>
      <Folders>
        <Folder Name="Page" UriKind="Relative" Directory="Page" EnableListen="True" />
        <Folder Name="Detail" UriKind="Relative" Directory="Detail" />
      </Folders>
    </CustomerConfig>
  </FolderData>

  <ExcelData Name="GuideData">
    <CustomerConfig>
      <Excel UriKind="Relative" FileName="GuideData.xlsx" />
    </CustomerConfig>
  </ExcelData>

  <JObjectDataWebApi Name="ProductsData">
    <CustomerConfig>
      <WebApi>
        <ApiOptions BaseUrl="http://58.214.31.206:9300/" ApiUrl="/api/getmessage" />
        <CacheOptions IsCache="True" Directory="CacheData" JsonFile="message.json">
          <ResourceColumns></ResourceColumns>
        </CacheOptions>
      </WebApi>
    </CustomerConfig>
  </JObjectDataWebApi>
</DataConfig>
```

## DataProvider URL grammar

From a control, bind to a data source like this:

```xml
<DataProvider>DataSourceName?CSTable=TableName&amp;Where=[col like %Game%]&amp;Orderby=[DESC Name]&amp;Name=Google</DataProvider>
```

| Component | Meaning |
|---|---|
| `DataSourceName` | The `Name` attribute from `Data.xml` |
| `CSTable` | Table/Folder/Sheet name inside the data source |
| `Where=[...]` | Filter expression (square brackets required) |
| `Orderby=[...]` | Sort expression (square brackets required) |
| `CustomKey=Value` | Passed to dynamic SQL for `DbData` |

### Default path variables

| Variable | Value |
|---|---|
| `{$DataPath}` | `/Shell/Data` |
| `{$BasePath}` | `/Shell/Data/<DataName>` |

### Template selection

Controls with `<Items>` use `<Template>` children. `TemplateID` selects which template renders:

```xml
<Items IsCacheUI="True">
  <Template Left="0" Top="0" Width="1920" Height="1080" TemplateID="10001">
    <ImageElement Name="resource">
      <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
      <ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\{$ImageName}</ImageSource>
    </ImageElement>
  </Template>
</Items>
```

Conditional template selection:

```xml
<Template TemplateID="{$Name}==Google">...</Template>
```

## WebAPI caching

`JObjectDataWebApi` and `JArrayDataWebApi` support local file caching:

```xml
<CacheOptions IsCache="True" Directory="CacheData" JsonFile="message.json">
  <ResourceColumns></ResourceColumns>
</CacheOptions>
```
