---
title: Web パフォーマンス テストのカスタム抽出規則のコーディング
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- extraction rules
- Web performance tests, creating custom extraction rules
- extraction rules, creating custom
ms.assetid: 6bcc5712-6cc6-4f59-8933-6e8078318c45
dev_langs:
- CSharp
- VB
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 92cce705135daa8bc54a7fab301cf5dcd8cf96d6
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75591178"
---
# <a name="code-a-custom-extraction-rule-for-a-web-performance-test"></a>Web パフォーマンス テストのカスタム抽出規則のコーディング

独自の抽出規則を作成できます。 これを行うには、抽出規則クラスから独自の規則を派生します。 抽出規則は、<xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> 基底クラスから派生します。

> [!NOTE]
> また、カスタム検証規則を作成することもできます。 詳細については、「[ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-a-custom-extraction-rule"></a>カスタム抽出規則を作成するには

1. Web パフォーマンス テストを含むテスト プロジェクトを開きます。

2. (省略可能) 抽出規則を格納する個別のクラス ライブラリ プロジェクトを作成します。

    > [!IMPORTANT]
    > クラスは、テストが含まれる同じプロジェクトで作成できます。 ただし、規則を再利用する場合は、規則を格納する別のクラス ライブラリ プロジェクトを作成することをお勧めします。 個別のプロジェクトを作成するには、ここで省略可能として説明されている手順を実行する必要があります。

3. (省略可能) クラス ライブラリ プロジェクトに、Microsoft.VisualStudio.QualityTools.WebTestFramework.dll への参照を追加します。

4. <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> クラスから派生するクラスを作成します。 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> メンバーと <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.RuleName*> メンバーを実装します。

5. (省略可能) 新しいクラス ライブラリ プロジェクトをビルドします。

6. (省略可能) テスト プロジェクトで、カスタム抽出規則を含むクラス ライブラリ プロジェクトへの参照を追加します。

7. テスト プロジェクトで、**Web パフォーマンス テスト エディター**を使用して Web パフォーマンス テストを開きます。

8. カスタム抽出規則を追加するには、Web パフォーマンス テスト要求を右クリックし、 **[抽出規則の追加]** をクリックします。

     **[抽出規則の追加]** ダイアログ ボックスが表示されます。 定義済みの検証規則と共に、カスタム検証規則が **[規則の選択]** ボックスに表示されます。 カスタム抽出規則を選択し、 **[OK]** をクリックします。

9. Web パフォーマンス テストを実行します。

## <a name="example"></a>例

次のコードは、カスタム抽出規則の実装を示しています。 この抽出規則では、指定された入力フィールドから値を抽出します。 この例を、独自のカスタム抽出規則のひな形として使用してください。

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.TestTools.WebTesting;
using System.Globalization;

namespace ClassLibrary2
{
    //-------------------------------------------------------------------------
    // This class creates a custom extraction rule named "Custom Extract Input"
    // The user of the rule specifies the name of an input field, and the
    // rule attempts to extract the value of that input field.
    //-------------------------------------------------------------------------
    public class CustomExtractInput : ExtractionRule
    {
        /// Specify a name for use in the user interface.
        /// The user sees this name in the Add Extraction dialog box.
        //---------------------------------------------------------------------
        public override string RuleName
        {
            get { return "Custom Extract Input"; }
        }

        /// Specify a description for use in the user interface.
        /// The user sees this description in the Add Extraction dialog box.
        //---------------------------------------------------------------------
        public override string RuleDescription
        {
            get { return "Extracts the value from a specified input field"; }
        }

        // The name of the desired input field
        private string NameValue;
        public string Name
        {
            get { return NameValue; }
            set { NameValue = value; }
        }

        // The Extract method.  The parameter e contains the web performance test context.
        //---------------------------------------------------------------------
        public override void Extract(object sender, ExtractionEventArgs e)
        {
            if (e.Response.HtmlDocument != null)
            {
                foreach (HtmlTag tag in e.Response.HtmlDocument.GetFilteredHtmlTags(new string[] { "input" }))
                {
                    if (String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase))
                    {
                        string formFieldValue = tag.GetAttributeValueAsString("value");
                        if (formFieldValue == null)
                        {
                            formFieldValue = String.Empty;
                        }

                        // add the extracted value to the web performance test context
                        e.WebTest.Context.Add(this.ContextParameterName, formFieldValue);
                        e.Success = true;
                        return;
                    }
                }
            }
            // If the extraction fails, set the error text that the user sees
            e.Success = false;
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name);
        }
    }
}
```

```vb
Imports System
Imports System.Collections.Generic
Imports Microsoft.VisualStudio.TestTools.WebTesting
Imports System.Globalization

Namespace ClassLibrary2

    '-------------------------------------------------------------------------
    ' This class creates a custom extraction rule named "Custom Extract Input"
    ' The user of the rule specifies the name of an input field, and the
    ' rule attempts to extract the value of that input field.
    '-------------------------------------------------------------------------
    Public Class CustomExtractInput
        Inherits ExtractionRule

        ' Specify a name for use in the user interface.
        ' The user sees this name in the Add Extraction dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleName() As String
            Get
                Return "Custom Extract Input"
            End Get
        End Property

        ' Specify a description for use in the user interface.
        ' The user sees this description in the Add Extraction dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleDescription() As String
            Get
                Return "Extracts the value from a specified input field"
            End Get
        End Property

        ' The name of the desired input field
        Private NameValue As String
        Public Property Name() As String
            Get
                Return NameValue
            End Get
            Set(ByVal value As String)
                NameValue = value
            End Set
        End Property

        ' The Extract method.  The parameter e contains the web performance test context.
        '---------------------------------------------------------------------
        Public Overrides Sub Extract(ByVal sender As Object, ByVal e As ExtractionEventArgs)

            If Not e.Response.HtmlDocument Is Nothing Then

                For Each tag As HtmlTag In e.Response.HtmlDocument.GetFilteredHtmlTags(New String() {"input"})

                    If String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase) Then

                        Dim formFieldValue As String = tag.GetAttributeValueAsString("value")
                        If formFieldValue Is Nothing Then

                            formFieldValue = String.Empty
                        End If

                        ' add the extracted value to the web performance test context
                        e.WebTest.Context.Add(Me.ContextParameterName, formFieldValue)
                        e.Success = True
                        Return
                    End If
                Next
            End If
            ' If the extraction fails, set the error text that the user sees
            e.Success = False
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name)
        End Sub
    End Class
End Namespace
```

<xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> メソッドに、抽出規則の中心的な機能が含まれています。 前の例の <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> メソッドは、この抽出規則の対象となる要求が生成する応答を示す <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionEventArgs> を受け取ります。 応答には、応答内のすべてのタグを含む <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument> が含まれています。 入力タグは、<xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument> からフィルターで除外されます。 各入力タグについて、`Name` プロパティに対してユーザーが指定した値を持つ `name` という属性があるかどうか、確認されます。 一致する属性を持つタグが見つかった場合、value 属性が存在すれば、その `value` 属性に含まれている値の抽出が試みられます。 存在する場合、タグの名前と値が抽出され、Web パフォーマンス テスト コンテキストに追加されます。 抽出規則が成功します。

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractAttributeValue>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractFormField>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHttpHeader>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractRegularExpression>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractText>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHiddenFields>
- [Web パフォーマンス テストのカスタム検証規則のコーディング](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
