---
title: プロジェクトに NuGet パッケージを含める
description: このドキュメントでは、Xamarin プロジェクトに NuGet パッケージを含める方法について説明します。 パッケージの検索およびダウンロードの手順を説明し、IDE 統合機能の概要を示します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 04/14/2017
ms.assetid: 5C800815-0B13-4B27-B017-95FCEF1A0EA2
ms.custom: video
ms.openlocfilehash: 728a225f4a1d14af986039cae7cb2fc8a493ecc9
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74983308"
---
# <a name="include-a-nuget-package-in-your-project"></a>プロジェクトに NuGet パッケージを含める

NuGet は、.NET 開発用の最も一般的なパッケージ マネージャーであり、Visual Studio for Mac および Windows の Visual Studio に組み込まれています。 パッケージを検索し、Xamarin.iOS プロジェクトおよび Xamarin.Android プロジェクトにいずれかの IDE を使用して追加することができます。

この記事では、プロジェクトに NuGet パッケージを含める方法について説明し、プロセスをシームレスにするツール チェーンを示します。

## <a name="nuget-in-visual-studio-for-mac"></a>Visual Studio for Mac の NuGet

NuGet パッケージの機能を示すため、まず、新しいアプリケーションを作成して、それにパッケージを追加します。 次に、パッケージの管理に役立つ IDE 機能について説明します。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

まず、以下に示すように `HelloNuget` という名前のプロジェクトを作成します。 この例では iOS 用の単一ビュー アプリケーションのテンプレートを示していますが、サポートされているどのプロジェクト タイプでも動作します。

![新しい iOS プロジェクトを作成する](media/nuget-walkthrough-NewProject.png)

## <a name="adding-a-package"></a>パッケージの追加

Visual Studio for Mac でプロジェクトを開いた状態で、**Solution Pad** の **[パッケージ]** フォルダーを右クリックし、 **[パッケージを追加]** を選択します。

![新しい NuGet パッケージのコンテキスト アクションを追加する](media/nuget-walkthrough-PackagesMenu.png)

これで、 **[パッケージを追加]** ウィンドウが起動します。 ソース ドロップダウンが次のように `nuget.org` に設定されていることを確認します。

![ソース リスト ドロップダウン](media/nuget-walkthrough-Source.png)

ウィンドウが開くと、既定のパッケージ ソースである nuget.org のパッケージ リストが読み込まれます。最初の結果は次のようになります。

![Nuget パッケージのリスト](media/nuget-walkthrough-AddPackages1.png)

`azure` などの特定のパッケージを検索するには、右上隅の検索ボックスを使用します。 使用するパッケージが見つかったら、それを選択し、 **[パッケージを追加]** ボタンをクリックしてインストールを開始します。

[Azure の NuGet パッケージを追加する](media/nuget-walkthrough-AddPackages2.png)

パッケージはダウンロードされた後、プロジェクトに追加されます。 ソリューションは次のように変更されます。

* **[参照]** ノードには、NuGet パッケージの一部であるすべてのアセンブリのリストが含まれます。
* **[パッケージ]** ノードには、ダウンロードした各 NuGet パッケージが表示されます。 このリストのパッケージを更新したり、削除したりすることができます。
* **packages.config** ファイルはプロジェクトに追加されます。 この XML ファイルは、このプロジェクトで参照されるパッケージ パージョンを追跡するために IDE で使用されます。 このファイルを手動で編集しないでください。ただし、バージョン管理で保持する必要があります。 project.json ファイルを packages.config ファイルの代わりに使用できることに注意してください。 project.json ファイルは、NuGet 3 で導入された新しいパッケージ ファイル形式であり、推移的な復元をサポートします。 project.json の詳細については、[NuGet のドキュメント](/NuGet/Schema/Project-Json)を参照してください。 Visual Studio for Mac で project.json ファイルを使用する前に、project.json ファイルを手動で追加して、プロジェクトを閉じてから再度開く必要があります。

## <a name="using-nuget-packages"></a>NuGet パッケージの使用

NuGet パッケージが追加され、プロジェクト参照が更新されたら、他のプロジェクト参照の場合と同じように API に対してプログラミングできます。

