# 弹出框控件（PopupShowElement）

## 1.控件作用

弹出框控件主要用于更加详细地介绍页面中的内容。

通常情况每个页面的悬浮控件所使用的格式都是相同的(是否可以移动，是否可以改变大小)，所以一般会把悬浮控件的内容抽象出来放到公共的 xml 中，如果页面使用到悬浮控都会使用一段引用代码来引用控件的配置文件，引用代码写在调用悬浮控件的页面中。通常用于介绍页面中的某个元素、展示详情、放大图片等场景。

弹出框控件支持 `Control` 事件，用于控制弹出框的显示与隐藏。

## 2.适用场景

- 图片或内容详情放大展示
- 产品介绍、新闻详情弹窗
- 提示信息、帮助说明
- 需要覆盖在当前页面之上的悬浮内容

## 3.前置依赖

使用弹出框控件前，必须满足以下条件：

1. 项目目录中存在 `UI.SweepPanel.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `PopupShowElement`；
3. 准备弹出框的公共配置文件（如 `PopupShow.xml`）；
4. 准备各个弹出框内容 XML 文件（位于 `EventPath` 指定目录下）。

## 4.整体流程

使用弹出框控件涉及三个主要部分：

1. **页面中声明 `PopupShowElement`**：通过 `IncludeTemplate` 引用公共弹出框配置；
2. **公共弹出框配置**（如 `PopupShow.xml`）：定义弹出框的布局行为（可移动、可缩放、边界等）；
3. **触发弹出框**：通过 `ImageButton` 等控件的 `ClickEvent` 调用 `PopupEvent`，并指定 `EventID`；
4. **弹出框内容文件**：在 `EventPath` 目录下创建与 `EventID` 同名的文件夹和 XML 文件，定义弹出框显示的具体内容。

## 5.控件 UI 效果

![Placeholder](../images/PopupShowElement.png)

## 6.页面中声明弹出框

在调用弹出框的页面中，声明一个 `PopupShowElement` 并通过 `IncludeTemplate` 引用公共配置文件：

```xml
<PopupShowElement Name="PopItems">
<!--使用IncludeTemplate 表示使用引用控件 FileSource为所引用的文件，具体含义请参考控件公用片段的讲解中FileSource片段讲解-->
    <IncludeTemplate>
        <FileSource UriKind="Application">Resource\ CanMovePopup\PopupShow.xml</FileSource>
    </IncludeTemplate>
</PopupShowElement>
```

### 6.1 1IncludeTemplate 说明

| 节点         | 说明                     | 示例                                  |
| ------------ | ------------------------ | ------------------------------------- |
| `FileSource` | 引用的弹出框配置文件路径 | `Resource\CanMovePopup\PopupShow.xml` |
| `UriKind`    | 路径解析方式             | `Application`                         |

### 6.2公共弹出框配置

在 `FileSource` 指定的路径下创建 `PopupShow.xml`，定义弹出框的布局行为。

### 6.3可改变型弹出框

```xml
（在上述FileSource指定的文件夹下新建上述指定名称的xml文件，这里是PopupShow.xml，分为固定型和可改变型，第一种为可改变型，第二种为固定型）

<Template>
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="6" UsePercent="False"/>
    <CustomerConfig>
        <!--参考CanContraint是否为可变True/false BounceRect.X, BounceRect.Y为弹出框出现的位置，BounceRect.Width为碰撞宽度，BounceRect.Height为碰撞高度，MaxScale为放大最大倍数，MinScale为缩小最大倍数，ScaleMode为缩小到小于最小倍数的样式Disppear为消失  -->
        <LayoutManager LayoutType="PopupShowLayout" CanContraint="True" BounceRect.X="0" BounceRect.Y="0" BounceRect.Width="1920"  BounceRect.Height="1080" MaxScale="2" MinScale="0.45" ScaleMode="Disppear"></LayoutManager>
    </CustomerConfig>
</Template>
```

### 6.4固定型弹出框

```xml
<Template >
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="6" UsePercent="False"/>
    <CustomerConfig>
        <LayoutManager  CanMove="False" CanScale="False" MaxItemCount="1"></LayoutManager>
        <HotShowMappings></HotShowMappings>
    </CustomerConfig>
</Template>


