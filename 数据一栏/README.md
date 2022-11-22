## SensingPlatform 的动态数据源配置

平台支持多种动态数据源，如DbData,ExcelData,FolderData,XmlData,JsonData等, 可以在SysConfig文件夹下的DataActivators.xml进行注册具体的可使用的数据源类型，同时也可自定义开发其它的数据源。具体的应用程序的数据源是在Data/Data.xml中进行配置的，具体的不同数据源的配置，请参考其它相关文档。      
*: Xml是区分大小写的，请特别注意

1. 数据源的注册
```xml
<?xml version="1.0" encoding="utf-8" ?>
<DataSourceFactory>
  <!--Data.Chart 数据源-->
  <Data ConfigType="BIData" AssemblyFile="Data.Chart" TypeName="Data.Chart.BIDataProvider, Data.Chart, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	<ConfigModel AssemblyFile="SensingPlatform.Foundation" TypeName="SensingPlatform.Foundation.DataAccessCenter.EmptyDataSouceModel, SensingPlatform.Foundation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
  <!--Data.Chart End-->
  
  <!--Data.Common 数据源-->
  <Data ConfigType="DbData" AssemblyFile="Data.Common" TypeName="Data.Common.CommonDbDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	<ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
  <Data ConfigType="XmlData" AssemblyFile="Data.Common" TypeName="Data.Common.CommonXmlDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	<ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.XmlDataSouceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
  <Data ConfigType="DeepZoomData" AssemblyFile="Data.DeepZoom" TypeName="Data.DeepZoom.DeepZoomDataProvider, Data.DeepZoom, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
     <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
  <Data ConfigType="TimeLineData" AssemblyFile="UI.SweepPanel" TypeName="UI.SweepPanel.CollapsibleContentDataProvider, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
     <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
    <Data ConfigType="ExcelTimeLineData" AssemblyFile="UI.SweepPanel" TypeName="UI.SweepPanel.ExcelCollapsibleContentDataProvider, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
     <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.ExcelDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
  <Data ConfigType="FolderData" AssemblyFile="Data.Common" TypeName="Data.Common.FolderDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
     <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.FolderDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
  <Data ConfigType="ExcelData" AssemblyFile="Data.Common" TypeName="Data.Common.ExcelDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
     <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.ExcelDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>

  <Data ConfigType="JObjectDataWebApi" AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.JObjectWebApiDataProvider, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>

  <Data ConfigType="JArrayDataWebApi" AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.JArrayWebApiDataProvider, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>
    <Data ConfigType="ActivityDataWebApi" AssemblyFile="Data.ExtendsWebApi" TypeName="Data.ExtendsWebApi.CategoryWebApiDataProvider, Data.ExtendsWebApi, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.WebAPI" TypeName="Data.WebAPI.WebApiCacheDataSourceModel, Data.WebAPI, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
  </Data>

	<Data ConfigType="NavigationData" AssemblyFile="Data.Navigation" TypeName="Data.Navigation.NavigationDataProvider, Data.Navigation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
		<ConfigModel AssemblyFile="Data.Navigation" TypeName="Data.Navigation.NavigationSourceModel, Data.Navigation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"></ConfigModel>
	</Data>
	<!--Data.Common End-->
</DataSourceFactory>
```

2. 数据源的配置参考

```xml
<?xml version="1.0" encoding="utf-8"?>
<DataConfig>
  <DbData>
  </DbData>
  <FolderData Name="FolderData">
    <CustomerConfig>
      <Folders>
        <Folder Name="Page" UriKind="Relative" Directory="Page" EnableListen="True"/>
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
        <ApiOptions BaseUrl="http://58.214.31.206:9300/" ApiUrl="/api/getmessage"></ApiOptions>
        <CacheOptions IsCache="True" Directory="CacheData" JsonFile="message.json">
            <ResourceColumns></ResourceColumns>
        </CacheOptions>
        </WebApi>
  </CustomerConfig>
</JObjectDataWebApi>

</DataConfig>
```

