---
title: サードパーティのアナライザーのインストール
ms.date: 08/27/2020
description: Visual Studio でサードパーティ製アナライザーをインストールする方法について説明します。 「.Vsix ファイルと NuGet アナライザーパッケージにアナライザーをインストールする方法」を参照してください。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3d4833ba922ddde1a1770cfd75cf446f210e2c79
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99859854"
---
# <a name="install-third-party-analyzers"></a>サードパーティ製アナライザーのインストール

Visual Studio には、.NET Compiler Platform (*Roslyn*) アナライザーのコアセットが含まれています。 これらのアナライザーは常にオンになっています。 追加のアナライザーは、NuGet パッケージとして、または *VSIX* ファイルの Visual Studio 拡張機能としてインストールできます。

## <a name="to-install-nuget-analyzer-packages"></a>NuGet analyzer パッケージをインストールするには

1. Www.nuget.org にインストールするアナライザーパッケージを見つけます。

   たとえば、 [StyleCop](https://www.nuget.org/packages/stylecop.analyzers/) をインストールして、コードベースでスタイルの問題を探すことができます。

2. パッケージ [マネージャーコンソール](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console) または [パッケージマネージャー UI](/nuget/quickstart/install-and-use-a-package-in-visual-studio#package-manager-console)を使用して、Visual Studio にパッケージをインストールします。

   > [!NOTE]
   > 各アナライザーパッケージの [www.nuget.org] ページには、 **パッケージマネージャーコンソール** に貼り付けるコマンドが表示されます。 クリップボードにテキストをコピーするための便利なボタンもあります。

   Analyzer アセンブリがインストールされ、[**参照**] [アナライザー] の下の **ソリューションエクスプローラー** に表示され  >  ます。

## <a name="to-install-vsix-analyzers"></a>VSIX アナライザーをインストールするには

::: moniker range="vs-2017"

1. Visual Studio で、[ **ツール**] [ > **拡張機能と更新プログラム**] を選択します。

   **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > または、 [Visual Studio Marketplace](https://marketplace.visualstudio.com)から直接、analyzer 拡張機能を見つけてダウンロードすることもできます。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio で、[ **拡張** 機能] [ > **拡張機能の管理**] を選択します。

   [ **拡張機能の管理** ] ダイアログボックスが表示されます。

   > [!NOTE]
   > または、 [Visual Studio Marketplace](https://marketplace.visualstudio.com)から直接、analyzer 拡張機能を見つけてダウンロードすることもできます。

::: moniker-end

2. 左側のウィンドウで [ **オンライン** ] を展開し、[ **Visual Studio Marketplace**] を選択します。

3. 検索ボックスに、インストールするアナライザー拡張機能の名前を入力します。

4. **[ダウンロード]** を選択します。

   拡張機能がダウンロードされます。

5. [ **OK** ] を選択してダイアログボックスを閉じ、Visual Studio のすべてのインスタンスを閉じて、 **VSIX インストーラー** を起動します。

   [ **VSIX インストーラー** ] ダイアログボックスが表示されます。

   ![Microsoft コード分析用の VSIX インストーラー](media/vsix-installer-code-analysis.png)

6. [ **変更** ] を選択してインストールを開始します。

7. 1 ~ 2 分後にインストールが完了します。 **[閉じる]** を選択します。

8. Visual Studio を再度開きます。

::: moniker range="vs-2017"

拡張機能がインストールされているかどうかを確認する場合は、[**ツール**] [  >  **拡張機能と更新プログラム**] を選択します。 [ **拡張機能と更新プログラム** ] ダイアログボックスで、左側の [ **インストール済み** ] カテゴリを選択し、名前を指定して拡張機能を検索します。

::: moniker-end

::: moniker range=">=vs-2019"

拡張機能がインストールされているかどうかを確認する場合は、[**拡張** 機能] [  >  **拡張機能の管理**] を選択します。 [ **拡張機能の管理** ] ダイアログボックスで、左側の [ **インストール済み** ] カテゴリを選択し、名前を指定して拡張機能を検索します。

::: moniker-end

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [Visual Studio でコード アナライザーを使用する](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>関連項目

- [Visual Studio のコードアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [.NET アナライザーのインストール](../code-quality/install-net-analyzers.md)