```

### 6.5CustomerConfig 参数说明

1.LayoutManager 节点

| 属性                | 必填 | 说明                                     | 示例                           |
| ------------------- | ---- | ---------------------------------------- | ------------------------------ |
| `LayoutType`        | 否   | 布局类型，弹出框固定为 `PopupShowLayout` | `PopupShowLayout`              |
| `CanContraint`      | 否   | 弹出框是否可变（可缩放/移动）            | `True`、`False`                |
| `CanMove`           | 否   | 弹出框是否可以拖动                       | `False`                        |
| `CanScale`          | 否   | 弹出框是否可以缩放                       | `False`                        |
| `BounceRect.X`      | 否   | 弹出框出现的 X 位置                      | `0`                            |
| `BounceRect.Y`      | 否   | 弹出框出现的 Y 位置                      | `0`                            |
| `BounceRect.Width`  | 否   | 碰撞区域宽度                             | `1920`                         |
| `BounceRect.Height` | 否   | 碰撞区域高度                             | `1080`                         |
| `MaxScale`          | 否   | 放大最大倍数                             | `2`                            |
| `MinScale`          | 否   | 缩小最小倍数                             | `0.45`                         |
| `ScaleMode`         | 否   | 小于最小倍数时的行为                     | `Disppear`、`Normal`、`Bounce` |
| `MaxItemCount`      | 否   | 最大弹出项数量                           | `1`                            |

2.ScaleMode 取值说明

| 取值       | 说明                   |
| ---------- | ---------------------- |
| `Disppear` | 缩小时消失             |
| `Normal`   | 正常缩放，无特殊控制   |
| `Bounce`   | 缩放时带有弹性回弹效果 |

3.HotShowMappings 节点

`HotShowMappings` 用于配置热点映射，具体参数以实际版本为准。

## 7.调用弹出框

配置好弹出框后，通过按钮的 `ClickEvent` 调用 `PopupEvent` 来显示弹出框。

ImageButton 中 ClickEvent 属性进行调用弹出框，ClickEvent 中的参数属性请参照简单控件中 ImageButton 控件的配置中的属性，下面是截取一段 ClickEvent 进行说明

```xml
<ImageButton>
    <ClickEvent>PopupEvent?TargetPageName=BriefingPage&TargetControlName=PageLeftSecondShow&X=0&Y=0&Height=841&Width=1604&EventID=PageHotBigBookShow&UriKind=Application&EventPath=Shell\Pages\BriefingPage\Items\PopupItems\SecondSho&PageName={$PageName}</ClickEvent>
</ImageButton>

```

### 7.1参数说明

| 参数                | 必填 | 说明                             | 示例                                                  |
| ------------------- | ---- | -------------------------------- | ----------------------------------------------------- |
| `TargetPageName`    | 是   | 目标页面名称                     | `BriefingPage`                                        |
| `TargetControlName` | 是   | 目标弹出框控件名称               | `PageLeftSecondShow`                                  |
| `X`                 | 否   | 弹出框显示位置 X                 | `0`                                                   |
| `Y`                 | 否   | 弹出框显示位置 Y                 | `0`                                                   |
| `Height`            | 否   | 弹出框高度                       | `841`                                                 |
| `Width`             | 否   | 弹出框宽度                       | `1604`                                                |
| `EventID`           | 是   | 弹出框内容标识，对应内容文件夹名 | `PageHotBigBookShow`                                  |
| `UriKind`           | 是   | 路径解析方式                     | `Application`                                         |
| `EventPath`         | 是   | 弹出框内容文件所在目录           | `Shell\Pages\BriefingPage\Items\PopupItems\SecondSho` |

> 注意：事件 URL 中的 `&` 必须转义为 `&amp;`。

### 7.2弹出框内容文件

调用 `PopupEvent` 时，`EventID` 指定了弹出框内容的标识。需要在 `EventPath` 目录下创建与 `EventID` 同名的文件夹，并在该文件夹下创建同名 XML 文件。

### 7.3目录结构

```
Shell/
└── Pages/
    └── BriefingPage/
        └── Items/
            └── PopupItems/
                └── SecondSho/
                    └── PageHotBigBookShow/
                        └── PageHotBigBookShow.xml
