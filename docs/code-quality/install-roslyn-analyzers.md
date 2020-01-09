---
title: Roslyn アナライザーのインストール
ms.date: 08/03/2018
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 9a833cb46811bd97467fdb048272c9feb2bb7873
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587382"
---
# <a name="install-net-compiler-platform-code-analyzers"></a>.NET Compiler Platform コードアナライザーをインストールする

Visual Studio には、.NET Compiler Platform (*Roslyn*) アナライザーのコアセットが含まれています。 これらのアナライザーは常にオンになっています。 追加のアナライザーは、NuGet パッケージとして、または*VSIX*ファイルの Visual Studio 拡張機能としてインストールできます。

## <a name="to-install-nuget-analyzer-packages"></a>NuGet analyzer パッケージをインストールするには

1. www.nuget.org をインストールするアナライザー パッケージを検索します。

   たとえば、コードにセキュリティやパフォーマンスの問題がないかどうかを確認するために、 [Microsoft FxCop アナライザーをインストール](install-fxcop-analyzers.md#nuget-package)することができます。 または、 [StyleCop](https://www.nuget.org/packages/stylecop.analyzers/)をインストールして、コードベースでスタイルの問題を探します。

2. パッケージ[マネージャーコンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)または[パッケージマネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)を使用して、Visual Studio にパッケージをインストールします。

   > [!NOTE]
   > 各アナライザーパッケージの www.nuget.org ページには、**パッケージマネージャーコンソール**に貼り付けるコマンドが表示されます。 クリップボードにテキストをコピーするための便利なボタンもあります。

   Analyzer アセンブリがインストールされ、[**参照** > **アナライザー**] の下の**ソリューションエクスプローラー**に表示されます。

## <a name="to-install-vsix-analyzers"></a>VSIX アナライザーをインストールするには

::: moniker range="vs-2017"

1. Visual Studio で、 **[ツール]** [> の**拡張機能と更新プログラム**] を選択します。

   **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > または、 [Visual Studio Marketplace](https://marketplace.visualstudio.com)から直接、analyzer 拡張機能を見つけてダウンロードすることもできます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio で、**拡張**機能 を選択して **拡張機能 > 管理**します。

   **[拡張機能の管理]** ダイアログボックスが表示されます。

   > [!NOTE]
   > または、 [Visual Studio Marketplace](https://marketplace.visualstudio.com)から直接、analyzer 拡張機能を見つけてダウンロードすることもできます。

::: moniker-end

2. 左側のウィンドウで **[オンライン]** を展開し、 **[Visual Studio Marketplace]** を選択します。

3. 検索ボックスに、インストールするアナライザー拡張機能の名前を入力します。 たとえば、コードにセキュリティやパフォーマンスの問題がないかどうかを確認するために、 [Microsoft FxCop アナライザーをインストール](install-fxcop-analyzers.md#vsix)することができます。

4. **[Download]** を選択します。

   拡張機能がダウンロードされます。

5. **[OK]** を選択してダイアログボックスを閉じ、Visual Studio のすべてのインスタンスを閉じて、 **VSIX インストーラー**を起動します。

   **[VSIX インストーラー]** ダイアログボックスが表示されます。

   ![Microsoft コード分析用の VSIX インストーラー](media/vsix-installer-code-analysis.png)

6. **[変更]** を選択してインストールを開始します。

7. 1 ~ 2 分後にインストールが完了します。 **[閉じる]** を選択します。

8. Visual Studio を再度開きます。

::: moniker range="vs-2017"

拡張機能がインストールされているかどうかを確認する場合は、 **[ツール]** [ > の**拡張機能と更新プログラム**] を選択します。 **[拡張機能と更新プログラム]** ダイアログボックスで、左側の **[インストール済み]** カテゴリを選択し、名前を指定して拡張機能を検索します。

::: moniker-end

::: moniker range=">=vs-2019"

拡張機能がインストールされているかどうかを確認する場合は、[拡張機能] > [拡張**機能の管理**] を**選択します**。 **[拡張機能の管理]** ダイアログボックスで、左側の **[インストール済み]** カテゴリを選択し、名前を指定して拡張機能を検索します。

::: moniker-end

## <a name="next-steps"></a>次のステップ:

> [!div class="nextstepaction"]
> [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>関連項目

- [Visual Studio のコードアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [FxCop アナライザーのインストール](../code-quality/install-fxcop-analyzers.md)
