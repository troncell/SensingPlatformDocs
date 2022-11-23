# SensingPlatform 的动态数据源配置

平台支持多种动态数据源，如DbData,ExcelData,FolderData,XmlData,JsonData等,同时还有一些特殊控件的数据源，BIData，DeepZoomData等 可以在SysConfig文件夹下的DataActivators.xml进行注册具体的可使用的数据源类型，同时也可自定义开发其它的数据源。具体的应用程序的数据源是在Data/Data.xml中进行配置的，具体的不同数据源的配置，请参考其它相关文档。      
*: Xml是区分大小写的，请特别注意

##  数据源的注册

所有的数据源类型，使用之前都需要在系统中提前进行注册。注册一次就可以了！
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

## 数据源的配置说明与参考
  1. 每个数据源必须又要唯一的名字
  2. 数据源的根目录为 /Shell/Data,默认变量为 --- {$DataPath}
  3. 每个数据源的相对目录为：/Shell/Data/[DataName]--{$BasePath}

```xml
<?xml version="1.0" encoding="utf-8"?>
<DataConfig>
<DbData Name="BrandSqliteData">
    <AutoFreshData Enable="true" IntervalTime="00:00:20"></AutoFreshData>
    <CustomerConfig>
      <Tables>
        <Table Name="BehaviorUsers" IsRealtimeLoad="True">
          <DataQuery Value="select * from BehaviorUser"></DataQuery>
        </Table>
      </Tables>
      <DbConnection>
        <ConnectionString Value="Data Source={$BasePath}\BehaviorTarget.db3;Version=3;Pooling=True;Max Pool Size=100;"></ConnectionString>
        <DbType>System.Data.SQLite.EF6</DbType>
        <Args>
          <Args Name="Loading" Value="True"/>
        </Args>
      </DbConnection>
    </CustomerConfig>
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

## 在控件中使用数据
1. 在控件中使用数据源，通过DataProvider来进行，因为数据源是数据的结合，一个在支持多个子元素的控件中，使用比较常见，如有配置Items/Controls等的控件中，通过Template模板，通过多条数据来实现动态加载子元素。
2. DataProvider中的配置值是一个典型的变种的Url结构(一般不包含协议、域名和端口)，它包含路径，以及后面的Query的键值对组成
3. 路径部分表示具体的数据源的名称，Query中的CSTable=Page的键值对，表示名称为Page的Table数据名称，Table有时为FolderData中的Folder/ExcelData中Sheet的名称等
4. Where=[col > 3] & OrderBy=[DESC COL]中的Where和OrderBy作为ExcelData中用户过滤和排序的默认关键字，其它的FolderData等也可以考虑跟进，目前没有进行支持
5. 其它的键值对可以用户自定义设置，用户传递到后方的动态SQL里面去，比较实用于DbData类型的数据源
6. 可以通过TemplateID来进行模板的选择，这是需要包含TemplateID列，同时TemplateID支持条件查询,如: TemplateID="{$Name}==Google", 表示Name字段的值为Google的时候用这个模板

```xml
//注意转义字符
<DataProvider>FolderData?CSTable=Page&Where=[col like %Game%]&Orderby=[DESC Name]&Name=Google</DataProvider>
```
参考例子，如下
```xml
<FlipViewElement Name="flipView">
		  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
		  <DataProvider>LUYEGroupData?CSTable=LUYEGroup</DataProvider>
		  <Items IsCacheUI="True">
			  <Template Left="0" Top="0" Width="1920" Height="1080" TemplateID="10001">	
		        <ImageElement Name="resource">
				  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" Opacity="1" IsUseCache="True" />
				  <ImageSource UriKind="Application">Shell\Pages\LUYEGroupPage\resource\{$Pic}</ImageSource>
			    </ImageElement>
			  </Template>
		  </Items>
		  <CustomerConfig>
			  <FlipView SliderFactor="0.2"> </FlipView>
		  </CustomerConfig>
	  </FlipViewElement>
```

