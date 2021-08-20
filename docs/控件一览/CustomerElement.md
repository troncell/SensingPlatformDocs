# 自定义控件（CustomerElement）

## 控件作用

可以根据自身需要，自定义一些特定的功能，它与相对布局控件一样，是个容器。




## 配置文件样例

```
<!-- 参考控件公用片段的讲解中UIDisplay片段讲解 -->
<UIDisplay Left="1300" Top="400" Width="27" Height="33" IsShow="True" ZIndex="1" UsePercent="False" />
```

```
<!-- AssemblyFile是使用到程序集(dll)的文件名称，TypeName是控件类名的全称 -->
<Activator AssemblyFile="DancingBubbles" TypeName="DancingBubbles.BlueBubble" />

```

## 配置说明
### 节点Activator
    
	决定了该特殊效果具体为哪种效果，确定该效果所使用到的程序集（dll）。

    	属性说明

			AssemblyFile：使用到程序集(dll)的文件名称

			TypeName：控件类名的全称



