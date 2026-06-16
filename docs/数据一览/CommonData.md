# Data.Common 数据源包

## 数据源用途

Data.Common 是平台最基础的数据源包，提供了多种常用数据源的 Provider 实现：

| ConfigType | Provider | 说明 |
| --- | --- | --- |
| DbData | `CommonDbDataProvider` | 数据库数据源，支持 SQLite、SQL Server 等。 |
| ExcelData | `ExcelDataProvider` | Excel 表格数据源。 |
| FolderData | `FolderDataProvider` | 文件夹文件数据源。 |
| XmlData | `CommonXmlDataProvider` | XML 文件数据源。 |

这些数据源需要在 `SysConfig/DataActivators.xml` 中注册后才能使用。

## 数据源注册

```xml
<DataSourceFactory>
  <Data ConfigType="DbData" AssemblyFile="Data.Common" TypeName="Data.Common.CommonDbDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.DbDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>

  <Data ConfigType="ExcelData" AssemblyFile="Data.Common" TypeName="Data.Common.ExcelDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.ExcelDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>

  <Data ConfigType="FolderData" AssemblyFile="Data.Common" TypeName="Data.Common.FolderDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.FolderDataSourceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>

  <Data ConfigType="XmlData" AssemblyFile="Data.Common" TypeName="Data.Common.CommonXmlDataProvider, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <ConfigModel AssemblyFile="Data.Common" TypeName="Data.Common.XmlDataSouceModel, Data.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Data>
</DataSourceFactory>
```

## 各数据源详细文档

- [DbData](DbData.md)
- [ExcelData](ExcelData.md)
- [FolderData](FolderData.md)
- [XmlData](XmlData.md)

## 通用特性

1. 所有数据源都支持通过 `DataProvider` 在控件中引用。
2. 都支持 `Where` 和 `OrderBy` 查询参数（部分数据源支持程度不同）。
3. 都支持 `AutoFreshData` 自动刷新机制（需要数据源 Provider 实现支持）。
4. 数据源文件默认存放在 `Shell/Data/{DataName}` 目录下，可使用 `{$BasePath}` 变量引用。

## 注意事项

1. 注册 `ConfigType` 名称需要与 `Data.xml` 中配置的元素名称一致。
2. 同一 `Data.xml` 中，不同数据源的 `Name` 不能重复。
3. 如果自定义数据源，也需要参考这种注册方式。
