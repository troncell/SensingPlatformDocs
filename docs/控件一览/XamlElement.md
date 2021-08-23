# 包动画控件（XamlElement）

## 控件作用

包动画控件主要用一些动画来展示一些东西，使得界面更加生动。



## 配置文件样例

```
<XamlElement>
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080"  IsShow="True" ZIndex="5" UsePercent="False" />
    <Xaml>
        <!--<FileSource UriKind="Application">Shell\Pages\homepage\textblock.xml</FileSource>-->
		<Border
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" >

			<!-- 黄色代码 -->
			
            <Border.Background>
                <LinearGradientBrush>
                    <LinearGradientBrush.GradientStops>
                        <GradientStop Color="#FF008000" Offset="0" />
                        <GradientStop Color="#FF0000FF" Offset="0.5" />
                        <GradientStop Color="#FFFF0000" Offset="1" />
                    </LinearGradientBrush.GradientStops>
                </LinearGradientBrush>
            </Border.Background>
        </Border>		
		
		<!-- 黄色代码 -->
	
    </Xaml>
</XamlElement>   

```


## 配置说明

#### 注：黄色部分的代码在Blend中复制即可

