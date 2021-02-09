---
title: テキスト テンプレートから Visual Studio またはその他のホストへのアクセス
description: テンプレートを実行するホストによって公開されているテキストテンプレートで、メソッドとプロパティを使用する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ce008d0a14cbd75cf8a46599ff67bd9e799ee8ce
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908875"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>テキストテンプレートから Visual Studio またはその他のホストにアクセスする

テキストテンプレートでは、テンプレートを実行するホストによって公開されているメソッドとプロパティを使用できます。 ホストの例として、Visual Studio があります。

> [!NOTE]
> ホストメソッドとプロパティは、通常のテキストテンプレートでは使用できますが、 *前処理* されたテキストテンプレートでは使用できません。

## <a name="obtain-access-to-the-host"></a>ホストへのアクセスを取得する

ホストにアクセスするには、 `hostspecific="true"` ディレクティブでを設定 `template` します。 これで `this.Host` 、型 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))を持つを使用できるようになりました。 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))型には、ファイル名を解決し、エラーをログに記録するために使用できるメンバーがあります。たとえば、のようになります。

### <a name="resolve-file-names"></a>ファイル名の解決

テキストテンプレートを基準としたファイルの完全なパスを検索するには、を使用 `this.Host.ResolvePath()` します。

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

### <a name="display-error-messages"></a>エラーメッセージを表示する

この例では、テンプレートを変換するときにメッセージをログに記録します。 ホストが Visual Studio の場合は、エラーが **エラー一覧** に追加されます。

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

## <a name="use-the-visual-studio-api"></a>Visual Studio API を使用する

Visual Studio でテキストテンプレートを実行している場合は、を使用し `this.Host` て、Visual studio によって提供されるサービスと読み込まれたパッケージまたは拡張機能にアクセスできます。

Hostspecific = "true" に設定し、にキャストし `this.Host` <xref:System.IServiceProvider> ます。

この例では、Visual Studio API を <xref:EnvDTE.DTE> サービスとして取得します。

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

## <a name="use-hostspecific-with-template-inheritance"></a>テンプレートの継承で hostSpecific を使用する

`hostspecific="trueFromBase"`属性も使用するかどうか、 `inherits` およびを指定するテンプレートから継承する場合はを指定し `hostspecific="true"` ます。 そうしないと、プロパティ `Host` が2回宣言されていることを示すコンパイラの警告が表示されることがあります。