必ず、必要な `using` ディレクティブをファイルの先頭に追加してください。

```csharp
using Newtonsoft.Json;
```

ほとんどの NuGet では、README や Nuget ソースへのプロジェクト ページ リンクなどの追加情報が提供されます。 通常は、[パッケージを追加] ページのパッケージの宣伝文にこのリンクが表示されます。

[プロジェクト ページ リンクを表示する](media/nuget-walkthrough-project-page.png)

<a name="Package_Updates" class="injected"></a>

## <a name="package-updates"></a>パッケージの更新

パッケージの更新は、すべて一度に行う ( **[パッケージ]** ノードを右クリックする) ことも、コンポーネントごとに個別に行うこともできます。

コンテキスト メニューにアクセスするには、次のように **[パッケージ]** を右クリックします。

![パッケージ メニュー](media/nuget-walkthrough-PackagesMenu.png)

* **[パッケージを追加]** - プロジェクトにさらにパッケージを追加するためのウィンドウが開きます。
* **[更新]** - 各パッケージのソース サーバーを確認し、新しいバージョンをダウンロードします。
* **[復元]** - 不足しているパッケージをダウンロードします (既存のパッケージを新しいバージョンに更新しません)。

更新オプションと復元オプションはソリューション レベルでも使用でき、ソリューション内のすべてのプロジェクトに影響します。

次のように、個々のパッケージを右クリックして、コンテキスト メニューにアクセスすることもできます。

![パッケージ メニュー](media/nuget-walkthrough-PackageMenu.png)

* **[バージョン番号]** - バージョン番号は無効になっているメニュー項目です。情報提供のみを目的としています。
* **[更新]** - ソース サーバーを確認し、新しいバージョン (存在する場合) をダウンロードします。
* **[削除]** - このプロジェクトからパッケージを削除し、プロジェクトの参照から関連するアセンブリを削除します。

## <a name="adding-package-sources"></a>パッケージ ソースの追加

インストール可能なパッケージが最初に nuget.org から取得されます。ただし、Visual Studio for Mac に他のパッケージの場所を追加することができます。 これは、開発中の独自の NuGet パッケージをテストする場合や、会社または組織内でプライベートの NuGet サーバーを使用する場合に便利です。

Visual Studio for Mac で、 **[Visual Studio]、[基本設定]、[NuGet]、[ソース]** の順に移動し、パッケージ ソースのリストを表示して編集します。 ソースはリモート サーバー (URL で指定) またはローカル ディレクトリである場合があります。

![パッケージ ソース](media/nuget-walkthrough-PackageSource.png)

**[追加]** をクリックして新しいソースをセットアップします。 パッケージ ソースのフレンドリ名と URL (またはファイル パス) を入力します。 ソースがセキュリティで保護された Web サーバーの場合は、ユーザー名とパスワードも入力します。それ以外の場合はこれらの項目を空白のままにします。

![パッケージ ソースを追加する](media/nuget-walkthrough-PackageSource2.png)

パッケージを検索する際に、以下のようにさまざまなソースを選択することができます。

![パッケージ ソースを追加する](media/nuget-walkthrough-PackageSource3.png)

## <a name="version-control"></a>バージョン コントロール

NuGet のドキュメントでは、[ソース管理にパッケージをコミットせずに NuGet を使用する方法](/nuget/consume-packages/packages-and-source-control)について説明しています。 ソース管理でバイナリおよび未使用の情報を格納しない場合は、自動的にサーバーからパッケージを復元するように Visual Studio for Mac を構成することができます。 これは、開発者が初めてソース管理からプロジェクトを取得するときに、Visual Studio for Mac が自動的に必要なパッケージをダウンロードしてインストールすることを意味します。

![パッケージを自動的に復元する](media/nuget-walkthrough-AutoRestore.png)

`packages` ディレクトリを追跡対象から除外する方法の詳細については、特定のソース管理のドキュメントを参照してください。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Using-NuGet/player]

## <a name="see-also"></a>関連項目

* [Visual Studio でパッケージをインストールして使用する (Windows)](/nuget/quickstart/install-and-use-a-package-in-visual-studio)
