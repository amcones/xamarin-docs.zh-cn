---
title: 在 Xamarin.Android 中的通知
ms.prod: xamarin
ms.assetid: 2E54F1D0-45F4-43A7-B3A3-4F483B7150CB
ms.technology: xamarin-android
author: conceptdev
ms.author: crdun
ms.date: 03/01/2018
ms.openlocfilehash: a0778de5dcc7e21ba011fe144be703b3b83b8247
ms.sourcegitcommit: e268fd44422d0bbc7c944a678e2cc633a0493122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50114036"
---
# <a name="notifications-in-xamarinandroid"></a>在 Xamarin.Android 中的通知


## <a name="overview"></a>概述

本部分介绍如何在 Xamarin.Android 中实现通知。 其中介绍了 Android 通知的各种 UI 元素，并讨论了 API 的涉及创建并显示一条通知。


## <a name="sections"></a>部分

### <a name="local-notifications-in-androidlocal-notificationsmd"></a>[在 Android 中的本地通知](local-notifications.md)

本部分介绍如何在 Xamarin.Android 中实现本地通知。 它介绍了 Android 通知的各种 UI 元素，并讨论了 API 的涉及创建并显示一条通知。 

### <a name="walkthrough---using-local-notifications-in-xamarinandroidlocal-notifications-walkthroughmd"></a>[演练-在 Xamarin.Android 中使用本地通知](local-notifications-walkthrough.md)  
 
本演练介绍如何在 Xamarin.Android 应用程序中使用本地通知。 它演示了创建和发布通知的基础知识。 当用户单击通知抽屉中的通知时在启动第二个活动。 


## <a name="for-further-reading"></a>其他阅读材料

[Firebase Cloud Messaging](~/android/data-cloud/google-messaging/firebase-cloud-messaging.md) &ndash; Firebase Cloud Messaging (FCM) 是一种便于移动应用和服务器应用程序之间的消息传送的服务。 Firebase Cloud Messaging 可用来实现远程通知 （也称为推送通知） 在 Xamarin.Android 应用程序中。

[通知](http://developer.android.com/guide/topics/ui/notifiers/notifications.html)&ndash;此 Android 开发人员主题是 Android 通知的权威指南。 它包括的设计注意事项部分，可帮助你设计您的通知，以便它们符合的 Android 用户界面的准则。 启动活动，该活动时，它提供有关 preserviing 导航的更多背景信息，并介绍如何在锁定屏幕上通知和控制媒体的播放中显示进度。 

[NotificationListenerService](https://developer.xamarin.com/api/type/Android.Service.Notification.NotificationListenerService/) &ndash;此 Android 服务使您的应用程序以侦听 （并与之交互） 的所有通知都发布在 Android 设备上，而不仅仅是您的应用程序注册到通知接收。 请注意，用户必须显式授予对您的应用程序，以便能够侦听的设备上的通知的权限。





## <a name="related-links"></a>相关链接

- [本地通知 （示例）](https://developer.xamarin.com/samples/monodroid/LocalNotifications/)
- [远程通知 （示例）](https://developer.xamarin.com/samples/monodroid/RemoteNotifications/)
