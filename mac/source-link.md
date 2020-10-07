---
title: ソース リンクを使用した NuGet パッケージのデバッグ
description: この記事では、Visual Studio for Mac のソース リンク機能について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 12/16/2019
ms.assetid: 4bcb8acf-db50-4bd8-a48e-86248f00c90b
ms.openlocfilehash: 307196dc7e33d268c45a9bb126c002ad426c5558
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91583919"
---
# <a name="debugging-into-nuget-packages-with-source-link"></a>ソース リンクを使用した NuGet パッケージのデバッグ

ソース リンク テクノロジを使用すると、ソース ファイルへのリンクを含む .PDB が付属している NuGet から、.NET アセンブリのソース コードをデバッグできます。 ソース リンクは、開発者が NuGet パッケージを作成するときに実行され、アセンブリとパッケージの内部にソース管理メタデータが埋め込まれます。 Visual Studio for Mac でソース リンクを有効にすると、インストールしたパッケージでソース ファイルを利用できるかどうかが IDE によって検出されます。 その後、Visual Studio for Mac によってそのダウンロードが提案されます。これにより、パッケージ コードをステップ実行できます。 ソース リンクは Xamarin プロジェクトの Mono 基本クラス ライブラリでも動作し、.NET Framework コードも同様にステップ インできます。 ソース リンクからは、効率的なデバッグを可能にするソース コントロール メタデータが提供されます。

> [!NOTE]
> 現在、Visual Studio for Mac ではシンボル サーバーはサポートされていません。 このため、シンボル サーバー上でホストされるメタデータを使用したソース リンクはサポートされていません。

## <a name="enable-source-link"></a>ソース リンクを有効にする

Visual Studio for Mac でソース リンクを有効にするには、 **[Visual Studio] > [ユーザー設定...] > [デバッガー]** の順に移動し、 **[Step into external code]\(外部コードにステップ イン\)** チェックボックスがオンになっていることを確認します。

![[Step into external code]\(外部コードにステップ イン\) チェックボックスを示すユーザー設定ダイアログのスクリーンショット](media/source-link1.png)

必要に応じて、 **[外部コードのダウンロード]** の設定を変更できます。
* 確認:Visual Studio for Mac により外部コードをダウンロードするように求められます
* 常に:Visual Studio for Mac により自動的に外部コードがダウンロードされます
* 使用しない:Visual Studio for Mac では関連する外部コードがダウンロードされません

既定では、 **[確認]** が選択されています。 NuGet パッケージの外部コードが検出されると、次のプロンプトが表示されます。

![NuGet パッケージの外部コードが検出されたときに表示されるプロンプトのスクリーンショット](media/source-link2.png)


## <a name="see-also"></a>関連項目

- [ソース リンクの GitHub リポジトリ](https://github.com/dotnet/sourcelink/blob/master/README.md)
- ソース リンクおよびソース リンクのサポートをパッケージに追加する方法に関する [.NET ドキュメント](/dotnet/standard/library-guidance/sourcelink)