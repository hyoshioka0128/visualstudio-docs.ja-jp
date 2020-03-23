---
title: ビルド アクション
description: この記事では、C# プロジェクトで使用できるさまざまなビルド アクションについて説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.assetid: 5399BCB1-E317-4C7B-87B1-C531E985DE6E
ms.openlocfilehash: d089f38bd91eda2565f215e8d15a74cc119b8767
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "73714401"
---
# <a name="build-actions"></a>ビルド アクション

Visual Studio for Mac プロジェクト内のすべてのファイルに、ビルド アクションがあります。 ビルド アクションにより、ビルド時にファイルに発生する内容を制御します。 

>[!NOTE]
>このトピックは、Visual Studio for Mac に適用されます。 Windows での Visual Studio については、「[ビルド アクション](/visualstudio/ide/build-actions)」を参照してください。

## <a name="set-a-build-action"></a>ビルド アクションを設定する

Visual Studio for Mac でファイルのビルド アクションを設定するには、次に示すように、任意のファイルを右クリックし、 **[ビルド アクション]** を参照します。

![ソリューション エクスプローラーで [コンパイル] ビルド アクションを選択する](media/projects-and-solutions-image1.png)

このファイルのビルド アクションはフライアウト メニューに表示されます。 

## <a name="build-action-values"></a>ビルド アクションの値

Visual Studio for Mac でビルドできるプロジェクトの一般的なビルド アクションには次が含まれます。

|ビルド アクション | プロジェクトの種類 | Description |
|--|--|--|
| **Compile** | any | ファイルはソース ファイルとして C# コンパイラに渡されます。|
| **コンテンツ** | .NET、Xamarin | ASP.NET プロジェクトの場合、展開時に、これらのファイルはサイトの一部として含まれます。 Xamarin.iOS プロジェクトと Xamarin.Mac プロジェクトの場合、アプリ バンドルに含まれます。|
| **Embedded Resource** | .NET | ファイルは、アセンブリに埋め込むリソースとして C# コンパイラに渡されます。 [ 名前空間の ](/dotnet/api/system.reflection.assembly.getmanifestresourcestream)Assembly.GetManifestResourceStream`System.Reflection` を使用すると、アセンブリからファイルを読み取ることができます。|
| **なし** | any | このファイルはいかなる形でもビルドに含まれません。IDE から簡単にアクセスできるようにプロジェクトに含まれています。 この値は、"ReadMe" ファイルなどのドキュメント ファイルで使用できます。|

> [!NOTE]
> 特定のプロジェクトの種類に対して追加のビルド アクションを定義して、ビルドア クションのリストをプロジェクトの種類に基づくものにして、このリストに含まれない値が表示されるようにすることができます。  

Xamarin.iOS プロジェクトには、**BundleResource** ビルド アクションがあります。このアクションでは、アプリ バンドルの一環としてファイルを追加します。 Xamarin.Android 固有のビルド アクションに関する詳細は、[ビルド プロセス](/xamarin/android/deploy-test/building-apps/build-process#Build_Actions) ガイドでご覧いただけます。

ソリューション エクスプローラーでは複数のファイルを選択することもできます。ビルド アクションを一度に複数のファイルに設定できます。

## <a name="see-also"></a>参照

- [ビルド アクション (Windows 上の Visual Studio)](/visualstudio/ide/build-actions)