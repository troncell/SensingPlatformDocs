# ExcelData数据源

## 数据源用途

主要用Excel作为数据源, 这种方式功能比较强大，同时可维护能力强，用户上手也比较简单！
ExcelTimeLineData仅作用于配置时间轴控件，配置方法和ExcelData一致。

## 数据的配置

```xml
        <ExcelTimeLineData Name="sjzData">
    <CustomerConfig>
      <Excel UriKind="Relative" FileName="sjzData.xlsx" />
      <Tables ContentDataTable="Content" ContentData="TimelineContentData" ListData="TimelineListData" ListType="DateGenerator">
        <Table Name="Content">
          <Sql Value="orderby=[Year,Month,Day];from=[Content]" />
        </Table>
        <Table Name="List">
          <Sql Value="orderby=[Year,Month,Day];from=[Content]" />
          <RerferenceItem MinItem="2013" MaxItem="2018">
            <Column Name="Year" Value="2012" />
            <Column Name="Month" Value="01" />
            <Column Name="Day" Value="" />
          </RerferenceItem>
        </Table>
      </Tables>
    </CustomerConfig>
  </ExcelTimeLineData>
```

## 配置讲解

这种数据源以Excel中的每个Sheet作为Table,Sheet中的第一行为Table的字段名，可以理解一个Sheet就是一个数据表

### Excel文件的配置
1. UriKind，文件的路径类型，支持Relative/Application等
2. FileName，Excel的文件名
3. Table Name，表名
4. Sql Value，sql查询方式
5. MinItem，时间轴开始的年份
6. MaxItem，时间轴结束的年份

