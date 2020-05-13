---
title: Web パフォーマンス テストのカスタム検証規則のコーディング
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- custom validation rules
- validation rules, creating
- web performance tests, creating custom validation rules
- rules, validation
- validation rules
ms.assetid: 989124bc-1a86-41f7-b37d-8f9e54dd4f0b
dev_langs:
- CSharp
- VB
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9780a4ee81a4d063b5cfb7f66b1a5ea023d8fa2f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75573405"
---
# <a name="code-a-custom-validation-rule-for-a-web-performance-test"></a>Web パフォーマンス テストのカスタム検証規則のコーディング

検証規則は独自に作成できます。 これを行うには、検証規則クラスから独自の規則クラスを派生します。 検証規則は、<xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule> 基底クラスから派生します。

> [!NOTE]
> また、カスタム抽出規則を作成することもできます。 詳細については、「[ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-custom-validation-rules"></a>カスタム検証規則を作成するには

1. Web パフォーマンス テストを含むテスト プロジェクトを開きます。

2. (省略可能) 検証規則を格納する個別のクラス ライブラリ プロジェクトを作成します。

    > [!IMPORTANT]
    > クラスは、テストが含まれる同じプロジェクトで作成できます。 ただし、規則を再利用する場合は、規則を格納する別のクラス ライブラリ プロジェクトを作成することをお勧めします。 個別のプロジェクトを作成するには、ここで省略可能として説明されている手順を実行する必要があります。

3. (省略可能) クラス ライブラリ プロジェクトに、Microsoft.VisualStudio.QualityTools.WebTestFramework.DLL への参照を追加します。

4. <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule> クラスから派生するクラスを作成します。 <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule.Validate*> メンバーと <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule.RuleName*> メンバーを実装します。

5. (省略可能) 新しいクラス ライブラリ プロジェクトをビルドします。

6. (省略可能) テスト プロジェクトで、カスタム検証規則を含むクラス ライブラリ プロジェクトへの参照を追加します。

7. テスト プロジェクトで、**Web パフォーマンス テスト エディター**を使用して Web パフォーマンス テストを開きます。

8. カスタム検証規則を Web パフォーマンス テスト要求に追加するには、要求を右クリックし、 **[検証規則の追加]** をクリックします。

     **[検証規則の追加]** ダイアログ ボックスが表示されます。 定義済みの検証規則と共に、カスタム検証規則が **[規則の選択]** ボックスに表示されます。 カスタム検証規則を選択し、 **[OK]** を選択します。

9. Web パフォーマンス テストを実行します。

## <a name="example"></a>例

次のコードは、カスタム検証規則の実装を示しています。 この検証規則は、定義済みの [必要なタグ] 検証規則の動作を模しています。 この例を、独自のカスタム検証規則のひな形として使用してください。

> [!WARNING]
> カスタム検証用のコード内のパブリック プロパティは、null 値にすることはできません。

```csharp
using System;
using System.Diagnostics;
using System.Globalization;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace SampleWebTestRules
{
    //-------------------------------------------------------------------------
    // This class creates a custom validation rule named "Custom Validate Tag"
    // The custom validation rule is used to check that an HTML tag with a
    // particular name is found one or more times in the HTML response.
    // The user of the rule can specify the HTML tag to look for, and the
    // number of times that it must appear in the response.
    //-------------------------------------------------------------------------
    public class CustomValidateTag : ValidationRule
    {
        /// Specify a name for use in the user interface.
        /// The user sees this name in the Add Validation dialog box.
        //---------------------------------------------------------------------
        public override string RuleName
        {
            get { return "Custom Validate Tag"; }
        }

        /// Specify a description for use in the user interface.
        /// The user sees this description in the Add Validation dialog box.
        //---------------------------------------------------------------------
        public override string RuleDescription
        {
            get { return "Validates that the specified tag exists on the page."; }
        }

        // The name of the required tag
        private string RequiredTagNameValue;
        public string RequiredTagName
        {
            get { return RequiredTagNameValue; }
            set { RequiredTagNameValue = value; }
        }

        // The minimum number of times the tag must appear in the response
        private int MinOccurrencesValue;
        public int MinOccurrences
        {
            get { return MinOccurrencesValue; }
            set { MinOccurrencesValue = value; }
        }

        // Validate is called with the test case Context and the request context.
        // These allow the rule to examine both the request and the response.
        //---------------------------------------------------------------------
        public override void Validate(object sender, ValidationEventArgs e)
        {
            bool validated = false;
            int numTagsFound = 0;

            foreach (HtmlTag tag in e.Response.HtmlDocument.GetFilteredHtmlTags(RequiredTagName))
            {
                Debug.Assert(string.Equals(tag.Name, RequiredTagName, StringComparison.InvariantCultureIgnoreCase));

                if (++numTagsFound >= MinOccurrences)
                {
                    validated = true;
                    break;
                }
            }

            e.IsValid = validated;

            // If the validation fails, set the error text that the user sees
            if (!validated)
            {
                if (numTagsFound > 0)
                {
                    e.Message = String.Format("Only found {0} occurrences of the tag", numTagsFound);
                }
                else
                {
                    e.Message = String.Format("Did not find any occurrences of tag '{0}'", RequiredTagName);
                }
            }
        }
    }
}
```

```vb
Imports System
Imports System.Diagnostics
Imports System.Globalization
Imports Microsoft.VisualStudio.TestTools.WebTesting

Namespace SampleWebTestRules

    '-------------------------------------------------------------------------
    ' This class creates a custom validation rule named "Custom Validate Tag"
    ' The custom validation rule is used to check that an HTML tag with a
    ' particular name is found one or more times in the HTML response.
    ' The user of the rule can specify the HTML tag to look for, and the
    ' number of times that it must appear in the response.
    '-------------------------------------------------------------------------
    Public Class CustomValidateTag
        Inherits Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule

        ' Specify a name for use in the user interface.
        ' The user sees this name in the Add Validation dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleName() As String
            Get
                Return "Custom Validate Tag"
            End Get
        End Property

        ' Specify a description for use in the user interface.
        ' The user sees this description in the Add Validation dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleDescription() As String
            Get
                Return "Validates that the specified tag exists on the page."
            End Get
        End Property

        ' The name of the required tag
        Private RequiredTagNameValue As String
        Public Property RequiredTagName() As String
            Get
                Return RequiredTagNameValue
            End Get
            Set(ByVal value As String)
                RequiredTagNameValue = value
            End Set
        End Property

        ' The minimum number of times the tag must appear in the response
        Private MinOccurrencesValue As Integer
        Public Property MinOccurrences() As Integer
            Get
                Return MinOccurrencesValue
            End Get
            Set(ByVal value As Integer)
                MinOccurrencesValue = value
            End Set
        End Property

        ' Validate is called with the test case Context and the request context.
        ' These allow the rule to examine both the request and the response.
        '---------------------------------------------------------------------
        Public Overrides Sub Validate(ByVal sender As Object, ByVal e As ValidationEventArgs)

            Dim validated As Boolean = False
            Dim numTagsFound As Integer = 0

            For Each tag As HtmlTag In e.Response.HtmlDocument.GetFilteredHtmlTags(RequiredTagName)

                Debug.Assert(String.Equals(tag.Name, RequiredTagName, StringComparison.InvariantCultureIgnoreCase))

                numTagsFound += 1
                If numTagsFound >= MinOccurrences Then

                    validated = True
                    Exit For
                End If
            Next

            e.IsValid = validated

            ' If the validation fails, set the error text that the user sees
            If Not (validated) Then
                If numTagsFound > 0 Then
                    e.Message = String.Format("Only found {0} occurrences of the tag", numTagsFound)
                Else
                    e.Message = String.Format("Did not find any occurrences of tag '{0}'", RequiredTagName)
                End If
            End If
        End Sub
    End Class
End Namespace
```

## <a name="see-also"></a>参照

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidateFormField>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleRequestTime>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleRequiredAttributeValue>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleRequiredTag>
- [Web パフォーマンス テストのカスタム抽出規則のコーディング](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)
