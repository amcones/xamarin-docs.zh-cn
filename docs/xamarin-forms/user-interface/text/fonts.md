---
title: 在 Xamarin.Forms 中的字体
description: 本文介绍如何在 Xamarin.Forms 应用程序中显示文本的控件上指定字体信息。
ms.prod: xamarin
ms.assetid: 49DD2249-C575-41AE-AE06-08F890FD6031
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 05/22/2017
ms.openlocfilehash: 1b90a3184b89ba9147525a87b52e048bbb59f5af
ms.sourcegitcommit: be6f6a8f77679bb9675077ed25b5d2c753580b74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2018
ms.locfileid: "53061141"
---
# <a name="fonts-in-xamarinforms"></a>在 Xamarin.Forms 中的字体

[![下载示例](~/media/shared/download.png)下载示例](https://developer.xamarin.com/samples/xamarin-forms/WorkingWithFonts/)

本文介绍了 Xamarin.Forms 如何允许您指定的字体特性 （包括权重和大小） 上显示文本的控件。 字体信息可以是[在代码中指定](#Setting_Font_in_Code)或[在 XAML 中指定](#Setting_Font_in_Xaml)。
它也是可以使用[自定义字体](#Using_a_Custom_Font)。

<a name="Setting_Font_in_Code" />

## <a name="setting-font-in-code"></a>在代码中设置字体

使用任何控件的显示文本的三个与字体相关的属性：

- **FontFamily** &ndash; `string`字体名称。
- **FontSize** &ndash;形式的字体大小`double`。
- **FontAttributes** &ndash;一个字符串，指定样式信息，如*斜体*并**加粗**(使用`FontAttributes`C# 中的枚举)。

此代码演示如何创建一个标签，并指定的字体大小和权重来显示：

```csharp
var about = new Label {
    FontSize = Device.GetNamedSize (NamedSize.Medium, typeof(Label)),
    FontAttributes = FontAttributes.Bold,
    Text = "Medium Bold Font"
};
```

<a name="FontSize" />

### <a name="font-size"></a>字号

`FontSize`属性可以设置为双精度值，例如：

```csharp
label.FontSize = 24;
```

此外可以使用`NamedSize`枚举具有四个内置选项;Xamarin.Forms 选择每个平台的最佳大小。

-  **Micro**
-  **小**
-  **中等**
-  **大型**

`NamedSize`枚举可以是任何位置使用`FontSize`可以使用指定`Device.GetNamedSize`方法将值转换为`double`:

```csharp
label.FontSize = Device.GetNamedSize(NamedSize.Small, typeof(Label));
```

<a name="FontAttributes" />

### <a name="font-attributes"></a>字体特性

字体样式等**粗体**并*斜体*可以设置`FontAttributes`属性。 目前支持以下值：

-  **无**
-  **加粗**
-  **斜体**

`FontAttribute`可以按如下所示使用枚举 (您可以指定单个属性或`OR`它们组合在一起):

```csharp
label.FontAttributes = FontAttributes.Bold | FontAttributes.Italic;
```

### <a name="setting-font-info-per-platform"></a>设置每个平台的字体信息

或者，`Device.RuntimePlatform`属性可以用于设置不同的字体名称在每个平台上，此代码中所示：

```csharp
label.FontFamily = Device.RuntimePlatform == Device.iOS ? "Lobster-Regular" :
   Device.RuntimePlatform == Device.Android ? "Lobster-Regular.ttf#Lobster-Regular" : "Assets/Fonts/Lobster-Regular.ttf#Lobster",
label.FontSize = Device.RuntimePlatform == Device.iOS ? 24 :
   Device.RuntimePlatform == Device.Android ? Device.GetNamedSize(NamedSize.Medium, label) : Device.GetNamedSize(NamedSize.Large, label);
```

是一个很好的适用于 iOS 的字体信息的来源[iosfonts.com](http://iosfonts.com)。

<a name="Setting_Font_in_Xaml" />

## <a name="setting-the-font-in-xaml"></a>在 XAML 中设置该字体

Xamarin.Forms 控制所有具有该显示文本`Font`可以在 XAML 中设置的属性。 在 XAML 中设置该字体的最简单方法是使用命名的大小的枚举值，在此示例中所示：

```xaml
<Label Text="Login" FontSize="Large"/>
<Label Text="Instructions" FontSize="Small"/>
```

没有内置的转换器，用于`Font`允许所有字体设置表示为 XAML 中的字符串值的属性。 下面的示例演示如何可以在 XAML 中指定的字体属性和大小：

```xaml
<Label Text="Italics are supported" FontAttributes="Italic" />
<Label Text="Biggest NamedSize" FontSize="Large" />
<Label Text="Use size 72" FontSize="72" />
```

若要指定多个`Font`设置，将合并到单个所需的设置`Font`属性字符串。 字体属性字符串的格式应为`"[font-face],[attributes],[size]"`。 参数的顺序很重要，所有参数都是可选的并且多个`attributes`可以指定，例如：

```xaml
<Label Text="Small bold text" Font="Bold, Micro" />
<Label Text="Medium custom font" Font="MarkerFelt-Thin, 42" />
<Label Text="Really big bold and italic text" Font="Bold, Italic, 72"  />
```

[`Device.RuntimePlatform`](~/xamarin-forms/platform/device.md#providing-platform-values) 此外可在 XAML 中呈现每个平台上不同的字体。 下面的示例在 iOS 上使用自定义字体 (<span style="font-family:MarkerFelt-Thin">MarkerFelt 精简</span>)，并在其他平台上指定仅大小/属性：

```xaml
<Label Text="Hello Forms with XAML">
    <Label.FontFamily>
        <OnPlatform x:TypeArguments="x:String">
                <On Platform="iOS" Value="MarkerFelt-Thin" />
                <On Platform="Android" Value="Lobster-Regular.ttf#Lobster-Regular" />
                <On Platform="UWP" Value="Assets/Fonts/Lobster-Regular.ttf#Lobster" />
        </OnPlatform>
    </Label.FontFamily>
</Label>
```

指定自定义字体，它是始终使用一个好办法`OnPlatform`，因为很难找到可在所有平台的字体。

<a name="Using_a_Custom_Font" />

## <a name="using-a-custom-font"></a>使用自定义字体

使用非内置字样的字体，则需要一些特定于平台的编码。 此屏幕截图显示自定义字体**Lobster**从[Google 的开放源代码字体](https://www.google.com/fonts)呈现使用 Xamarin.Forms。

 [![IOS 和 Android 上的自定义字体](fonts-images/custom-sml.png "自定义字体示例")](fonts-images/custom.png#lightbox "自定义字体示例")

为每个平台所需的步骤如下所述。 包含与应用程序的自定义字体文件时，请务必验证字体的许可证进行分发。

### <a name="ios"></a>iOS

可以通过首先确保将加载它，然后使用 Xamarin.Forms 按名称引用它来显示自定义字体`Font`方法。
按照中的说明[这篇博客文章](http://blog.xamarin.com/custom-fonts-in-ios/):

1. 添加字体文件**生成操作： BundleResource**，和
2. 更新**Info.plist**文件 (**提供的应用程序字体**，或`UIAppFonts`、 密钥)，然后
3. 它按名称引用任何在 Xamarin.Forms 中定义一种字体位置 ！

```csharp
new Label
{
    Text = "Hello, Forms!",
    FontFamily = Device.RuntimePlatform == Device.iOS ? "Lobster-Regular" : null // set only for iOS
}
```

### <a name="android"></a>Android

适用于 Android 的 Xamarin.Forms 可以引用按照特定的命名标准添加到项目的自定义字体。 首先添加字体文件的**资产**文件夹中的应用程序项目并设置*生成操作： AndroidAsset*。 然后，使用的完整路径和*字体名称*，作为在 Xamarin.Forms 中，字体名称的哈希 （#） 分隔，如以下代码段演示了：

```csharp
new Label
{
  Text = "Hello, Forms!",
  FontFamily = Device.RuntimePlatform == Device.Android ? "Lobster-Regular.ttf#Lobster-Regular" : null // set only for Android
}
```

### <a name="windows"></a>Windows

适用于 Windows 平台的 Xamarin.Forms 可以引用按照特定的命名标准添加到项目的自定义字体。 首先添加字体文件的 **/Assets 字体/** 文件夹中的应用程序项目并设置<span class="UIItem">生成操作： 内容</span>。 然后，使用的完整路径和字体文件名后, 跟哈希 （#） 和<span class="UIItem">字体名称</span>，如以下代码段所示：

```csharp
new Label
{
    Text = "Hello, Forms!",
    FontFamily = Device.RuntimePlatform == Device.UWP ? "Assets/Fonts/Lobster-Regular.ttf#Lobster" : null // set only for UWP apps
}
```

> [!NOTE]
> 请注意，但使用的字体文件名称和字体名称可能不同。 若要发现 Windows 上的字体名称，右键单击.ttf 文件，然后选择**预览版**。 然后可以从预览窗口中确定的字体名称。

此时完成了应用程序的常用代码。 此时，可将特定于平台的电话拨号程序实现为 [DependencyService](~/xamarin-forms/app-fundamentals/dependency-service/index.md)。

### <a name="xaml"></a>XAML

此外可以使用[ `Device.RuntimePlatform` ](~/xamarin-forms/platform/device.md#providing-platform-values)中 XAML 呈现自定义字体：

```xaml
<Label Text="Hello Forms with XAML">
    <Label.FontFamily>
        <OnPlatform x:TypeArguments="x:String">
                <On Platform="iOS" Value="Lobster-Regular" />
                <On Platform="Android" Value="Lobster-Regular.ttf#Lobster-Regular" />
                <On Platform="UWP" Value="Assets/Fonts/Lobster-Regular.ttf#Lobster" />
        </OnPlatform>
    </Label.FontFamily>
</Label>
```

<a name="Summary" />

## <a name="summary"></a>总结

Xamarin.Forms 提供了简单的默认设置，以便你可以轻松地为所有支持的平台的文本的大小。 它还允许你指定的字体和大小&ndash;甚至以不同方式为每个平台&ndash;需要更精细的控制时。

此外可以使用格式正确的字体属性的 XAML 中指定字体信息。

## <a name="related-links"></a>相关链接

- [FontsSample](https://developer.xamarin.com/samples/xamarin-forms/WorkingWithFonts/)
- [文本 （示例）](https://developer.xamarin.com/samples/xamarin-forms/UserInterface/Text/)
