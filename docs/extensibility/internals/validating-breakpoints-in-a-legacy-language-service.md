---
title: 従来の言語サービスでのブレークポイントの検証 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af09e4f8f2156100bea9267c92ffebeb64ce1aa3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704091"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>従来の言語サービスでのブレークポイントの検証
ブレークポイントは、デバッガーで実行されている間、プログラムの実行を特定の時点で停止することを示します。 エディターはブレークポイントの有効な場所を構成する情報を知らないので、ユーザーはソース ファイル内の任意の行にブレークポイントを配置できます。 デバッガーが起動すると、マークされたすべてのブレークポイント (保留中のブレークポイントと呼ばれます) が、実行中のプログラム内の適切な場所にバインドされます。 同時に、ブレークポイントが有効なコードの場所をマークすることを確認するために検証されます。 たとえば、ソース コード内のその場所にコードがないため、コメントのブレークポイントは無効です。 デバッガーは無効なブレークポイントを無効にします。

 言語サービスは表示されるソース コードを認識しているため、デバッガーが起動する前にブレークポイントを検証できます。 ブレークポイントの<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>有効な位置を指定する範囲を返すメソッドをオーバーライドできます。 デバッガーが起動してもブレークポイントの場所は検証されますが、デバッガーの読み込みを待たずに無効なブレークポイントがユーザーに通知されます。

## <a name="implementing-support-for-validating-breakpoints"></a>ブレークポイントの検証のサポートの実装

- メソッド<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>には、ブレークポイントの位置が与えられます。 実装では、場所が有効かどうかを判断し、ブレークポイントの行位置に関連付けられたコードを識別するテキスト範囲を返すことによって、これを示す必要があります。

- 場所<xref:Microsoft.VisualStudio.VSConstants.S_OK>が有効な場合、または<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>無効な場合に返します。

- ブレークポイントが有効な場合、ブレークポイントと共にテキスト範囲が強調表示されます。

- ブレークポイントが無効な場合は、ステータス バーにエラー メッセージが表示されます。

### <a name="example"></a>例
 この例では、パーサーを<xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>呼び出して、指定した場所にあるコードの範囲を取得するメソッドの実装を示します。

 この例では、テキスト範囲を`GetCodeSpan`検証し、有効<xref:Microsoft.VisualStudio.Package.AuthoringSink>なブレークポイントの位置かどうかを返す`true`メソッドをクラスに追加したことを前提としています。

```csharp
using Microsoft VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        public override int ValidateBreakpointLocation(IVsTextBuffer buffer,
                                                       int line,
                                                       int col,
                                                       TextSpan[] pCodeSpan)
        {
            int retval = VSConstants.S_FALSE;
            if (pCodeSpan != null)
            {
                // Initialize span to current line by default.
                pCodeSpan[0].iStartLine = line;
                pCodeSpan[0].iStartIndex = col;
                pCodeSpan[0].iEndLine = line;
                pCodeSpan[0].iEndIndex = col;
            }

            if (buffer != null)
            {
                IVsTextLines textLines = buffer as IVsTextLines;
                if (textLines != null)
                {
                    Source src = this.GetSource(textLines);
                    if (src != null)
                    {
                        TokenInfo tokenInfo = new TokenInfo();
                        string text = src.GetText();
                        ParseRequest req = CreateParseRequest(src,
                                                              line,
                                                              col,
                                                              tokenInfo,
                                                              text,
                                                              src.GetFilePath(),
                                                              ParseReason.CodeSpan,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        TextSpan span = new TextSpan();
                        if (sink.GetCodeSpan(out span))
                        {
                            pCodeSpan[0] = span;
                            retval = VSConstants.S_OK;
                        }
                    }
                }
            }
            return retval;
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
