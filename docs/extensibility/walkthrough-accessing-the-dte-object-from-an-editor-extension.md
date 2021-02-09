---
title: エディター拡張機能から DTE オブジェクトにアクセスする
description: このチュートリアルのコード例を使用して、エディター拡張機能から DTE オブジェクトにアクセスする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/24/2019
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7228165d49c7f11c15d12086933c473699ef6bc8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99905586"
---
# <a name="walkthrough-access-the-dte-object-from-an-editor-extension"></a>チュートリアル: エディター拡張機能から DTE オブジェクトにアクセスする

Vspackage では、dte <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトの型を使用してメソッドを呼び出すことにより、dte オブジェクトを取得できます。 Managed Extensibility Framework (MEF) 拡張機能では、型のを使用してメソッドをインポートし、呼び出すことができ <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> <xref:EnvDTE.DTE> ます。

## <a name="prerequisites"></a>前提条件

このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="get-the-dte-object"></a>DTE オブジェクトを取得する

1. C# VSIX プロジェクトを作成し、 **Dtetest** という名前を指定します。 **エディター分類子** 項目テンプレートを追加し、 **dtetest** という名前を指定します。

   詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

::: moniker range=">=vs-2019"

2. 次のアセンブリ参照をプロジェクトに追加します。

    - Microsoft. VisualStudio
    - VisualStudio (変更不可)

3. *DTETestProvider.cs* ファイルで、次のディレクティブを追加し `using` ます。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. クラスで、を `DTETestProvider` インポート <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> します。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. メソッドで `GetClassifier()` 、ステートメントの前に次のコードを追加し `return` ます。

    ```csharp
   ThreadHelper.ThrowIfNotOnUIThread();
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

::: moniker range="vs-2017"

2. 次のアセンブリ参照をプロジェクトに追加します。

   - EnvDTE
   - Microsoft. VisualStudio

3. *DTETestProvider.cs* ファイルで、次のディレクティブを追加し `using` ます。

    ```csharp
    using EnvDTE;
    using Microsoft.VisualStudio.Shell;
    ```

4. クラスで、を `DTETestProvider` インポート <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> します。

    ```csharp
    [Import]
    internal SVsServiceProvider ServiceProvider = null;
    ```

5. メソッドで `GetClassifier()` 、ステートメントの前に次のコードを追加し `return` ます。

    ```csharp
   DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));
   ```

::: moniker-end

## <a name="see-also"></a>関連項目

- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)
- [DTE を使って Visual Studio を起動する](launch-visual-studio-dte.md)
