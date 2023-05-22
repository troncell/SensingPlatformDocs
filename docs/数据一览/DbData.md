# DbData数据源

## 数据源用途
主要用于配置数据库中的数据，通过数据库可以拿到动态的数据，目前使用比较多的就是SQLite的数据库，这种数据库一般用于双向数据交付，或者数据来源于第三方的数据库，本程序主要用于数据的显示。

## 数据的配置

```xml
<DbData Name="BrandSqliteData">
  <AutoFreshData Enable="True" IntervalTime="00:00:20"></AutoFreshData>
  <CustomerConfig>
    <Tables>
      <Table Name="BehaviorUsers" IsRealtimeLoad="True">
        <DataQuery Value="select * from BehaviorUser limit 1"></DataQuery>
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
```

## 配置讲解

整个配置分为两个大类，一个是数据库的配置，一个是Table的配置,以及更高级的自动数据刷新功能
### 数据库的配置
1.  DbType支持 System.Data.SQLite.EF6 和 System.Data.SqlClient两种，如有需要其它的数据类型，请联系平台开发者。
2. 链接字符串支持变量的替换，系统自带两个默认的{$DataPath}和{$BasePath}； 其中DataPath为应用Data的根目录，不包Name的文件架，BasePath是包含Name的文件夹，推荐使用BasePath变量。 如果数据第三方已经准备好了，可以使用绝对目录配置。另外Args支持Name和Value的变量替换。
### Tables的配置
1. 支持多个Table的配置，通过Name来区分，Name不能相同
2. IsRealtimeLoad支持True和False，True表示数据是每次动态加载的，比如弹出框的数据，由于数据源数据变化，这样弹出的内容就会动态的变化，False表示不动态加载，程序启动的时候进行预加载，后面使用的时候使用缓存的，不更新数据。
3. DataQuery表示数据的查询SQL(当然可以是任意SQL,如果不清楚SQL请不要乱写），同时DataQuery支持动态的变量，支持从DataProvier进行传入，这样的话就可以实现加载动态的数据，要实现这个功能，IsRealtimeLoad必须为True。

### 数据源定制更新
1. AutoFreshData节点，主要用于通知消费这个数据源的UI进行数据更新，从而用新的数据更新UI, 一般用于数据源会第三方的系统进行更新，从而我们的应用也进行刷新的应用场景，此时IsRealtimeLoad需要同时启用，才起作用。
2. Enable是是否启用定时刷新机制，
3. IntervalTime是数据定时更新的时间，采用hh:MM:ss的格式，如1分40秒刷新一次，写成"00:01:30"，注意Enable为True时，这个时间才有效.

