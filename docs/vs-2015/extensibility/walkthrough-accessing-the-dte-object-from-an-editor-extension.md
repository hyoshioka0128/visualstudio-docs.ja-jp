---
title: 'チュートリアル: エディター拡張機能から DTE オブジェクトにアクセスする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - getting the DTE object
ms.assetid: c1f40bab-c6ec-45b0-8333-ea5ceb02a39d
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b14b59465b94ddd0a09748f0e309166bf3d4114
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148878"
---
# <a name="walkthrough-accessing-the-dte-object-from-an-editor-extension"></a>チュートリアル: エディターの拡張機能から DTE オブジェクトにアクセスする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Vspackage では、dte <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトの型を使用してメソッドを呼び出すことにより、dte オブジェクトを取得できます。 Managed Extensibility Framework (MEF) 拡張機能では、型のを使用してメソッドをインポートし、呼び出すことができ <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> <xref:EnvDTE.DTE> ます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="getting-the-dte-object"></a>DTE オブジェクトの取得  
  
#### <a name="to-get-the-dte-object-from-the-serviceprovider"></a>ServiceProvider から DTE オブジェクトを取得するには  
  
1. という名前の C# VSIX プロジェクトを作成 `DTETest` します。 エディター分類子項目テンプレートを追加し、という名前を指定 `DTETest` します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
2. 次のアセンブリ参照をプロジェクトに追加します。  
  
    - EnvDTE  
  
    - EnvDTE80  
  
    - VisualStudio (変更不可)  
  
3. DTETest.cs ファイルにアクセスし、次のディレクティブを追加し `using` ます。  
  
    ```csharp  
    using EnvDTE;  
    using EnvDTE80;  
    using Microsoft.VisualStudio.Shell;  
  
    ```  
  
4. クラスで、 `GetDTEProvider` をインポート <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> します。  
  
    ```csharp  
    [Import]  
    internal SVsServiceProvider ServiceProvider = null;  
  
    ```  
  
5. `GetClassifier()` メソッドに次のコードを追加します。  
  
    ```csharp  
    DTE dte = (DTE)ServiceProvider.GetService(typeof(DTE));  
  
    ```  
  
6. インターフェイスを使用する必要がある場合は、 <xref:EnvDTE80.DTE2> DTE オブジェクトをキャストすることができます。  
  
## <a name="see-also"></a>参照  
 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
