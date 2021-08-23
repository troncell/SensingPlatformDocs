# 正方体控件（Square3DElement）

## 控件作用

3D立方体主要以正方体的方式来展示图片。

## 控件UI效果

![Placeholder](../../images/Square3DElement.png)

## 配置文件样例

```
<Square3DElement>
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="false" />
    <DataProvider>IntroductionData?CSTable=AboutUs</DataProvider>
    <CustomerConfig>
        <Square3D>
            <Layout ItemWidth="420" ItemHeight="540" Row="1" Colum="5" SurfaceWidth="1.2" InitAngleX="18" InitAngleY="20" IntervalAngle="10"></Layout>
            <Zoom ZoomInZ="-2.5"></Zoom>
            <AnimationTime>400</AnimationTime>
        </Square3D>
    </CustomerConfig>
</Square3DElement>
```
## 配置说明

### 节点Layout

    属性说明

        ItemWidth:图片的宽度；

        ItemHeight：图片的高度；

        Row：一个面显示的行数；

        Colum：一个面显示的列数；

        SurfaceWidth：一个面显示的宽度（3D大小一般在0-4之间）

        InitAngleX：初始的X轴倾斜角度；

        InitAngleY：初始的Y轴倾斜角度；

        IntervalAngle：每个列倾斜的角度差。

### 节点Zoom  

    属性说明

        ZoomInZ：点击某个图像放大后摄像机移动的Z轴的距离（值越小放大倍数越大）

### 节点AnimationTime

    动画间隔时间 


