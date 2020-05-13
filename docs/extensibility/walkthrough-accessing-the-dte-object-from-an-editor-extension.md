---
title: エディター拡張機能から DTE オブジェクトにアクセスする
ms.date: 04/24/2019
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e37bdb21b7c8132f0dfb166d19e03d36e838245d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697656"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>チュートリアル: エディター拡張機能から DTE オブジェクトにアクセスする

VSPackages では、DTE オブジェクトの型を使用して<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>メソッドを呼び出すことによって、DTE オブジェクトを取得できます。 マネージ機能拡張フレームワーク (MEF) 拡張機能では、インポート<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>し、型を<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A>使用してメソッドを呼び出<xref:EnvDTE.DTE>すことができます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="get-the-dte-object"></a>DTE オブジェクトを取得する

1. C# VSIX プロジェクトを作成し **、DTETest**という名前を付けます。 **エディター分類子**項目テンプレートを追加し、名前**DTETest**.

   詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

::: moniker range=">=vs-2019"

2. プロジェクトに次のアセンブリ参照を追加します。

    - フレームワーク
    - をクリックします。

3. *DTETestProvider.cs*ファイルに、次`using`のディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. クラスで`DTETestProvider`、 をインポート<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>します。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. メソッドで`GetClassifier()`、ステートメントの前に次のコード`return`を追加します。

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. プロジェクトに次のアセンブリ参照を追加します。

   - EnvDTE
   - フレームワーク

3. *DTETestProvider.cs*ファイルに、次`using`のディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. クラスで`DTETestProvider`、 をインポート<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>します。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. メソッドで`GetClassifier()`、ステートメントの前に次のコード`return`を追加します。

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>関連項目

- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
- [DTE を使って Visual Studio を起動する](launch-visual-studio-dte.md)
