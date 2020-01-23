---
title: エディター拡張機能から DTE オブジェクトにアクセスする
ms.date: 04/24/2019
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d023359412b423c9c12d7c7d8a37e79571cbc11a
ms.sourcegitcommit: e3c3d2b185b689c5e32ab4e595abc1ac60b6b9a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76269086"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>チュートリアル: エディター拡張機能から DTE オブジェクトにアクセスする

Vspackage では、dte オブジェクトの型を使用して <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> メソッドを呼び出すことにより、DTE オブジェクトを取得できます。 Managed Extensibility Framework (MEF) 拡張機能では、<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> をインポートし、<xref:EnvDTE.DTE>の種類を使用して <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> メソッドを呼び出すことができます。

## <a name="prerequisites"></a>Prerequisites

このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="get-the-dte-object"></a>DTE オブジェクトを取得する

1. C# VSIX プロジェクトを作成し、 **dtetest**という名前を指定します。 **エディター分類子**項目テンプレートを追加し、 **dtetest**という名前を指定します。

   詳細については、「[エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

::: moniker range=">=vs-2019"

2. 次のアセンブリ参照をプロジェクトに追加します。

    - Microsoft. VisualStudio
    - Microsoft.VisualStudio.Shell.Immutable.10.0

3. *DTETestProvider.cs*ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. `DTETestProvider` クラスで、<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>をインポートします。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. `GetClassifier()` メソッドで、`return` ステートメントの前に次のコードを追加します。

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 次のアセンブリ参照をプロジェクトに追加します。

   - EnvDTE
   - Microsoft. VisualStudio

3. *DTETestProvider.cs*ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. `DTETestProvider` クラスで、<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>をインポートします。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. `GetClassifier()` メソッドで、`return` ステートメントの前に次のコードを追加します。

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>関連項目

- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)
- [DTE を使用して Visual Studio を起動する](launch-visual-studio-dte.md)
