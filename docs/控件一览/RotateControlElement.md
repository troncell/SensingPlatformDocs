# 图片旋转控件（RotateControlElement）

## 控件作用

在页面显示图片，可以点击拖动图片旋转。

## 控件UI效果

![Placeholder](../../images/RotateControlElement.png)

## 配置文件样例

```
<RotateControlElement>
  <UIDisplay Left="600" Top="450" Width="973" Height="913" IsShow="True" ZIndex="1" UsePercent="False" />
  <CustomerConfig>
    <RotateConfig Path="Images" Orientation="Y" Sensitivity="0.05" />
    <AutoRotate Value="True" Orientation="1" Duration="00:00:04" StartTime="2" />
  </CustomerConfig>
</RotateControlElement>



```
## 配置说明

### 节点CustomerConfig

    属性说明

        注：旋转方式读取文件夹的图片，顺序为图片的name，例如：image1.png → image2.png → image3.png   

        Path：图片的存放路径位置；

        Orientation：旋转方向，X或Y；

        Sensitivity：摩擦系数 默认是1 ，其值越大，移动越慢；

        Value：设置是否可以自动旋播放，其值为True或False；

        Orientation：设置为移动到上一张还是下一张图片,设置为1为移动到下一张图片，其它值为移动到上一张图片；

        Duration：为设置多长时间移动一圈，其值为时间型；

        StartTime：表示多久无人操作则开始自动旋转，其值为整数，单位为秒；

        




