---
title: テンプレートからテンプレートを生成するためにエスケープシーケンスを使用する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, generating templates from templates
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1460b03a027a2b33844edc7d617f8b5f21208772
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594644"
---
# <a name="how-to-generate-templates-from-templates-by-using-escape-sequences"></a>方法: エスケープ シーケンスを使用してテンプレートからテンプレートを生成する
別のテキスト テンプレートを作成するテキスト出力として生成されたテキスト テンプレートを作成することができます。 これを行うには、テキスト テンプレートのタグを区切るためにエスケープ シーケンスを使用する必要があります。 エスケープシーケンスを使用しない場合、生成されたテキストテンプレートには定義済みの意味があります。 テキスト テンプレートでのエスケープ シーケンスの使用の詳細については、次を参照してください。[テキスト テンプレートでのエスケープ シーケンスの使用](../modeling/using-escape-sequences-in-text-templates.md)

### <a name="to-generate-a-text-template-from-within-a-text-template"></a>テキスト テンプレート内でテキスト テンプレートを生成するには

- 別のテキスト テンプレート ファイル内で、ディレクティブ、ステートメント、式、クラス機能といった必要なマークアップ タグをテキスト テンプレート内で作成するためにエスケープ文字として、バックスラッシュ (\\) を使用します。

    ```
    \<#@ directive \#>
    \<# statement \#>
    \<#= expression \#>
    \<#+ classfeature \#>
    ```

## <a name="example"></a>使用例
 次の例では、エスケープ文字を使用して、テキスト テンプレートからテキスト テンプレートを生成します。 `output` ディレクティブは、変換先ファイルのテキスト テンプレート ファイルの種類 (.tt) を設定します。

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
