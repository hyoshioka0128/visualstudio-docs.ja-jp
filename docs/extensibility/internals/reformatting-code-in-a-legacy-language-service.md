---
title: レガシ言語サービスでコードを再フォーマットする |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- reformatting code, supporting in language services [managed package framework]
- language services [managed package framework], reformatting code
ms.assetid: 08bb3375-8fef-4f4e-9efa-0d7333bab0eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd3e83c7299298b16a6fb3178b189479a80e1728
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705908"
---
# <a name="reformatting-code-in-a-legacy-language-service"></a>従来の言語サービスの再フォーマット コード

ソース[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コードでは、インデントと空白の使用を正規化することで再フォーマットできます。 これには、各行の先頭にスペースやタブを挿入または削除する、行間に新しい行を追加する、スペースをタブまたはタブにスペースで置き換えることなどが含まれます。

> [!NOTE]
> 改行文字の挿入または削除は、ブレークポイントやブックマークなどのマーカーに影響を与えますが、スペースやタブを追加または削除してもマーカーには影響しません。

ユーザーは、[**編集**] メニューの [**詳細設定**] メニューから **[選択範囲の書式設定**] または [**文書の書式設定**] を選択して、再フォーマット操作を開始できます。 再フォーマット操作は、コード スニペットまたは特定の文字が挿入されたときにトリガーすることもできます。 たとえば、C# で右中かっこを入力すると、対応する左中かっこと右中かっこの間のすべてが自動的に適切なレベルにインデントされます。

**[選択範囲の書式設定]** または [**ドキュメントの書式設定**] コマンド<xref:Microsoft.VisualStudio.Package.ViewFilter>を言語サービス<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>に送信すると<xref:Microsoft.VisualStudio.Package.Source>[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、クラスはクラス内のメソッドを呼び出します。 書式設定をサポートするには、メソッドを<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>オーバーライドし、独自の書式コードを指定する必要があります。

## <a name="enabling-support-for-reformatting"></a>再フォーマットのサポートの有効化

書式設定をサポートするには、VSPackage `EnableFormatSelection` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>を登録するときに`true`のパラメーターを に設定する必要があります。 これにより、プロパティ<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableFormatSelection%2A>が`true`に設定されます。 この<xref:Microsoft.VisualStudio.Package.ViewFilter.CanReformat%2A>メソッドは、このプロパティの値を返します。 true を返す場合<xref:Microsoft.VisualStudio.Package.ViewFilter>、クラスは<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>.

## <a name="implementing-reformatting"></a>再フォーマットの実装

再フォーマットを実装するには、<xref:Microsoft.VisualStudio.Package.Source>クラスからクラスを派生させ、メソッドをオーバーライド<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>する必要があります。 オブジェクト<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>はフォーマットする範囲を記述し、オブジェクト<xref:Microsoft.VisualStudio.Package.EditArray>はスパンで行われた編集を保持します。 このスパンはドキュメント全体にできます。 ただし、スパンに複数の変更が加えられる可能性があるため、すべての変更は 1 つのアクションで元に戻せる必要があります。 これを行うには、オブジェクト内のすべての変更を<xref:Microsoft.VisualStudio.Package.CompoundAction>ラップします (このトピックの「複合アクション クラスの使用」を参照してください)。

### <a name="example"></a>例

次の例では、コンマの後にタブが続くか行の末尾に入っていない限り、選択範囲内の各コンマの後にスペースが 1 つあるかどうかを確認します。 行の最後のコンマの後の末尾のスペースは削除されます。 このメソッドがメソッドからどのように呼び出されるのかについては、このトピックの「CompoundAction クラス<xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>の使用」を参照してください。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        private void DoFormatting(EditArray mgr, TextSpan span)
        {
            // Make sure there is one space after every comma unless followed
            // by a tab or comma is at end of line.
            IVsTextLines pBuffer = GetTextLines();
            if (pBuffer != null)
            {
                int    startIndex = span.iStartIndex;
                int    endIndex   = 0;
                string line       = "";
                // Loop over all lines in span
                for (int i = span.iStartLine; i <= span.iEndLine; i++)
                {
                    if (i < span.iEndLine)
                    {
                        pBuffer.GetLengthOfLine(i, out endIndex);
                    }
                    else
                    {
                        endIndex = span.iEndIndex;
                    }
                    pBuffer.GetLineText(i, startIndex, i, endIndex, out line);

                    if (line.Length > 0)
                    {
                        int index = 0;
                        // Loop over all commas in line
                        while ((index = line.IndexOf(',', index)) != -1)
                        {
                            int spaceIndex = index + 1;
                            // Determine how many spaces after comma
                            while (spaceIndex < line.Length && line[spaceIndex] == ' ')
                            {
                                ++spaceIndex;
                            }

                            int      spaceCount      = spaceIndex - (index + 1);
                            string   replacementText = " ";
                            bool     fDoEdit         = true;
                            TextSpan editTextSpan    = new TextSpan();

                            editTextSpan.iStartLine  = i;
                            editTextSpan.iEndLine    = i;
                            editTextSpan.iStartIndex = index + 1;

                            if (spaceIndex == line.Length)
                            {
                                if (spaceCount > 0)
                                {
                                    // Delete spaces after a comma at end of line
                                    editTextSpan.iEndIndex = spaceIndex;
                                    replacementText = "";
                                }
                                else
                                {
                                    // Otherwise, do not add spaces if comma is
                                    // at end of line.
                                    fDoEdit = false;
                                }
                            }
                            else if (spaceCount == 0)
                            {
                                if (spaceIndex < line.Length && line[spaceIndex] == '\t')
                                {
                                    // Do not insert space if a tab follows
                                    // a comma.
                                    fDoEdit = false;
                                }
                                else
                                {
                                    // No space after comma so add a space.
                                    editTextSpan.iEndIndex = index + 1;
                                }
                            }
                            else if (spaceCount > 1)
                            {
                                // More than one space after comma, replace
                                // with a single space.
                                editTextSpan.iEndIndex = spaceIndex;
                            }
                            else
                            {
                                // Single space after a comma and not at end
                                // of the line, leave it alone.
                                fDoEdit = false;
                            }
                            if (fDoEdit)
                            {
                                // Add edit operation
                                mgr.Add(new EditSpan(editTextSpan, replacementText));
                            }
                            index = spaceIndex;
                        }
                    }
                    startIndex = 0; // All subsequent lines start at 0
                }
                // Apply all edits
                mgr.ApplyEdits();
            }
        }
    }
}
```

## <a name="using-the-compoundaction-class"></a>複合アクションクラスの使用

コードのセクションで行われるすべての再フォーマットは、1 回の操作で元に戻せる必要があります。 これは<xref:Microsoft.VisualStudio.Package.CompoundAction>クラスを使用して実行できます。 このクラスは、テキスト バッファーに対する一連の編集操作を 1 つの編集操作にラップします。

### <a name="example"></a>例

クラスの使用方法の例を次に示<xref:Microsoft.VisualStudio.Package.CompoundAction>します。 メソッドの例については、このトピックの「書式設定のサポートの実装」の例を`DoFormatting`参照してください。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override void ReformatSpan(EditArray mgr, TextSpan span)
        {
            string description = "Reformat code";
            CompoundAction ca = new CompoundAction(this, description);
            using (ca)
            {
                ca.FlushEditActions();      // Flush any pending edits
                DoFormatting(mgr, span);    // Format the span
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目

- [従来の言語サービスの特徴](legacy-language-service-features1.md)
