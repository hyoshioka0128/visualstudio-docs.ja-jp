---
title: 従来の言語サービスでブレークポイントを検証する |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80704091"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>従来の言語サービスでのブレークポイントの検証
ブレークポイントは、デバッガーで実行されている特定の時点でプログラムの実行を停止する必要があることを示します。 ブレークポイントの有効な場所を構成する内容についての情報がエディターに含まれていないため、ソースファイル内の任意の行にブレークポイントを設定できます。 デバッガーを起動すると、マークされているすべてのブレークポイント (保留中のブレークポイントと呼ばれます) が、実行中のプログラム内の適切な場所にバインドされます。 同時に、有効なコードの場所をマークするようにブレークポイントが検証されます。 たとえば、コメントのブレークポイントは無効です。これは、ソースコード内のその場所にコードがないためです。 デバッガーは無効なブレークポイントを無効にします。

 言語サービスは表示されているソースコードを認識しているため、デバッガーを起動する前にブレークポイントを検証できます。 メソッドをオーバーライドして、 <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> ブレークポイントの有効な位置を指定するスパンを返すことができます。 デバッガーが起動されてもブレークポイントの位置は検証されますが、ユーザーにはデバッガーが読み込まれるのを待たずに無効なブレークポイントが通知されます。

## <a name="implementing-support-for-validating-breakpoints"></a>ブレークポイントの検証のサポートの実装

- <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A>メソッドには、ブレークポイントの位置が指定されます。 実装では、位置が有効であるかどうかを判断し、ブレークポイントの位置に関連付けられているコードを識別するテキスト範囲を返すことによってこれを示す必要があります。

- <xref:Microsoft.VisualStudio.VSConstants.S_OK>位置が有効である場合はを返し、有効でない場合はを返し <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> ます。

- ブレークポイントが有効な場合、テキスト範囲はブレークポイントと共に強調表示されます。

- ブレークポイントが無効である場合は、エラーメッセージがステータスバーに表示されます。

### <a name="example"></a>例
 この例では、パーサーを <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> 呼び出して、指定した位置にあるコード (存在する場合) の範囲を取得するメソッドの実装を示します。

 この例では、 `GetCodeSpan` <xref:Microsoft.VisualStudio.Package.AuthoringSink> テキスト範囲を検証するクラスにメソッドを追加し、 `true` それが有効なブレークポイントの位置である場合はを返すことを前提としています。

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
