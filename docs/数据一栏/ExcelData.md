# ExcelData数据源

## 数据源用途

主要用Excel作为数据源, 这种方式功能比较强大，同时可维护能力强，用户上手也比较简单！

## 数据的配置

```xml
<ExcelData Name="GuideData">
    <CustomerConfig>
      <Excel UriKind="Relative" FileName="GuideData.xlsx" />
    </CustomerConfig>
  </ExcelData>
```

## 配置讲解

这种数据源以Excel中的每个Sheet作为Table,Sheet中的第一行为Table的字段名，可以理解一个Sheet就是一个数据表

### Excel文件的配置
1. UriKind，文件的路径类型，支持Relative/Application等
2. FileName，Excel的文件名