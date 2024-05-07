# ExcelData 数据源

## 数据源用途

主要用 Excel 作为数据源, 这种方式功能比较强大，同时可维护能力强，用户上手也比较简单！
ExcelTimeLineData 仅作用于配置时间轴控件，配置方法和 ExcelData 一致。

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

这种数据源以 Excel 中的每个 Sheet 作为 Table,Sheet 中的第一行为 Table 的字段名，可以理解一个 Sheet 就是一个数据表

### Excel 文件的配置

1. UriKind，文件的路径类型，支持 Relative/Application 等
2. FileName，Excel 的文件名
3. Table Name，表名
4. Sql Value，sql 查询方式
5. MinItem，时间轴开始的年份
6. MaxItem，时间轴结束的年份
