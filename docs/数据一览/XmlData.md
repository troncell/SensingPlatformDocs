# XmlData数据源

## 数据源用途

主要用Xml作为数据源, 这种方式的通用性比较好一些，一些WebApi会采用这种格式的！

## 数据的配置

```xml
<DbData Name="XmlBrandData">
  <CustomerConfig>
    <Tables>
      <Table Name="BehaviorUsers">
        <DataQuery Value="Brands.xml"></DataQuery>
      </Table>
      <Table Name="Users">
        <DataQuery Value="Users.xml"></DataQuery>
      </Table>
    </Tables>
  </CustomerConfig>
</DbData>
```

## 配置讲解

这种数据源以Excel中的每个Sheet作为Table,Sheet中的第一行为Table的字段名，可以理解一个Sheet就是一个数据表

### Tables的配置

1. 支持多个Table的配置，通过Name来区分，Name不能相同
2. DataQuery表示Xml数据的文件名，这个Xml数据必须存放在当前的数据源目录下面
3. Xml的格式如下，其中带有Path的属性，会自动填充当前数据源的相对目录

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Config>
  <Items>
    <Item Name="William" Path=""></Item>
    <Item Name="William" Path=""></Item>
  </Items>
</Config>
```
