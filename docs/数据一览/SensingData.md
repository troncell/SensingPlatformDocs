# FolderData 数据源

## 数据源用途

主要用于AppPod中的数据作为数据源，这种方式简单明了，比较直观。同时监听文件夹内的文件变化也可以拿到动态的文件，本配置用于文件夹的数据显示。

## 数据的配置

在文件 Data.xml 里添加，添加后同时需要在 Data 文件夹下有对应文件夹和子文件夹

```xml
<SensingData Name="SensingData">
    <CustomerConfig>
      <Tables>
        <Table Name = "Ads" Type = "Ads">
          <Sql Value="SkuId=[]" />
        </Table>
        <Table Name="Products" Type ="Products">
          <Sql Value="CategoryIds=[17295];" />
        </Table>
      </Tables>
    </CustomerConfig>
  </SensingData>
```


## 配置讲解