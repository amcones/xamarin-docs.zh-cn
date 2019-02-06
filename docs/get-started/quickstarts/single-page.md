---
title: 创建单页 Xamarin.Forms 应用程序
description: 本文介绍如何创建单页跨平台 Xamarin.Forms 应用程序，这样就可以输入的说明，并将其保存到设备的存储。
zone_pivot_groups: platform
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: E8CF05B1-54B9-428B-8518-D068837BD61E
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/02/2019
ms.openlocfilehash: 7696ece64da28f05bb15866214de4a7f1103d06f
ms.sourcegitcommit: 817d26585093cd180a36b28179eb354b0eb900b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55292796"
---
# <a name="create-a-single-page-xamarinforms-application"></a>创建单个页 Xamarin.Forms 应用程序

[![下载示例](~/media/shared/download.png)下载示例](https://developer.xamarin.com/samples/xamarin-forms/GetStarted/Notes/SinglePage/)

在此快速入门中，你将了解如何：

- 创建跨平台 Xamarin.Forms 应用程序。
- 定义用于使用可扩展应用程序标记语言 (XAML) 页的用户界面。
- 与 XAML 代码中的用户界面元素进行交互。

快速入门教程演示如何创建，可输入的说明，并将其保存到设备的存储的跨平台 Xamarin.Forms 应用程序。 最终的应用程序如下所示：

[![](single-page-images/screenshots-sml.png "便笺应用程序")](single-page-images/screenshots.png#lightbox "Notes Application")

::: zone pivot="windows"

### <a name="prerequisites"></a>预备知识

- Visual Studio 2017 （最新版本） 中，使用**使用.NET 的移动开发**安装工作负载。
- 了解C#。
- （可选）配对的 Mac 生成在 iOS 上的应用程序。

有关这些先决条件的详细信息，请参阅[安装 Xamarin](~/cross-platform/get-started/installation/index.md)。 有关将 Visual Studio 2017 连接到 Mac 生成主机的信息，请参阅[与适用于 Xamarin.iOS 开发的 Mac 配对](~/ios/get-started/installation/windows/connecting-to-mac/index.md)。

## <a name="get-started-with-visual-studio"></a>Visual Studio 入门

1. 启动 Visual Studio 中，并在开始页上单击**创建新项目...** 创建新项目：

    ![](single-page-images/vs/new-solution.png "新建项目")

2. 在“新建项目”对话框中，单击“跨平台”，选择“移动应用(Xamarin.Forms)”模板，将“名称”设为“便笺”，为项目选择合适的位置，然后单击“确定”按钮：

    ![](single-page-images/vs/new-project.png "跨平台项目模板")

    > [!IMPORTANT]
    > 本快速入门中的 C# 和 XAML 片段要求将解决方案命名为“便笺”。 使用不同的名称会导致：将本快速入门中的代码复制到解决方案中时出现生成错误。

3. 在“新的跨平台应用”对话框中，单击“空白应用”，选择“.NET Standard”作为代码共享策略，然后单击“确定”按钮：

    ![](single-page-images/vs/new-app.png "新的跨平台应用")

    有关创建.NET Standard 库的详细信息，请参阅[Xamarin.Forms 应用程序剖析](deepdive.md#anatomy-of-a-xamarinforms-application)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

4. 在“解决方案资源管理器”的“便笺”项目中，双击“MainPage.xaml”将其打开：

    ![](single-page-images/vs/open-mainpage-xaml.png "打开的 MainPage.xaml")

5. 在“MainPage.xaml”中，删除所有模板代码，替换为以下代码：

    ```xaml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 x:Class="Notes.MainPage">
        <StackLayout Margin="10,35,10,10">
            <Label Text="Notes"
                   HorizontalOptions="Center"
                   FontAttributes="Bold" />
            <Editor x:Name="editor"
                    Placeholder="Enter your note"
                    HeightRequest="100" />
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="*" />
                </Grid.ColumnDefinitions>
                <Button Text="Save"
                        Clicked="OnSaveButtonClicked" />
                <Button Grid.Column="1"
                        Text="Delete"
                        Clicked="OnDeleteButtonClicked"/>
            </Grid>
        </StackLayout>
    </ContentPage>
    ```

    该代码以声明的方式定义页面的用户界面，它包含一个用于显示文本的 [`Label`、](xref:Xamarin.Forms.Label)一个用于文本输入的 [`Editor`](xref:Xamarin.Forms.Editor) 以及两个指示应用程序保存或删除文件的 [`Button`](xref:Xamarin.Forms.Button) 实例。 这两个 `Button` 实例水平放置在 [`Grid`](xref:Xamarin.Forms.Grid) 中，而 `Label`、`Editor` 和 `Grid` 垂直放置在 [`StackLayout`](xref:Xamarin.Forms.StackLayout) 中。 有关创建用户界面的详细信息，请参阅[用户界面](deepdive.md#user-interface)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

    按 **Ctrl+S**，保存对 **MainPage.xaml** 所做的更改，然后关闭文件。

6. 在“解决方案资源管理器”的“便笺”项目中，展开“MainPage.xaml”，然后双击“MainPage.xaml.cs”将其打开：

    ![](single-page-images/vs/open-mainpage-codebehind.png "打开的 MainPage.xaml.cs")

7. 在“MainPage.xaml.cs”中，删除所有模板代码并将其替换为以下代码：

    ```csharp
    using System;
    using System.IO;
    using Xamarin.Forms;

    namespace Notes
    {
        public partial class MainPage : ContentPage
        {
            string _fileName = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData), "notes.txt");

            public MainPage()
            {
                InitializeComponent();

                if (File.Exists(_fileName))
                {
                    editor.Text = File.ReadAllText(_fileName);
                }
            }

            void OnSaveButtonClicked(object sender, EventArgs e)
            {
                File.WriteAllText(_fileName, editor.Text);
            }

            void OnDeleteButtonClicked(object sender, EventArgs e)
            {
                if (File.Exists(_fileName))
                {
                    File.Delete(_fileName);
                }
                editor.Text = string.Empty;
            }
        }
    }
    ```

    此代码定义一个 `_fileName` 字段，该字段引用名为 `notes.txt` 的文件，而该文件将便笺数据存储在应用程序的本地应用程序数据文件夹中。 如果有文件，则在执行页构造函数时读取文件并将其显示在 [`Editor`](xref:Xamarin.Forms.Editor) 中。 按“保存”[`Button`](xref:Xamarin.Forms.Button)时执行 `OnSaveButtonClicked` 事件处理程序，将 `Editor` 的内容保存到文件中。 按“删除”`Button` 时执行 `OnDeleteButtonClicked` 事件处理程序，删除该文件（前提是它存在）并删除 `Editor` 中的任何文本。 有关用户交互的详细信息，请参阅[响应用户交互](deepdive.md#responding-to-user-interaction)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

    按 **Ctrl+S**，保存对 **MainPage.xaml.cs** 所做的更改，然后关闭文件。

### <a name="building-the-quickstart"></a>生成快速入门

1. 在 Visual Studio 中，选择“生成”>“生成解决方案”菜单项（或按 F6）。 将生成解决方案，Visual Studio 状态栏中将显示一条成功消息：

      ![](single-page-images/vs/build-succeeded.png "生成已成功")

    如果发生错误，请重复前面的步骤并更正任何错误，直到成功生成解决方案。

2. 在 Visual Studio 工具栏中，按“开始”按钮（类似“播放”按钮的三角形按钮），启动所选 Android Emulator 内的应用程序：

    ![](single-page-images/vs/android-start.png "Visual Studio Android 工具栏")

    [![](single-page-images/vs/notes-android.png "在 Android 模拟器中的说明")](single-page-images/vs/notes-android-large.png#lightbox "Notes in the Android Simulator")

    输入便笺内容，然后按“保存”按钮。

    有关每个平台上启动应用程序的方式的详细信息，请参阅[启动每个平台上的应用程序](deepdive.md#launching-the-application-on-each-platform)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

    > [!NOTE]
    > 以下步骤仅供在拥有符合 Xamarin.Forms 开发系统要求的[配对 Mac](~/ios/get-started/installation/windows/connecting-to-mac/index.md)时执行。

3. 在 Visual Studio 工具栏中，右键单击“Notes.iOS”项目，然后选择“设为启动项目”。

      ![](single-page-images/vs/set-as-startup-project-ios.png "将 iOS 设为启动项目")

4. 在 Visual Studio 工具栏中，按“开始”按钮（类似“播放”按钮的三角形按钮），启动所选 [iOS 远程模拟器](~/tools/ios-simulator/index.md)内的应用程序：

    ![](single-page-images/vs/ios-start.png "Visual Studio iOS 工具栏")

    [![](single-page-images/vs/notes-ios.png "在 iOS 模拟器中的说明")](single-page-images/vs/notes-ios-large.png#lightbox "iOS 模拟器中的说明")

    输入便笺内容，然后按“保存”按钮。

    有关每个平台上启动应用程序的方式的详细信息，请参阅[启动每个平台上的应用程序](deepdive.md#launching-the-application-on-each-platform)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

::: zone-end
::: zone pivot="macos"

### <a name="prerequisites"></a>系统必备

- Visual Studio for Mac （最新发行版）、 iOS 和 Android 平台支持安装。
- Xcode （最新发行版）。
- 了解C#。

有关这些先决条件的详细信息，请参阅[安装 Xamarin](~/cross-platform/get-started/installation/index.md)。

## <a name="get-started-with-visual-studio-for-mac"></a>Visual Studio for Mac 入门

1. 启动 Visual Studio for Mac，然后在起始页上单击“新建项目...”创建新项目：

    ![](single-page-images/vsmac/new-project.png "新建解决方案")

2. 在“为新项目选择一个模板”对话框中，单击“多平台”>“应用”，选择“空白窗体应用”模板，然后单击“下一步”按钮：

    ![](single-page-images/vsmac/choose-template.png "选择模板")

3. 在“配置空白窗体应用”对话框中，将新应用命名为“便笺”，确保选中“使用 .NET Standard”单选按钮，然后单击“下一步”按钮：    

    ![](single-page-images/vsmac/configure-app.png "配置 Forms 应用程序")

4. 在“配置新空白窗体应用”对话框中，将“解决方案”和“项目”名称保留设置为“便笺”，为项目选择合适的位置，然后单击“创建”按钮创建项目：

    ![](single-page-images/vsmac/configure-project.png "配置 Forms 项目")

    > [!IMPORTANT]
    > 本快速入门中的 C# 和 XAML 片段要求将解决方案和项目都命名为“便笺”。 使用不同的名称会导致：将本快速入门中的代码复制到项目中时出现生成错误。

    有关创建.NET Standard 库的详细信息，请参阅[Xamarin.Forms 应用程序剖析](deepdive.md#anatomy-of-a-xamarinforms-application)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

5. 在“Solution Pad”的“便笺”项目中，双击“MainPage.xaml”将其打开：

    ![](single-page-images/vsmac/mainpage-xaml.png "MainPage.xaml")

6. 在“MainPage.xaml”中，删除所有模板代码，替换为以下代码：

    ```xaml
    <?xml version="1.0" encoding="utf-8"?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                 xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                 x:Class="Notes.MainPage">
        <StackLayout Margin="10,35,10,10">
            <Label Text="Notes"
                   HorizontalOptions="Center"
                   FontAttributes="Bold" />
            <Editor x:Name="editor"
                    Placeholder="Enter your note"
                    HeightRequest="100" />
            <Grid>
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="*" />
                    <ColumnDefinition Width="*" />
                </Grid.ColumnDefinitions>
                <Button Text="Save"
                        Clicked="OnSaveButtonClicked" />
                <Button Grid.Column="1"
                        Text="Delete"
                        Clicked="OnDeleteButtonClicked"/>
            </Grid>
        </StackLayout>
    </ContentPage>
    ```

    该代码以声明的方式定义页面的用户界面，它包含一个用于显示文本的 [`Label`、](xref:Xamarin.Forms.Label)一个用于文本输入的 [`Editor`](xref:Xamarin.Forms.Editor) 以及两个指示应用程序保存或删除文件的 [`Button`](xref:Xamarin.Forms.Button) 实例。 这两个 `Button` 实例水平放置在 [`Grid`](xref:Xamarin.Forms.Grid) 中，而 `Label`、`Editor` 和 `Grid` 垂直放置在 [`StackLayout`](xref:Xamarin.Forms.StackLayout) 中。 有关创建用户界面的详细信息，请参阅[用户界面](deepdive.md#user-interface)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

    通过选择“文件”>“保存”，或按 **&#8984; + S**，保存对 **MainPage.xaml** 所做的更改，然后关闭文件。

7. 在“Solution Pad”的“便笺”项目中，展开“MainPage.xaml”，然后双击“MainPage.xaml.cs”将其打开：

    ![](single-page-images/vsmac/mainpage-xaml-cs.png "MainPage.xaml.cs")

8. 在“MainPage.xaml.cs”中，删除所有模板代码并将其替换为以下代码：

    ```csharp
    using System;
    using System.IO;
    using Xamarin.Forms;

    namespace Notes
    {
        public partial class MainPage : ContentPage
        {
            string _fileName = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData), "notes.txt");

            public MainPage()
            {
                InitializeComponent();

                if (File.Exists(_fileName))
                {
                    editor.Text = File.ReadAllText(_fileName);
                }
            }

            void OnSaveButtonClicked(object sender, EventArgs e)
            {
                File.WriteAllText(_fileName, editor.Text);
            }

            void OnDeleteButtonClicked(object sender, EventArgs e)
            {
                if (File.Exists(_fileName))
                {
                    File.Delete(_fileName);
                }
                editor.Text = string.Empty;
            }
        }
    }
    ```

    此代码定义一个 `_fileName` 字段，该字段引用名为 `notes.txt` 的文件，而该文件将便笺数据存储在应用程序的本地应用程序数据文件夹中。 如果有文件，则在执行页构造函数时读取文件并将其显示在 [`Editor`](xref:Xamarin.Forms.Editor) 中。 按“保存”[`Button`](xref:Xamarin.Forms.Button)时执行 `OnSaveButtonClicked` 事件处理程序，将 `Editor` 的内容保存到文件中。 按“删除”`Button` 时执行 `OnDeleteButtonClicked` 事件处理程序，删除该文件（前提是它存在）并删除 `Editor` 中的任何文本。 有关用户交互的详细信息，请参阅[响应用户交互](deepdive.md#responding-to-user-interaction)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

    通过选择“文件”>“保存”，或按 **&#8984; + S**，保存对 **MainPage.xaml.cs** 所做的更改，然后关闭文件。

### <a name="building-the-quickstart"></a>生成快速入门

1. 在 Visual Studio for Mac 中，选择“生成”>“生成所有”菜单项，或按 **&#8984; + B**。 项目将生成，并在 Visual Studio for Mac 工具栏中显示一条成功消息。

      ![](single-page-images/vsmac/build-successful.png "生成成功")

    如果发生错误，请重复前面的步骤并更正任何错误，直到成功生成项目。

2. 在中**Solution Pad**，选择**Notes.iOS**项目，右键单击，并选择**设为启动项目**:

      ![](single-page-images/vsmac/set-startup-project-ios.png "将 iOS 设为启动项目")

3. 在 Visual Studio for Mac 工具栏中，按“开始”按钮（类似“播放”按钮的三角形按钮），启动所选 iOS 模拟器内的应用程序：

      ![](single-page-images/vsmac/start.png "Visual Studio for Mac 工具栏")

      [![](single-page-images/vsmac/notes-ios.png "在 iOS 模拟器中的说明")](single-page-images/vsmac/notes-ios-large.png#lightbox "iOS 模拟器中的说明")

    输入便笺内容，然后按“保存”按钮。

    有关每个平台上启动应用程序的方式的详细信息，请参阅[启动每个平台上的应用程序](deepdive.md#launching-the-application-on-each-platform)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

4. 在中**Solution Pad**，选择**Notes.Droid**项目，右键单击，并选择**设为启动项目**:

      ![](single-page-images/vsmac/set-startup-project-android.png "将 Android 设为启动项目")

5. 在 Visual Studio for Mac 工具栏中，按“开始”按钮（类似“播放”按钮的三角形按钮），启动所选 Android Emulator 内的应用程序：

      [![](single-page-images/vsmac/notes-android.png "在 Android 模拟器中的说明")](single-page-images/vsmac/notes-android-large.png#lightbox "Notes in the Android Simulator")

    输入便笺内容，然后按“保存”按钮。

    有关每个平台上启动应用程序的方式的详细信息，请参阅[启动每个平台上的应用程序](deepdive.md#launching-the-application-on-each-platform)中[Xamarin.Forms 快速入门的深入探讨](deepdive.md)。

::: zone-end

## <a name="next-steps"></a>后续步骤

在此快速入门中，你学习了如何：

- 创建跨平台 Xamarin.Forms 应用程序。
- 定义用于使用可扩展应用程序标记语言 (XAML) 页的用户界面。
- 与 XAML 代码中的用户界面元素进行交互。

若要打开此单页面应用程序到多页应用程序，请继续学习下一步的快速入门教程。

> [!div class="nextstepaction"]
> [下一页](multi-page.md)

## <a name="related-links"></a>相关链接

- [便笺（示例）](https://developer.xamarin.com/samples/xamarin-forms/GetStarted/Notes/SinglePage/)
- [Xamarin.Forms 快速入门的深入探讨](deepdive.md)
