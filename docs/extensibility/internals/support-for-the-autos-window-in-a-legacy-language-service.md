---
title: 旧式言語サービスの自動ウィンドウのサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 75f8c761721dde5dad4bb75b8675f71f678b06df
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704884"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>従来の言語サービスでの自動変数ウィンドウのサポート
**Autos**ウィンドウには、デバッグ中のプログラムが一時停止したとき (ブレークポイントまたは例外が原因で) スコープ内の変数やパラメーターなどの式が表示されます。 式には、ローカルまたはグローバル変数、およびローカル スコープで変更されたパラメーターを含めることができます。 **また、[自動**変数] ウィンドウには、クラス、構造体、またはその他の型のインスタンス化を含めることもできます。 式エバリュエーターが評価できるものは **、[自動**変数] ウィンドウに表示される可能性があります。

 管理パッケージ フレームワーク (MPF) は **、[自動**変数] ウィンドウを直接サポートしません。 ただし、メソッドをオーバーライドした<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A>場合は、[自動変数] ウィンドウに表示される式の一覧**を**返すことができます。

## <a name="implementing-support-for-the-autos-window"></a>自動ウィンドウのサポートの実装
 **Autos**ウィンドウをサポートするために必要なのは、<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A><xref:Microsoft.VisualStudio.Package.LanguageService>クラスにメソッドを実装することだけです。 ソース ファイル内の場所を指定して、どの式を **[自動**変数] ウィンドウに表示するかを実装で決定する必要があります。 このメソッドは、各文字列が 1 つの式を表す文字列のリストを返します。 の戻り値<xref:Microsoft.VisualStudio.VSConstants.S_OK>は、リストに式が含まれていること<xref:Microsoft.VisualStudio.VSConstants.S_FALSE>を示し、表示する式がないことを示します。

 返される実際の式は、コード内のその位置に表示される変数またはパラメーターの名前です。 これらの名前は式エバリュエーターに渡され、値と型を取得し、その後**Autos**ウィンドウに表示されます。

### <a name="example"></a>例
 次の例は、解析の理由<xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A><xref:Microsoft.VisualStudio.Package.ParseReason>を使用してメソッドから式のリストを<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>取得するメソッドの実装を示しています。 各式は、インターフェイスを実装する`TestVsEnumBSTR`としてラップされます<xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR>。

 メソッドと`GetAutoExpressionsCount``GetAutoExpression`メソッドはオブジェクトの`TestAuthoringSink`カスタム メソッドであり、この例をサポートするために追加されました。 パーサーによってオブジェクトに追加された式に (`TestAuthoringSink`<xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A>メソッドを呼び出すことによって) パーサーの外部からアクセスできる方法を表します。

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
