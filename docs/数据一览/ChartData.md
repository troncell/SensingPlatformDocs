# ChartData 数据源（BIData）

## 数据源用途

ChartData 用于为图表控件提供数据支持。它通过 SQL 查询数据库，生成图表（Chart）、表格（Grid）、标题（Title）等数据上下文。

## 数据源注册

在 `SysConfig/DataActivators.xml` 的 `DataSourceFactory` 节点中注册：

```xml
<Data ConfigType="BIData" AssemblyFile="Data.Chart" TypeName="Data.Chart.BIDataProvider, Data.Chart, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <ConfigModel AssemblyFile="SensingPlatform.Foundation" TypeName="SensingPlatform.Foundation.DataAccessCenter.EmptyDataSouceModel, SensingPlatform.Foundation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Data>
```

## 数据的配置

在 `Shell/Data/Data.xml` 里添加：

```xml
<BIData Name="ChartData">
  <CustomerConfig>
    <ChartConfigName>ChartData.xml</ChartConfigName>
    <PrecisionConfigName>PrecisionControl.xml</PrecisionConfigName>
    <CovertXvalueConfigName>CovertXvalueControl.xml</CovertXvalueConfigName>
  </CustomerConfig>
</BIData>
```

## 配置讲解

### CustomerConfig 节点

| 节点 | 说明 |
| --- | --- |
| ChartConfigName | 图表主配置文件名，位于当前数据源目录下。 |
| PrecisionConfigName | 数据精度控制配置文件名。 |
| CovertXvalueConfigName | X 轴值转换配置文件名。 |

### ChartData.xml 结构

ChartData.xml 包含 ChartDatas、DataProviders、GridDatas、RollDatas 等配置节：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Root>
  <DataProviders>
    <DataProvider Name="MainDb">
      <ConnectionString>Data Source={0};Version=3;</ConnectionString>
      <DBNamespace>System.Data.SQLite.EF6</DBNamespace>
      <DataFile>ChartData.db3</DataFile>
    </DataProvider>
  </DataProviders>

  <ChartDatas>
    <ChartData Name="SalesChart" Type="COLUMN">
      <XValue Type="string">MM-dd</XValue>
      <TitleData Type="sql" DataProvider="MainDb">
        select Title from SalesTitle where Id=1
      </TitleData>
      <MainData Type="sql" DataProvider="MainDb" NeedConvertXvalue="False">
        select Date as xvalue, Amount as yvalue from Sales
      </MainData>
    </ChartData>
  </ChartDatas>

  <GridDatas>
    <GridData Name="SalesGrid">
      <MainData Type="sql" DataProvider="MainDb" NeedPrecision="False">
        select * from Sales
      </MainData>
      <NullValue>-</NullValue>
    </GridData>
  </GridDatas>
</Root>
```

### ChartData 配置

| 属性 | 说明 |
| --- | --- |
| Name | 图表名称，供控件引用。 |
| Type | 图表类型，支持 `COLUMN`、`LINE`、`AREA`、`PIE`、`CANDLESTICK` 等。 |

### 子节点

| 节点 | 说明 |
| --- | --- |
| XValue | X 轴值配置，`Type` 支持 `date` 或 `string`，值为格式化字符串。 |
| TitleData | 图表标题数据，`Type` 支持 `sql`。 |
| MainData | 图表主数据，`Type` 支持 `sql`，`DataProvider` 指定数据源，`NeedConvertXvalue` 是否转换 X 轴值。 |

### GridData 配置

| 节点 | 说明 |
| --- | --- |
| MainData | 表格主数据，`Type` 支持 `sql`，`NeedPrecision` 是否进行精度控制。 |
| NullValue | 空值显示内容。 |

## 在页面中使用

ChartData 通常由 `UI.SensingChart` 控件消费，通过控件配置指定 `BIData` 名称和具体图表/表格名称。

```xml
<SensingChart Name="SalesChart">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
  <CustomerConfig>
    <ChartDataName>SalesChart</ChartDataName>
    <DataProvider>ChartData</DataProvider>
  </CustomerConfig>
</SensingChart>
```

## 注意事项

1. ChartData 需要数据库支持，目前主要使用 SQLite。
2. SQL 查询结果中，图表数据需要包含 `xvalue` 和 `yvalue` 列（蜡烛图需要 `yvalue1`、`yvalue2` 等）。
3. 精度控制和 X 轴转换配置文件可选，如果不需要可以配置为空文件。
4. 详细的图表控件使用请参考 [控件一览/SensingChartElement.md](../控件一览/SensingChartElement.md)。
