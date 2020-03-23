---
title: FxCop アナライザーのインストール
ms.date: 08/03/2018
ms.topic: conceptual
helpviewer_keywords:
- fxcop analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 1d734ea4d87dc5d1b8f2ca7f1a1891a4cf7d512b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508772"
---
# <a name="install-fxcop-analyzers-in-visual-studio"></a>ビジュアル スタジオでの FxCop アナライザーのインストール

マイクロソフトは、レガシ分析から最も重要な[「FxCop」](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)ルールを含むアナライザーのセットを作成しました。 これらのアナライザーは、コードのセキュリティ、パフォーマンス、および設計上の問題などをチェックします。

これらの FxCop アナライザーは、NuGet パッケージとして、または Visual Studio の VSIX 拡張機能としてインストールできます。 それぞれの長所と短所について詳しくは[、「NuGet パッケージと VSIX 拡張機能](roslyn-analyzers-overview.md#nuget-package-versus-vsix-extension)」をご覧ください。

## <a name="nuget-package"></a>NuGet パッケージ

::: moniker range=">=vs-2019"

Visual Studio 2019 バージョン 16.3 以降では、プロジェクトの[コード分析](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)プロパティ ページから直接パッケージをインストールできます。

1. **ソリューション エクスプローラ**でプロジェクト ノードを右クリックし、[**プロパティ]** をクリックして、[**コード分析**] タブを選択します。

   ![Visual Studio のプロパティ ページから FxCop アナライザー パッケージをインストールします。](media/install-fxcop-properties-page.png)

2. **[インストール]** を選びます。

   パッケージの最新バージョンをインストールします。 アセンブリは **、ソリューション エクスプローラー**の **[参照** > **アナライザ]** の下に表示されます。

   ![ソリューション エクスプローラーの [アナライザー] ノード](media/solution-explorer-analyzers-node.png)

Visual Studio 2019 の古いバージョンを使用している場合は、[パッケージ マネージャー コンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)またはパッケージ[マネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)を使用してパッケージをインストールします。

::: moniker-end

::: moniker range="vs-2017"

1. Visual Studio のバージョンに基づいて、インストール[するアナライザー パッケージ](#fxcopanalyzers-package-versions)のバージョンを決定します。

2. [パッケージ マネージャー コンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)またはパッケージ マネージャー UI を使用して Visual Studio で[パッケージ](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)をインストールします。

   > [!NOTE]
   > 各アナライザ パッケージのnuget.orgページには、**パッケージ マネージャ コンソール**に貼り付けるコマンドが表示されます。 クリップボードにテキストをコピーするための便利なボタンもあります。
   >
   > ![パッケージ マネージャ コンソール コマンドを示すNuGet.orgページ](media/nuget-package-manager-command.png)

   アナライザー アセンブリがインストールされ、**ソリューション エクスプローラー**の **[参照**>**アナライザ]** の下に表示されます。

::: moniker-end

### <a name="custom-installation"></a>カスタム インストール

カスタム インストールの場合は、たとえば、パッケージの別のバージョンを指定するには、プロジェクトの [コード分析] プロパティ ページで省略記号 (..) ボタンを選択します。 このボタンは、検索文字列として "Microsoft.CodeAnalysis.FxCopAnalyzers" を使用して NuGet パッケージ マネージャーを開きます。

![カスタム FxCop アナライザー パッケージをインストールするプロパティ ページから Visual Studio](media/install-fxcop-properties-page-ellipsis.png)

> [!TIP]
> Visual Studio のバージョンに基づいて、インストール[するアナライザー パッケージ](#fxcopanalyzers-package-versions)のバージョンを決定します。 パッケージ[マネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)からパッケージをインストールすることもできます。

### <a name="fxcopanalyzers-package-versions"></a>パッケージバージョン

次のガイドラインを使用して、Visual Studio のバージョンにインストールする FxCop アナライザー パッケージのバージョンを決定します。

| Visual Studio のバージョン | FxCop アナライザー パッケージ バージョン |
| - | - |
| 2019 (すべてのバージョン)<br />Visual Studio 2017 バージョン 15.8 以降 | [最新](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) |
| Visual Studio 2017 バージョン 15.5 から 15.7 | [2.6.3](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.3) |
| Visual Studio 2017 バージョン 15.3 から 15.4 | [2.3.0-beta1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.3.0-beta1) |
| Visual Studio 2017 バージョン 15.0 から 15.2 | [2.0.0-ベータ2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.0.0-beta2) |
| ビジュアル スタジオ 2015 の更新プログラム 2 と 3 | [1.2.0-ベータ2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.2.0-beta2) |
| Visual Studio 2015 更新プログラム 1 | [1.1.0](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.1.0) |
| Visual Studio 2015 RTW | [1.0.1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.0.1) |

## <a name="vsix"></a>VSIX

::: moniker range="vs-2017"

Visual Studio 2017 バージョン 15.5 以降では、マネージ プロジェクトのすべての FxCop アナライザーを含む[Microsoft コード分析 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)年の拡張機能をインストールできます。

1. Visual Studio で、[**ツール**>**の拡張機能と更新]** を選択します。

   **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > または、拡張機能を[Visual Studio マーケットプレース](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)から直接ダウンロードします。

2. 左側のウィンドウで **[オンライン**] を展開し **、[Visual Studio マーケットプレース**] を選択します。

3. 検索ボックスに「コード分析」と入力し **、Microsoft コード分析 2017**年の拡張機能を探します。

   ![マイクロソフト コード分析 2017 年の拡張機能](media/extensions-and-updates-code-analysis.png)

::: moniker-end

::: moniker range=">=vs-2019"

[Microsoft コード分析 2019](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)年の拡張機能には、マネージ プロジェクトのすべての FxCop アナライザーが含まれています。 この拡張機能をインストールするには、次の手順に従います。

1. Visual Studio で、[**拡張機能**>の**管理] を**選択します。

   [**拡張機能の管理**] ダイアログ ボックスが開きます。

   > [!NOTE]
   > または、拡張機能を[Visual Studio マーケットプレース](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)から直接ダウンロードします。

2. 左側のウィンドウで **[オンライン**] を展開し **、[Visual Studio マーケットプレース**] を選択します。

3. 検索ボックスに「コード分析」と入力し **、Microsoft コード分析 2019**年の拡張機能を探します。

   ![マイクロソフト コード分析 2019 年の拡張機能](media/manage-extensions-code-analysis.png)

::: moniker-end

4. [**ダウンロード ]** を選択します。

   拡張機能がダウンロードされます。

5. **[OK] を**選択してダイアログ ボックスを閉じ、Visual Studio のすべてのインスタンスを閉じて**VSIX インストーラー**を起動します。

   **[VSIX インストーラー** ] ダイアログ ボックスが開きます。

   ::: moniker range="vs-2017"

   ![マイクロソフトコード分析用の VSIX インストーラー](media/vsix-installer-code-analysis.png)

   ::: moniker-end

6. [**変更]** を選択してインストールを開始します。

   1、2 分後にインストールが完了します。

7. [**閉じる**] を選択し、もう一度 Visual Studio を開きます。

::: moniker range="vs-2017"

拡張機能がインストールされているかどうかを確認する場合は、[**ツール** > **の拡張機能と更新]** を選択します。 [**拡張機能と更新プログラム**] ダイアログ ボックスで、左側の [**インストール済み**] カテゴリを選択し、名前で拡張子を検索します。

::: moniker-end

::: moniker range=">=vs-2019"

拡張機能がインストールされているかどうかを確認する場合は、[**拡張機能** > の**管理]** を選択します。 [**拡張機能の管理**] ダイアログ ボックスで、左側の [**インストール済み**] カテゴリを選択し、名前で拡張子を検索します。

::: moniker-end

## <a name="see-also"></a>関連項目

- [コード アナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)
- [レガシ分析からコード アナライザへの移行](../code-quality/migrate-from-legacy-analysis-to-fxcop-analyzers.md)
