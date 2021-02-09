---
title: テキストテンプレートからテキストテンプレートを生成する
description: エスケープシーケンスを使用して別のテキストテンプレートからテキストテンプレートを生成する方法について説明します。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, generating templates from templates
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: e3debeeafa55e483e9625c67534694debff6acfa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922792"
---
# <a name="how-to-generate-templates-from-templates-by-using-escape-sequences"></a>方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成する
生成されたテキストの出力として別のテキストテンプレートを作成するテキストテンプレートを作成できます。 そのためには、エスケープシーケンスを使用してテキストテンプレートタグを記述する必要があります。 エスケープシーケンスを使用しない場合、生成されたテキストテンプレートには定義済みの意味があります。 テキストテンプレートでのエスケープシーケンスの使用の詳細については、「 [テキストテンプレートでのエスケープシーケンスの使用](../modeling/using-escape-sequences-in-text-templates.md)」を参照してください。

### <a name="to-generate-a-text-template-from-within-a-text-template"></a>テキストテンプレート内からテキストテンプレートを生成するには

- 区切り記号 ( \\ ) をエスケープ文字として使用して、テキストテンプレート内でディレクティブ、ステートメント、式、およびクラス機能のために必要なマークアップタグを別のテキストテンプレートファイルに生成します。

    ```
    \<#@ directive \#>
    \<# statement \#>
    \<#= expression \#>
    \<#+ classfeature \#>
    ```

## <a name="example"></a>例
 次の例では、エスケープ文字を使用してテキストテンプレートからテキストテンプレートを生成します。 ディレクティブは、 `output` 変換先のファイルの種類をテキストテンプレートファイルの種類 (.tt) に設定します。

```csharp
\<#@ output extension=".tt" \#>
\<#@ assembly name="System.Xml.dll" \#>
\<#@ import namespace="System.Xml" \#>
\<#
XmlDocument xDoc = new XmlDocument();
//System.Diagnostics.Debugger.Break();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {\#>
           \<#= attr.Name \#>
       \<#}
     }
\#>
```

 生成されたテキスト出力はテキストテンプレートです。

```
<#@ output extension=".tt" #>
<#@ assembly name="System.Xml.dll" #>
<#@ import namespace="System.Xml" #>
<#
XmlDocument xDoc = new XmlDocument();
//System.Diagnostics.Debugger.Break();
    xDoc.Load(@"E:\CSharp\Overview.xml");
    XmlAttributeCollection attributes = xDoc.Attributes;
    if (attributes != null)
    {
       foreach (XmlAttribute attr in attributes)
       {#>
           <#= attr.Name #>
       <#}
     }
#>
```
