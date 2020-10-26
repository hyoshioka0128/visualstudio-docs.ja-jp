---
title: FxCop アナライザーのインストール
ms.date: 08/03/2018
ms.topic: how-to
helpviewer_keywords:
- fxcop analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: d789299212ec7420f40135dd655056f16b6e4f35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88893347"
---
# <a name="install-fxcop-analyzers-in-visual-studio"></a>Visual Studio で FxCop アナライザーをインストールする

Microsoft は、従来の分析から最も重要な "FxCop" ルールを含む、 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)という名前のアナライザーのセットを作成しました。 これらのアナライザーは、セキュリティ、パフォーマンス、および設計上の問題についてコードをチェックします。

これらの FxCop アナライザーは、NuGet パッケージとして、または Visual Studio の VSIX 拡張機能としてインストールできます。 それぞれの長所と短所については、 [NuGet パッケージと VSIX 拡張機能](roslyn-analyzers-overview.md#nuget-package-versus-vsix-extension)に関するページを参照してください。

## <a name="nuget-package"></a>NuGet パッケージ

::: moniker range=">=vs-2019"

Visual Studio 2019 バージョン16.3 以降では、プロジェクトの [コード分析のプロパティ] ページから直接 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet パッケージをインストールできます。

1. **ソリューションエクスプローラー**でプロジェクトノードを右クリックし、[**プロパティ**] をクリックして、[**コード分析**] タブを選択します。

   ![Visual Studio の [プロパティ] ページから FxCop アナライザーパッケージをインストールする](media/install-fxcop-properties-page.png)

2. **[インストール]** を選択します。

   Visual Studio によって、FxCopAnalyzers パッケージの最新バージョンがインストールされます。 アセンブリは、[**参照**] [アナライザー] の下の**ソリューションエクスプローラー**に表示され  >  **Analyzers**ます。

   ![ソリューションエクスプローラーのアナライザーノード](media/solution-explorer-analyzers-node.png)

以前のバージョンの Visual Studio 2019 を使用している場合は、パッケージ [マネージャーコンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) または [パッケージマネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)のいずれかを使用してパッケージをインストールします。

::: moniker-end

::: moniker range="vs-2017"

1. 使用している Visual Studio のバージョンに基づいて、インストールする[アナライザーパッケージのバージョンを決定](#fxcopanalyzers-package-versions)します。

2. パッケージ [マネージャーコンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) または [パッケージマネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)を使用して、Visual Studio にパッケージをインストールします。

   > [!NOTE]
   > 各アナライザーパッケージの [nuget.org] ページには、 **パッケージマネージャーコンソール**に貼り付けるコマンドが表示されます。 クリップボードにテキストをコピーするための便利なボタンもあります。
   >
   > ![パッケージマネージャーコンソールコマンドを示す NuGet.org ページ](media/nuget-package-manager-command.png)

   Analyzer アセンブリがインストールされ、[**参照**] [アナライザー] の下の**ソリューションエクスプローラー**に表示され > **Analyzers**ます。

::: moniker-end

### <a name="custom-installation"></a>カスタム インストール

カスタムインストールの場合、たとえば、別のバージョンのパッケージを指定するには、プロジェクトの [コード分析のプロパティ] ページで省略記号 (...) ボタンを選択します。 このボタンをクリックすると、NuGet パッケージマネージャーが検索文字列として "FxCopAnalyzers" と共に開きます。

![Visual Studio の [プロパティ] ページからカスタム FxCop アナライザーパッケージをインストールする](media/install-fxcop-properties-page-ellipsis.png)

> [!TIP]
> 使用している Visual Studio のバージョンに基づいて、インストールする [アナライザーパッケージのバージョン](#fxcopanalyzers-package-versions) を決定します。 パッケージ [マネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)からパッケージをインストールすることもできます。

### <a name="fxcopanalyzers-package-versions"></a>FxCopAnalyzers パッケージのバージョン

次のガイドラインを使用して、使用している Visual Studio のバージョンに合わせてインストールする FxCop アナライザーパッケージのバージョンを決定します。

| Visual Studio のバージョン | FxCop アナライザーパッケージのバージョン |
| - | - |
| Visual Studio 2019 (すべてのバージョン) | [latest](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) |
| Visual Studio 2017 バージョン 15.9 | [2.9.10](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.9.10) |
| Visual Studio 2017 バージョン15.5 から15.8 | [2.6.4](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.4) |
| Visual Studio 2017 バージョン15.3 から15.4 | [2.3.0-beta1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.3.0-beta1) |
| Visual Studio 2017 バージョン15.0 から15.2 | [2.0.0-beta2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.0.0-beta2) |
| Visual Studio 2015 update 2 および3 | [1.2.0-beta2](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.2.0-beta2) |
| Visual Studio 2015 更新プログラム 1 | [1.1.0](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.1.0) |
| Visual Studio 2015 RTW | [1.0.1](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/1.0.1) |

## <a name="vsix"></a>VSIX

::: moniker range="vs-2017"

Visual Studio 2017 バージョン15.5 以降では、マネージプロジェクトのすべての FxCop アナライザーを含む [Microsoft Code Analysis 2017](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017) 拡張機能をインストールできます。

1. Visual Studio で、[ **ツール**] [ > **拡張機能と更新プログラム**] を選択します。

   **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > または、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2017)から拡張機能を直接ダウンロードします。

2. 左側のウィンドウで [ **オンライン** ] を展開し、[ **Visual Studio Marketplace**] を選択します。

3. 検索ボックスに「code analysis」と入力し、 **Microsoft Code analysis 2017** 拡張機能を探します。

   ![Microsoft Code Analysis 2017 拡張機能](media/extensions-and-updates-code-analysis.png)

::: moniker-end

::: moniker range=">=vs-2019"

[Microsoft Code Analysis 2019](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)拡張機能には、マネージプロジェクトのすべての FxCop アナライザーが含まれています。 この拡張機能をインストールするには:

1. Visual Studio で、[ **拡張**機能] [ > **拡張機能の管理**] を選択します。

   [ **拡張機能の管理** ] ダイアログボックスが表示されます。

   > [!NOTE]
   > または、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.MicrosoftCodeAnalysis2019)から拡張機能を直接ダウンロードします。

2. 左側のウィンドウで [ **オンライン** ] を展開し、[ **Visual Studio Marketplace**] を選択します。

3. 検索ボックスに「code analysis」と入力し、 **Microsoft Code analysis 2019** 拡張機能を探します。

   ![Microsoft Code Analysis 2019 拡張機能](media/manage-extensions-code-analysis.png)

::: moniker-end

4. **[ダウンロード]** を選択します。

   拡張機能がダウンロードされます。

5. [ **OK** ] を選択してダイアログボックスを閉じ、Visual Studio のすべてのインスタンスを閉じて、 **VSIX インストーラー**を起動します。

   [ **VSIX インストーラー** ] ダイアログボックスが表示されます。

   ::: moniker range="vs-2017"

   ![Microsoft コード分析用の VSIX インストーラー](media/vsix-installer-code-analysis.png)

   ::: moniker-end

6. [ **変更** ] を選択してインストールを開始します。

   1 ~ 2 分後にインストールが完了します。

7. [ **閉じる**] を選択し、もう一度 Visual Studio を開きます。

::: moniker range="vs-2017"

拡張機能がインストールされているかどうかを確認する場合は、[**ツール**] [  >  **拡張機能と更新プログラム**] を選択します。 [ **拡張機能と更新プログラム** ] ダイアログボックスで、左側の [ **インストール済み** ] カテゴリを選択し、名前を指定して拡張機能を検索します。

::: moniker-end

::: moniker range=">=vs-2019"

拡張機能がインストールされているかどうかを確認する場合は、[**拡張**機能] [  >  **拡張機能の管理**] を選択します。 [ **拡張機能の管理** ] ダイアログボックスで、左側の [ **インストール済み** ] カテゴリを選択し、名前を指定して拡張機能を検索します。

::: moniker-end

## <a name="see-also"></a>関連項目

- [Visual Studio のコードアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)
- [レガシ分析からコードアナライザーへの移行](../code-quality/migrate-from-legacy-analysis-to-fxcop-analyzers.md)