```

### 7.4内容文件示例

`PageHotBigBookShow.xml` 的内容通常是一个 `SysPage`：

```xml
<Template>
    <SysPage>
        <!--参考 CommonElement.md 中 UIDisplay 片段讲解-->
        <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />

        <Controls>
            <!--关闭弹出框按钮-->
            <ImageButton>
                <UIDisplay Left="1480" Top="950" Width="158" Height="42" IsShow="True" ZIndex="5" UsePercent="False" />

                <ImageSource UriKind="Application">Resource\Picture\Others\close.png</ImageSource>

                <ClickEvent>ChangePopupState?State=Close&Args=imageButton</ClickEvent>
            </ImageButton>

            <!--其他弹出框内容控件-->
            <ImageElement>
                <UIDisplay Left="0" Top="0" Width="1604" Height="841" IsShow="True" ZIndex="1" UsePercent="False" />

                <ImageSource UriKind="Application">Shell\Pages\BriefingPage\resource\detail.png</ImageSource>
            </ImageElement>
        </Controls>
    </SysPage>
</Template>
```

## 8.关闭弹出框

### 8.1在弹出框内容文件中，通常使用 `ImageButton` 触发 `ChangePopupState` 事件关闭弹出框：

```xml
<ClickEvent>ChangePopupState?State=Close&Args=imageButton</ClickEvent>
```

| 参数    | 说明                         | 示例    |
| ------- | ---------------------------- | ------- |
| `State` | 弹出框状态，`Close` 表示关闭 | `Close` |

### 8.2控制弹出框显示与隐藏

弹出框控件支持 `Control` 事件，用于控制弹出框的显示和隐藏。

```xml
<ClickEvent>Control?TargetControlName=PopItems&Action=Show</ClickEvent>
```

| 参数                | 说明                               | 示例       |
| ------------------- | ---------------------------------- | ---------- |
| `TargetControlName` | 目标弹出框控件名称                 | `PopItems` |
| `Action`            | 操作类型，`Show` 显示，`Hide` 隐藏 | `Show`     |

## 9.UIControlDict.xml 添加弹出框控件

如果使用弹出框控件则需要在 UIControlDict.xml 中添加弹出框控件

```

  <Element ViewType="PopupShowElement" AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.PopupControl.PopupShowControl, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.PopupControl.PopupShowElementViewModel, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```

## 10.部署说明

1. 将 `UI.SweepPanel.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 创建公共弹出框配置文件（如 `Resource\CanMovePopup\PopupShow.xml`）；
4. 在页面 XML 中使用 `PopupShowElement` 引用公共配置；
5. 在 `EventPath` 目录下创建与 `EventID` 同名的文件夹和 XML 文件；
6. 在页面中添加触发 `PopupEvent` 的按钮。

## 11.常见问题

### 弹出框不显示

- 检查 `PopupShowElement` 的 `Name` 是否与 `PopupEvent` 中的 `TargetControlName` 一致；
- 检查 `EventPath` 和 `EventID` 是否正确；
- 检查弹出框内容文件是否存在于正确路径；
- 检查 `ZIndex` 是否过低被其他控件遮挡。

### 点击关闭按钮没有反应

- 检查关闭按钮的 `ClickEvent` 是否为 `ChangePopupState?State=Close`；
- 检查事件 URL 中的 `&` 是否已转义为 `&amp;`。

### 弹出框位置不对

- 调整 `PopupEvent` 中的 `X`、`Y`、`Width`、`Height`；
- 调整公共配置中的 `BounceRect.X`、`BounceRect.Y`。

### 弹出框无法移动或缩放

- 检查 `LayoutManager` 的 `CanMove` 和 `CanScale` 是否设为 `True`；
- 检查 `CanContraint` 是否配置正确。

### 弹出框内容显示异常

- 检查内容文件是否为有效的 `SysPage` 结构；
- 检查内容文件中的 `UIDisplay` 是否覆盖整个弹出框区域；
- 检查内容文件路径和文件名是否与 `EventID` 一致。

## 12.注意事项

- 弹出框内容文件必须放在 `EventPath\EventID\EventID.xml` 路径下；
- `PopupShowElement` 的 `ZIndex` 应设置较高，确保弹出框显示在其他控件之上；
- 事件 URL 中的特殊字符必须正确转义；
- 公共弹出框配置可被多个页面复用，建议统一管理。
