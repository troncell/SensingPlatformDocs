# DbData数据源

## 数据源用途
主要用于配置数据库中的数据，通过数据库可以拿到动态的数据，目前使用比较多的就是SQLite的数据库，这种数据库一般用于双向数据交付，或者数据来源于第三方的数据库，本程序主要用于数据的显示。
TimeLineData仅作用于配置时间轴控件，配置方法和DbData一致。

## 数据的配置

```xml
  <TimeLineData Name="TryTimeLineData">
    <CustomerConfig>
      <DbConnection>
        <DbType>Microsoft.Data.Sqlite</DbType>
        <ConnectionString Value="Data Source={$BasePath}/{$DataSourcePath};">
          <Args DataSourcePath="TryTimeLineData.db3" />
        </ConnectionString>
      </DbConnection>
      <Tables ContentDataTable="Content" ContentData="TimelineContentData" ListData="TimelineListData" ListType="DateGenerator">
        <Table Name="Content">
          <Sql Value="select * from EventData order by Year,Month,Day" />
        </Table>
        <Table Name="List">
          <Sql Value="select * from EventData order by Year,Month,Day" />
          <RerferenceItem MinItem="2013" MaxItem="2018">
            <Column Name="Year" Value="2012" />
            <Column Name="Month" Value="01" />
            <Column Name="Day" Value="" />
          </RerferenceItem>
        </Table>
      </Tables>
    </CustomerConfig>
  </TimeLineData>
```

## 配置讲解

这种数据源以每个表中的第一行为Table的字段名，每个表下可有多个字段。

### Excel文件的配置
1. DbType，支持 System.Data.SQLite.EF6， System.Data.SqlClient，Microsoft.Data.Sqlite，如有需要其它的数据类型，请联系平台开发者。
2. Args，文件名
3. Table Name，表名
4. Sql Value，sql查询方式
5. MinItem，时间轴开始的年份
6. MaxItem，时间轴结束的年份

