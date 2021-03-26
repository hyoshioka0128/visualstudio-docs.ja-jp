---
title: 従来の言語サービスで [自動変数] ウィンドウをサポートする
description: '[自動変数] ウィンドウのサポートを実装する方法について説明します。このウィンドウには、デバッグ中のプログラムが一時停止したときにスコープ内にある式が表示されます。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 70a8697027cde07ca2b30d01a73a80d771155c5c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080633"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>従来の言語サービスの [自動変数] ウィンドウのサポート

[ **自動変数** ] ウィンドウには、デバッグ中のプログラムが一時停止されている場合 (ブレークポイントまたは例外によって)、スコープ内にある変数やパラメーターなどの式が表示されます。 式には、変数、ローカルまたはグローバル、およびローカルスコープで変更されたパラメーターを含めることができます。 [ **自動変数** ] ウィンドウには、クラス、構造体、またはその他の型のインスタンス化を含めることもできます。 式エバリュエーターで評価できるものは、[ **自動変数** ] ウィンドウに表示される可能性があります。

 Managed package framework (MPF) では、[ **自動変数** ] ウィンドウの直接サポートは提供されません。 ただし、メソッドをオーバーライドする場合は、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> [ **自動変数** ] ウィンドウに表示される式の一覧を返すことができます。

## <a name="implementing-support-for-the-autos-window"></a>[自動変数] ウィンドウのサポートの実装

 [ **自動変数** ] ウィンドウをサポートするために必要なのは、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> クラスにメソッドを実装することだけです <xref:Microsoft.VisualStudio.Package.LanguageService> 。 の実装では、ソースファイル内の場所を指定して、[ **自動変数** ] ウィンドウに式を表示する必要があることを決定する必要があります。 メソッドは、各文字列が単一の式を表す文字列のリストを返します。 戻り値は、 <xref:Microsoft.VisualStudio.VSConstants.S_OK> リストに式が含まれていることを示し、 <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> は表示する式が存在しないことを示します。

 実際に返される式は、コード内のその場所に表示される変数またはパラメーターの名前です。 これらの名前は、式エバリュエーターに渡され、値と型を取得して、[ **自動変数** ] ウィンドウに表示されます。

### <a name="example"></a>例
 次の例は、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 解析理由を使用してメソッドから式のリストを取得するメソッドの実装を示して <xref:Microsoft.VisualStudio.Package.ParseReason> います。 各式は、インターフェイスを実装するとしてラップされ `TestVsEnumBSTR` <xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> ます。

 `GetAutoExpressionsCount` `GetAutoExpression` メソッドとメソッドは、オブジェクトのカスタムメソッドであり、 `TestAuthoringSink` この例をサポートするために追加されています。 これは、パーサーに `TestAuthoringSink` よって (メソッドを呼び出すことによって) オブジェクトに追加された式 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> がパーサーの外部でアクセスできる1つの方法を表します。

```csharp
using Microsoft.VisualStudio;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        public override int GetProximityExpressions(IVsTextBuffer buffer,
                                                    int line,
                                                    int col,
                                                    int cLines,
                                                    out IVsEnumBSTR ppEnum)
        {
            int retval = VSConstants.E_NOTIMPL;
            ppEnum = null;
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
                                                              ParseReason.Autos,
                                                              null);
                        req.Scope = this.ParseSource(req);
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;

                        retval = VSConstants.S_FALSE;
                        int spanCount = sink.GetAutoExpressionsCount();
                        if (spanCount > 0) {
                            TestVsEnumBSTR bstrList = new TestVsEnumBSTR();
                            for (int i = 0; i < spanCount; i++)
                            {
                                TextSpan span;
                                sink.GetAutoExpression(i, out span);
                                string expression = src.GetText(span.iStartLine,
                                                                span.iStartIndex,
                                                                span.iEndLine,
                                                                span.iEndIndex);
                                bstrList.AddString(expression);
                            }
                            ppEnum = bstrList;
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
