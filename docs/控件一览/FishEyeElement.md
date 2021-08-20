# 鱼眼控件（FishEyeElement）

## 控件作用

鱼眼控件可分为连接数据库动态生成鱼眼个数，和用户自定义鱼眼个数，主要用于展示图片集合。

## 控件UI效果
![Placeholder](../../images/FishEyeElement.png)


## 配置文件样例
```
<!-- Name为鱼眼控件在页面中的名字，为可选项 -->
<FishEyeElement Name="FishEye">
	<UIDisplay Left="200" Top="300" Width="1000" Height="500" IsShow="True" ZIndex="1" UsePercent="False" />
	<DataProvider>
		FishEyeData?CSTable=FishEye
	</DataProvider>
	<Items>
		<Template>
			<ImageElement>
				<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Application">
					{$IconPath}
				</ImageSource>
				<ClickEvent>
					{$EventAction}?Page={$NavigatePage}&amp;Args=imageButton
				</ClickEvent>
			</ImageElement>
			<!-- 放置CustomerConfig片段 -->
			<CustomerConfig>
				<!-- 放置FishEys片段，ItemGap是上面配置的各个Items中节点直接的间隙 -->
				<FishEye ItemGap="100">
				</FishEye>
				<!-- 放置AutoPlay片段，是自动播放，IdleTime等待在指定的时间内没有操作将会执行自动播放，单位是毫秒，Step是移动的速度 -->
				<AutoPlay IdleTime="10000" Step="3">
				</AutoPlay>
			</CustomerConfig>
		</Template>
	</Items>
</FishEyeElement>
```


## 配置说明
### 节点FishEye

    属性说明

        ItemGap：上面配置的各个Items中节点直接的间隙；

### 节点AutoPlay 

    只要放置该片段，就会自动播放。
    
    属性说明    

        IdleTime：等待在指定的时间内没有操作将会执行自动播放，单位是毫秒;

        Step：移动的速度。

