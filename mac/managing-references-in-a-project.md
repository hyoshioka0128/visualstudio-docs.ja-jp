---
title: プロジェクト内の参照の管理
description: この記事では、Visual Studio for Mac でプロジェクト内の参照を管理する方法について説明します
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.assetid: 4AD51385-B0A8-4BA7-B2D4-BF2BD167A142
ms.topic: overview
ms.openlocfilehash: 28ea53826a19a9ec97349060702cf13c68342ad2
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938998"
---
# <a name="managing-references-in-a-project"></a>プロジェクト内の参照の管理

Visual Studio for Mac には、プロジェクトに参照を追加する方法が 2 つあります。

![プロジェクト参照](media/projects-and-solutions-image10.png)

これらのボタンの役割は、次のとおりです。

* 関連項目
* NuGet (パッケージ フォルダーで追加)

さらに、Web 参照とネイティブ参照は任意のプロジェクトに追加することもできます。

## <a name="assembly-references"></a>アセンブリ参照

Xamarin 内の各フレームワークには、十数個のアセンブリが付属しています。 これらのアセンブリ パッケージの一部は、プロジェクトの既定では参照されていません。

ご利用のプロジェクトで参照するパッケージを編集するには、 **[参照の編集]** ダイアログを使用します。このダイアログは、[参照] フォルダーをダブルクリックするか、コンテキスト メニュー操作で **[参照の編集]** を選択することで表示できます。

![アセンブリの参照ダイアログ](media/projects-and-solutions-image11.png)

各 Xamarin フレームワークで使用できるアセンブリについては、「[Available Assemblies](https://developer.xamarin.com/guides/cross-platform/advanced/available-assemblies/)」(使用可能なアセンブリ) ガイドを参照してください。

## <a name="nuget"></a>NuGet

NuGet は、.NET 開発用の最も人気のあるパッケージ マネージャーです。 Visual Studio for Mac は NuGet をサポートしているので、パッケージを検索してプロジェクトに追加することができます。

追加するには、Solution Pad で **[パッケージ]** フォルダーを右クリックし、[パッケージの追加] を選択します。

NuGet パッケージの使用方法については、「[Including a NuGet package in your Project](nuget-walkthrough.md)」(プロジェクトに NuGet パッケージを含める) チュートリアルを参照してください。

## <a name="see-also"></a>関連項目

- [参照の管理 (Windows の Visual Studio)](/visualstudio/ide/managing-references-in-a-project)
- [拡張 SDK と比較して NuGet を使用した参照の追加 (Windows の Visual Studio)](/visualstudio/ide/adding-references-using-nuget-versus-an-extension-sdk)