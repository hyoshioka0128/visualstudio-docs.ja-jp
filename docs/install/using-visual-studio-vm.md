---
title: Azure 仮想マシンでの Visual Studio の使用
titleSuffix: ''
description: Azure 仮想マシンで Visual Studio を使用する方法を説明します
ms.date: 04/23/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- azure services
- virtual machine
- installation
- visual studio
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 6453c263cb970ae3fff2c134f1ae570bca730b93
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183237"
---
# <a name="visual-studio-images-on-azure"></a><a id="top"> </a> Azure 上の Visual Studio イメージ

構成済みの Azure 仮想マシン (VM) での Visual Studio の使用は、短時間で何もない状態から開発環境を稼働状態にする簡単な方法です。 Visual Studio の構成が異なるさまざまなシステム イメージを、[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/compute?filters=virtual-machine-images%3Bmicrosoft%3Bwindows&page=1&subcategories=application-infrastructure) で入手できます。

まだ Azure を使ったことがない場合は、 [無料の Azure アカウントを作成してください](https://azure.microsoft.com/free)。

## <a name="what-configurations-and-versions-are-available"></a>利用できる構成とバージョン

最新のメジャー バージョンである Visual Studio 2019、Visual Studio 2017、Visual Studio 2015 のイメージは、Azure Marketplace で見つけることができます。  リリースされたメジャー バージョンごとに、最初に "Web にリリースされた" (RTW) バージョンと最新の更新バージョンを確認できます。  それぞれのバージョンに、Visual Studio Enterprise Edition と Visual Studio Community Edition があります。  これらのイメージは少なくとも毎月更新され、Visual Studio と Windows の最新の更新プログラムが組み込まれます。  イメージの名前は同じままですが、各イメージの説明には、インストールされる製品バージョンとイメージの "更新" 日が含まれます。

| リリース バージョン                                                                                                                                          | エディション              |    製品バージョン    |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------:|:-----------------------:|
| [Visual Studio 2019:最新版 (バージョン 16.5)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftvisualstudio.visualstudio2019latest?tab=Overview) | Enterprise、Community | バージョン 16.5.4    |
| Visual Studio 2019:RTW                         | エンタープライズ            | バージョン 16.0.13    |
| Visual Studio 2017:最新 (バージョン 15.9)           | Enterprise、Community | バージョン 15.9.22   |
| Visual Studio 2017:RTW                             | Enterprise、Community | バージョン 15.0.28   |
| Visual Studio 2015:最新 (更新プログラム 3)              | Enterprise、Community | バージョン 14.0.25431.01 |

> [!NOTE]
> Microsoft のサービス ポリシーに従って、Visual Studio 2015 の最初にリリースされた (RTW) バージョンは、サービスの有効期限が切れています。 Visual Studio 2015 製品ラインに提供されるバージョンとして残っているのは Visual Studio 2015 Update 3 だけです。

詳細については、[Visual Studio サービス ポリシー](/visualstudio/productinfo/vs-servicing-vs)に関する説明を参照してください。

## <a name="what-features-are-installed"></a>インストールされる機能

各イメージには、その Visual Studio エディションの推奨される機能が含まれます。 一般に、インストールには次のものが含まれます。

* 利用可能なすべてのワークロードと、各ワークロードの推奨されるオプション コンポーネント
* .NET 4.6.2 と .NET 4.7 SDK、Targeting Pack、開発者ツール
* Visual F#
* Visual Studio 向け GitHub 拡張
* LINQ to SQL ツール

イメージをビルドするときの Visual Studio のインストールは、次のコマンド ラインを使用して行われます。

```shell
    vs_enterprise.exe --allWorkloads --includeRecommended --passive ^
       --add Microsoft.Net.Component.4.7.SDK ^
       --add Microsoft.Net.Component.4.7.TargetingPack ^
       --add Microsoft.Net.Component.4.6.2.SDK ^
       --add Microsoft.Net.Component.4.6.2.TargetingPack ^
       --add Microsoft.Net.ComponentGroup.4.7.DeveloperTools ^
       --add Microsoft.VisualStudio.Component.FSharp ^
       --add Component.GitHub.VisualStudio ^
       --add Microsoft.VisualStudio.Component.LinqToSql
```

必要な Visual Studio の機能がイメージに含まれない場合は、フィードバック ツール (ページの右上隅) を使ってそのことをフィードバックしてください。

## <a name="what-size-vm-should-i-choose"></a>VM のサイズの選択

Azure では、全サイズの仮想マシンを提供しています。 Visual Studio は高性能のマルチスレッド アプリケーションであるため、少なくとも 2 つのプロセッサと 7 GB のメモリを含む VM サイズが必要です。 Visual Studio イメージでは、次の VM サイズをお勧めします。

* Standard_D2_v3
* Standard_D2s_v3
* Standard_D4_v3
* Standard_D4s_v3
* Standard_D2_v2
* Standard_D2S_v2
* Standard_D3_v2

最新のマシンのサイズについては、「[Azure の Windows 仮想マシンのサイズ](/azure/virtual-machines/windows/sizes)」を参照してください。

Azure では、VM のサイズを変更することで、最初の選択を再調整できます。 より適切なサイズで新しい VM をプロビジョニングしたり、既存の VM のサイズを異なる基盤ハードウェアに合わせて変更したりできます。 詳細については、「[Windows VM のサイズ変更](/azure/virtual-machines/windows/resize-vm)」を参照してください。

## <a name="after-the-vm-is-running-whats-next"></a>VM 実行後の次の操作

Visual Studio は、Azure の "ライセンス持ち込み" モデルに従います。 専用ハードウェアへのインストールと同様に、最初に行うことの 1 つは、Visual Studio のインストールのライセンスを有効にすることです。 Visual Studio のロックを解除するには、次のいずれかを行います。
- Visual Studio サブスクリプションに関連付けられている Microsoft アカウントでサインインする
- 最初の購入に付属するプロダクト キーを使用して Visual Studio のロックを解除する

詳細については、「[Visual Studio にサインイン](../ide/signing-in-to-visual-studio.md)」および「[Visual Studio のロックを解除する方法](../ide/how-to-unlock-visual-studio.md)」を参照してください。

## <a name="how-do-i-save-the-development-vm-for-future-or-team-use"></a>将来の使用やチームが使用するために開発 VM を保存する方法

開発環境の範囲は広大であり、環境が複雑になるほどその構築にはコストがかかります。 環境の構成に関係なく、構成済みの VM を、将来使用するためやチームの他のメンバーのために "基本イメージ" として保存 (キャプチャ) できます。 その後は、新しい VM を起動するときに、Azure Marketplace イメージではなく基本イメージからプロビジョニングします。

簡単なまとめ:システム準備ツール (Sysprep) を使用して実行中の VM をシャットダウンし、Azure Portal の UI を使用して、VM をイメージとして "*キャプチャ (図 1)* " します。 Azure は、イメージを含む `.vhd` ファイルをユーザーが選んだストレージ アカウントに保存します。 その後、新しいイメージはサブスクリプションのリソース一覧にイメージ リソースとして表示されます。

![Azure portal の UI を使ってイメージをキャプチャする](media/capture-vm.png)

*(図 1) Azure portal の UI を使ってイメージをキャプチャします。*

詳細については、「[Azure で一般化された VM の管理対象イメージを作成する](/azure/virtual-machines/windows/capture-image-resource)」参照してください。

> [!IMPORTANT]
> 必ず Sysprep を使用して VM を準備してください。 そうしないと、Azure はイメージから VM をプロビジョニングできません。

> [!NOTE]
> イメージの保存にはやはり若干のコストがかかりますが、その増加分は、VM を必要とするチーム メンバーごとに、一から VM を再構築するためのオーバーヘッド コストに比べればたいしたことはないはずです。 たとえば、チーム全体で再利用可能な 127 GB のイメージを作成して 1 か月保存するには数ドルのコストがかかります。 ただし、そのコストは、各従業員が使うために適切に構成された開発用ボックスを構築して検証するために費やす従業員の作業時間数と比べればわずかなものです。

さらに、さまざまな開発構成や複数のコンピューター構成のように、開発タスクやテクノロジをさらに広げることが必要な場合があります。 Azure DevTest Labs を使用して、"ゴールデン イメージ" の構築を自動化する "_レシピ_" を作成できます。 DevTest Labs を使用して、チームが実行する VM のポリシーを管理することもできます。 「[開発者のための Azure DevTest Labs の使用](/azure/devtest-lab/devtest-lab-developer-lab)」は、DevTest Labs の詳細についての最適なソースです。

## <a name="next-steps"></a>次の手順

事前構成済みの Visual Studio イメージについて理解したので、次のステップは新しい VM の作成です。

* [Azure Portal で VM を作成する](/azure/virtual-machines/windows/quick-create-portal)
* [Windows の仮想マシンの概要](/azure/virtual-machines/windows/overview)
