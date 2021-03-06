---
title: Xamarin Live Player 安装程序
description: 本文档介绍如何设置 Xamarin Live Player 和使用它来对正在运行的应用程序进行实时编辑。
ms.prod: xamarin
ms.assetid: 5DDF9203-8826-4B04-93F5-B8D07EDE3873
author: lobrien
ms.author: laobri
ms.date: 08/08/2018
ms.openlocfilehash: dd987b6d1a6db8e27544ddd95cdc219bb5f783b5
ms.sourcegitcommit: 7eed80186e23e6aff3ddbbf7ce5cd1fa20af1365
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/11/2018
ms.locfileid: "51526645"
---
# <a name="xamarin-live-player-setup"></a>Xamarin Live Player 安装程序

Xamarin Live Player，可以对您的应用程序进行实时编辑，并具有这些更改反映实时设备上。 Xamarin Live Player 应用-无需设置仿真程序或使用电缆将部署中运行你的代码 ！ 本文介绍如何设置 Xamarin Live Player。

![预览功能](~/media/shared/preview.png)

## <a name="1-get-the-android-app"></a>1.获取 Android 应用

Xamarin Live Player 现在可供从 Google Play 的 Android:

[ ![Google Play 上提供](install-images/google-play-badge.png)](https://play.google.com/store/apps/details?id=com.xamarin.live)

Xamarin Live Player 是可通过适用于 Android 设备没有 Google Play [HockeyApp](https://aka.ms/xlp-hockeyapp)分发。 此外，早期的预览版本为可以通过选择加入直接从 Google Play 安装 Android[测试程序](https://play.google.com/apps/testing/com.xamarin.live)

# <a name="visual-studiotabwindows"></a>[Visual Studio](#tab/windows)

## <a name="2-get-visual-studio-2017"></a>2.获取 Visual Studio 2017

Xamarin Live Player 需要：

- Visual Studio 2017 15.4年或更高版本。
- Visual Studio 计算机和同一 WiFi 网络上的设备。

## <a name="3-using-xamarin-live-player-for-the-first-time"></a>3.第一次使用 Xamarin Live Player

1. 打开**Visual Studio 2017**。
2. 转到**工具 > 选项...** ，然后选择**Xamarin > 其他**选项卡。
3. 刻度线**启用 Xamarin Live Player**:

    ![选中选项窗口中的启用 Xamarin Live Player 框](install-images/vs2017-options.png)

4. 创建或打开 Xamarin 项目 (或[示例](~/tools/live-player/samples.md))。
5. 选择**Live Player**设备列表中：

    ![设备列表包括 Xamarin Live Player 选项](install-images/devices-empty-windows.png)

    - 如果已具有配对设备，它将作为一个选项可用。
    - 否则系统将提示进行配对时所需的设备。

6. 按**运行**按钮或选择下列任一选项从**运行**或右键单击菜单：

    - **启动但不调试**– 你可以编辑该应用程序并在设备发生的更改，请参阅 （如进行更改并保存该文件，应用程序重新启动）。
    - **开始调试**– 你可以设置断点并检查变量，但不能编辑代码。

    或者，选择**工具 > Xamarin Live Player > 实时运行当前视图**，从中可以编辑该应用程序并在设备发生的更改，请参阅。 （而不是应用程序的主屏幕） 显示当前视图。

7. 如果已配对设备和设备上运行 Xamarin Live Player 应用，将立即执行的代码 ！

    如果配对设备没有，则将收到有关如何对设备的显示 QR 码：

    ![对设备窗口](install-images/manage-empty-windows.png)

    如果设备不能连接的配对，则可能会出现错误。

# <a name="visual-studio-for-mactabmacos"></a>[Visual Studio for Mac](#tab/macos)

## <a name="2-get-visual-studio-for-mac"></a>2.使 Visual Studio for Mac

Xamarin Live Player 需要：

- OS X 10.11，macOS 10.12，或更高版本
- Visual Studio for Mac
- Mac 和同一 WiFi 网络上的设备

## <a name="3-using-xamarin-live-player-for-the-first-time"></a>3.第一次使用 Xamarin Live Player

1. 打开**Visual Studio for Mac**。
2. 转到**Visual Studio > 首选项...** ，然后选择**项目 > Xamarin Live Player （预览）** 选项卡。
3. 刻度线**启用 Xamarin Live Player**:

    [![选中选项窗口中的启用 Xamarin Live Player 框](install-images/vsmac-options-sml.png)](install-images/vsmac-options.png#lightbox)

4. 创建或打开 Xamarin 项目 (或[示例](~/tools/live-player/samples.md))。
5. 选择**Live Player**设备列表中。

    ![设备列表包括 Xamarin Live Player 选项](install-images/devices.png)

    - 如果已具有配对设备，它将作为一个选项可用。
    - 否则系统将提示进行配对时所需的设备。
    - 选择**Xamarin Live Player 设备...** 来管理你想要使用 Xamarin Live Player 设备。

6. 按**运行**按钮或选择下列任一选项从**运行**或右键单击菜单：

    ![运行菜单选项](install-images/run-menu.png)

    - **启动但不调试**– 你可以编辑该应用程序并在设备发生的更改，请参阅 （如进行更改并保存该文件，应用程序重新启动）。
    - **开始调试**– 你可以设置断点并检查变量，但不能编辑代码。
    - **实时运行当前视图**– 你可以编辑该应用程序并在设备发生的更改，请参阅。 （而不是应用程序的主屏幕） 显示当前视图。

7. 如果已配对设备和设备上运行 Xamarin Live Player 应用，将立即执行的代码 ！

    如果配对设备没有，则将收到有关如何对设备的显示 QR 码：

    ![对设备窗口](install-images/manage-empty.png)

    如果设备不能连接的配对，则将出现错误：

    ![无法连接到设备的错误消息](install-images/error-cannot-connect.png)

-----

如果遇到任何问题或无法连接，请参阅[限制和故障排除](~/tools/live-player/troubleshooting.md)。

## <a name="related-links"></a>相关链接

- [限制](~/tools/live-player/limitations.md)
- [疑难解答](~/tools/live-player/troubleshooting.md)
- [Xamarin Live Player 示例](~/tools/live-player/samples.md)
