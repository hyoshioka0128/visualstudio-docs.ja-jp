---
title: テキストテンプレートから Visual Studio 2015 またはその他のホストにアクセスする |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: a68886da-7416-4785-8145-3796bb382cba
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0e8cedc66d6b52f80239364a3e51b73e93a69aa4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655332"
---
# <a name="accessing-visual-studio-or-other-hosts-from-a-text-template"></a>テキスト テンプレートから Visual Studio またはその他のホストへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストテンプレートでは、など、テンプレートを実行するホストによって公開されているメソッドとプロパティを使用でき [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

 これは、プリプロセスされたテキストテンプレートではなく、通常のテキストテンプレートに適用されます。

## <a name="obtaining-access-to-the-host"></a>ホストへのアクセスを取得しています

`hostspecific="true"`ディレクティブでを設定 `template` します。 これにより  `this.Host` 、 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))型のを使用できます。 この型には、ファイル名を解決したりエラーをログに記録したりするために使用できるメンバーが含まれています。

### <a name="resolving-file-names"></a>ファイル名の解決
 テキストテンプレートを基準としたファイルの完全なパスを検索するには、これを使用します。ホストの ResolvePath ()。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>

```

### <a name="displaying-error-messages"></a>エラーメッセージの表示
 この例では、テンプレートを変換するときにメッセージをログに記録します。 ホストがの場合は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、エラーウィンドウに追加されます。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.CodeDom.Compiler" #>
<#
  string message = "test message";
  this.Host.LogErrors(new CompilerErrorCollection()
    { new CompilerError(
       this.Host.TemplateFile, // Identify the source of the error.
       0, 0, "0",   // Line, column, error ID.
       message) }); // Message displayed in error window.
#>

```

## <a name="using-the-visual-studio-api"></a>Visual Studio API の使用
 でテキストテンプレートを実行している場合は、を使用して、に [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] `this.Host` よって提供さ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] れるサービスと読み込まれたパッケージまたは拡張機能にアクセスできます。

 Hostspecific = "true" に設定し、にキャストし `this.Host` <xref:System.IServiceProvider> ます。

 この例では、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] API を <xref:EnvDTE.DTE> サービスとして取得します。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#
 IServiceProvider serviceProvider = (IServiceProvider)this.Host;
 DTE dte = serviceProvider.GetService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>

```

## <a name="using-hostspecific-with-template-inheritance"></a>テンプレート継承での hostSpecific の使用
 `hostspecific="trueFromBase"`属性も使用するかどうか、 `inherits` およびを指定するテンプレートから継承する場合はを指定し `hostspecific="true"` ます。 これにより、プロパティが2回宣言されているという結果に対するコンパイラ警告が回避 `Host` されます。
