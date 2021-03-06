---
title: Microsoft 分发的 Mobile OpenJDK
description: 逐步介绍了如何配置适用于移动开发的 Microsoft 分发的 OpenJDK，并进行疑难解答。
ms.prod: xamarin
ms.assetid: B5F8503D-F4D1-44CB-8B29-187D1E20C979
ms.technology: xamarin-android
author: vyedin
ms.author: vyedin
ms.date: 07/22/2018
ms.openlocfilehash: aad88ad883dea1e0430a047a71a2c191195efffe
ms.sourcegitcommit: 2f6a5c1abf90fbdb0475fd8a3ce6de3cd7c7d575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52459897"
---
# <a name="microsofts-mobile-openjdk-distribution"></a>Microsoft 分发的 Mobile OpenJDK

_本指南介绍切换到 OpenJDK 内部分发的步骤。此分发适用于移动开发。_

## <a name="overview"></a>概述

自 Visual Studio 15.9 和 Visual Studio for Mac 7.7 起，Visual Studio Tools for Xamarin 已从 Oracle JDK 迁移到仅用于 Android 开发的 OpenJDK 轻型版本。 此次迁移是必需的，因为 Oracle 将于 2019 年终止对 JDK 8 的商业分发的支持，而 JDK 8 是所有 Android 开发的必需依赖项。

此迁移带来以下优势：

- 始终拥有适用于 Android 开发的 OpenJDK 版本。

- 下载 Oracle 的 JDK 9 或更高版本不会影响开发体验。

- 减少了下载大小和占用空间。

- 第三方服务器和安装程序不再出现问题。

若要更快地迁移到改进后体验，可以使用 Microsoft 分发的 Mobile OpenJDK 内部版本在 Windows 和 Mac 上进行测试。 下面介绍了具体设置过程，随时可以还原回 Oracle JDK。

## <a name="download"></a>下载

如果在 Windows 上的 Visual Studio 安装程序中选择 Android SDK 包，则会自动为你安装 Mobile OpenJDK 分发。 对于已选择 Android SDK 的用户，该分发将包含在 15.9 的更新中。

在 Mac 上，将安装 Mobile OpenJDK，作为新安装的 Android 工作负载的一部分。 对于现有 Visual Studio for Mac 用户，系统将提示你将其作为 7.7 更新的一部分进行安装。 IDE 会提示你移动到新的 JDK，并在下次重启时切换为使用该 JDK。

## <a name="troubleshooting"></a>疑难解答

如果在 Mac 或 Windows 上设置时遇到问题，可以按照以下步骤进行手动设置：

检查是否已在计算机上的正确位置安装 OpenJDK：

- **Mac** &ndash; **$HOME/Library/Developer/Xamarin/jdk/microsoft_dist_openjdk_1.8.0.9**
- **Windows** &ndash; **C:\\Program Files\\Android\\jdk\\microsoft_dist_openjdk_1.8.0.9**

如果此路径为空，则可以下载以下其中一个包：

- **Mac** &ndash; https://dl.xamarin.com/OpenJDK/mac/microsoft-dist-openjdk-1.8.0.9.zip
- **Windows x86** &ndash; https://dl.xamarin.com/OpenJDK/win32/microsoft-dist-openjdk-1.8.0.9.zip
- **Windows x64** &ndash; https://dl.xamarin.com/OpenJDK/win64/microsoft-dist-openjdk-1.8.0.9.zip

将 IDE 定目标到新 JDK：

- **Mac** &ndash; 依次单击“工具 > SDK 管理器 > 位置”，并将“Java SDK (JDK)位置”更改为 OpenJDK 安装的完整路径。 在以下示例中，此路径设置为“$HOME/Library/Developer/Xamarin/jdk/microsoft_dist_openjdk_1.8.0.9”。

![在 Mac 上设置 Microsoft 分发的 Mobile OpenJDK 的 JDK 路径](openjdk-images/vsm.png)

- **Windows** &ndash; 依次单击“工具 > 选项 > Xamarin > Android 设置”，并将“Java 开发工具包位置”设置为 OpenJDK 安装的完整路径。 在以下示例中，此路径设置为“C:\\Program Files\\Android\\jdk\\microsoft_dist_openjdk_1.8.0.9”：

![在 Windows 上设置 Microsoft 分发的 Mobile OpenJDK 的 JDK 路径](openjdk-images/vs.png)

## <a name="known-issues"></a>已知问题

### <a name="package-openjdkv1regkeyversion1809chipx64-failed-to-install"></a>包“OpenJDKV1.RegKey,version=1.8.0.9,chip=x64”安装失败

某些公司环境中可能存在这一问题。 计算机上已具有 OpenJDK - 请按照[上述疑难解答步骤](#troubleshooting)将 IDE 指向正确位置。 可以在[此处](https://developercommunity.visualstudio.com/content/problem/382549/packageidopenjdkv1regkeypackageactioninstallreturn.html)跟踪问题的状态。

### <a name="unknown-update-type-zip-when-upgrading-visual-studio-for-mac-to-77"></a>将 Visual Studio for Mac 升级到 7.7 时出现“未知更新类型: zip”

如果尝试将较旧版本的 Visual Studio for Mac 升级到 7.7，则可能出现此问题。 若要解决此问题，请取消选中更新程序中的 OpenJDK，安装更新的其余部分，然后再次检查更新以获取 OpenJDK 包。 如果仍遇到问题，可以按照[上述疑难解答步骤](#troubleshooting)手动安装 OpenJDK。 如果遇到此问题，请提交附有日志的 bug 文件。

## <a name="summary"></a>总结

本文介绍了如何配置 IDE 以使用 Microsoft 分发的 Mobile OpenJDK，以及在遇到问题时如何进行故障排除。
