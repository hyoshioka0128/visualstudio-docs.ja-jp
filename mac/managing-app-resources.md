---
title: アプリ リソースの管理
description: この記事は、Visual Studio for Mac でさまざまなプラットフォーム用のアプリ リソースを管理する方法について説明した各種のガイドにリンクしています
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 61EAAB8F-3C32-4574-924F-CFC616604089
ms.openlocfilehash: c3572edc46d4f69a338ba655b32254126a7fce9c
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "67692858"
---
# <a name="managing-app-resources"></a>アプリ リソースの管理

アプリケーションには、画像、テキスト ファイル、オーディオ ファイルなどのアプリ リソース ファイルが必要ですが、これらはアプリケーションと共にコンパイルされません。 Visual Studio for Mac でサポートされる各プラットフォームでは、これらのリソースは、以下のガイドで説明するように、異なる方法で処理されます。

## <a name="xamarinforms"></a>Xamarin.Forms

Xamarin.Forms コードは複数のプラットフォームで実行されます。各プラットフォームには独自のファイル システムがあり、ファイルへの読み書き方法は各ファイル システムによって指示されます。 Xamarin.Forms では、各プラットフォームでネイティブのファイル API を使用するか、埋め込みリソースとしてファイルを追加することによって、アプリ リソースを管理できます。

* [イメージの処理](https://developer.xamarin.com/guides/xamarin-forms/user-interface/images/)
* [ファイルの処理]( https://developer.xamarin.com/guides/xamarin-forms/application-fundamentals/files/)

## <a name="xamarinios"></a>Xamarin.iOS

* [リソースの処理](https://developer.xamarin.com/guides/ios/application_fundamentals/working_with_resources/)
* [イメージの処理](https://developer.xamarin.com/guides/ios/application_fundamentals/working_with_images/)
* [ファイル システムの処理](https://developer.xamarin.com/guides/ios/application_fundamentals/working_with_the_file_system/)

## <a name="xamarinandroid"></a>Xamarin.Android

* [Android リソース](https://developer.xamarin.com/guides/android/application_fundamentals/resources_in_android/)

## <a name="xamarinmac"></a>Xamarin.Mac

* [イメージの処理](https://developer.xamarin.com/guides/mac/application_fundamentals/working-with-images/)

## <a name="see-also"></a>参照

- [アプリケーション リソースの管理 (Windows 上の Visual Studio)](/visualstudio/ide/managing-application-resources-dotnet)