---
title: レガシー言語サービスでのアウトライン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be485a0e7406d49c4dcce77958c720e0b62504b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706810"
---
# <a name="outlining-in-a-legacy-language-service"></a>従来の言語サービスのアウトライン
アウトラインを使用すると、複雑なプログラムを概要またはアウトラインに集約できます。 たとえば、C# では、すべてのメソッドを 1 行に折りたたんで、メソッド シグネチャのみを表示できます。 さらに、構造体とクラスを折りたたんで、構造体とクラスの名前だけを表示することもできます。 1 つのメソッド内では、 `foreach` `if`、 などのステートメントの最初の行だけを表示することで、複雑なロジックを折りたたんで全体的`while`なフローを表示できます。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[チュートリアル: アウトライン](../../extensibility/walkthrough-outlining.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="enabling-support-for-outlining"></a>アウトラインのサポートを有効にする
 `AutoOutlining`レジストリ エントリは 1 に設定され、アウトラインの自動表示が有効になります。 自動アウトライン表示では、ファイルが読み込まれるか変更されたときに、隠れた領域を識別してアウトライングリフを表示するために、ソース全体の解析が設定されます。 アウトラインは、ユーザーが手動で制御することもできます。

 レジストリ エントリの`AutoOutlining`値は、<xref:Microsoft.VisualStudio.Package.LanguagePreferences>クラスのプロパティを<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A>通じて取得できます。 レジストリ`AutoOutlining`エントリは、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性の名前付きパラメーターで初期化できます (詳細については、[レガシ言語サービスの登録を](../../extensibility/internals/registering-a-legacy-language-service1.md)参照してください)。

## <a name="the-hidden-region"></a>隠れた領域
 アウトラインを提供するには、言語サービスが非表示の領域をサポートしている必要があります。 これらは、展開または折りたたむことができるテキストの範囲です。 隠し領域は、中かっこなどの標準言語シンボルまたはカスタム シンボルで区切ることができます。 たとえば、C# には、`#region`/`#endregion`非表示の領域を区切るペアがあります。

 非表示の領域は、インターフェイスとして公開されている非表示の領域マネージャーによって管理されます<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>。

 アウトラインでは、インターフェイスを非表示の<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion>領域を使用し、非表示領域の範囲、現在の表示状態、およびスパンが折りたたまれたときに表示されるバナーを含みます。

 言語サービス パーサーは<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A>、このメソッドを使用して、非表示領域の既定の動作を持つ新しい非表示<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A>領域を追加します。 非表示の領域が非表示の領域セッションに与えられると[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、言語サービスの非表示領域を管理します。

 非表示領域セッションがいつ破棄されるか、非表示の領域が変更されたか、特定の非表示領域が表示されていることを確認する必要がある場合。クラスから派生したクラス<xref:Microsoft.VisualStudio.Package.Source>は、 <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A>、<xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A>および 、 、および<xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A>のそれぞれをオーバーライドする必要があります。

### <a name="example"></a>例
 ここでは、すべての中かっこのペアに対して非表示の領域を作成する簡単な例を示します。 言語は中かっこの一致を提供し、一致する中かっこには少なくとも中かっこ ({と }) が含まれると仮定されます。 この方法は、説明のみを目的とします。 完全な実装では、 のケースの完全な処理<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>が行われます。 この例では、一時的にプ<xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A>リファレンスを`true`設定する方法も示します。 別の方法として、言語`AutoOutlining`パッケージの`ProvideLanguageServiceAttribute`属性に名前付きパラメーターを指定します。

 この例では、コメント、文字列、およびリテラルに対する C# 規則を想定しています。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{

    public class MyLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences  GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(MyLanguageService).GUID,
                                                        Name);
                m_preferences.Init();
                // Temporarily enabled auto-outlining
                m_preferences.AutoOutlining = true;
            }
            return m_preferences;
        }

        public override AuthoringScope  ParseSource(ParseRequest req)
        {
            Source source = (Source) this.GetSource(req.FileName);
            switch (req.Reason)
            {
               case ParseReason.HighlightBraces:
               case ParseReason.MatchBraces:
               case ParseReason.MemberSelectAndHighlightBraces:
                  if (source.Braces != null)
                  {
                      foreach (TextSpan[] brace in source.Braces)
                      {
                         if (brace.Length == 2)
                         {
                             if (req.Sink.HiddenRegions == true
                                   && source.GetText(brace[0]).Equals("{")
                                   && source.GetText(brace[1]).Equals("}"))
                             {
                                //construct a TextSpan of everything between the braces
                                TextSpan hideSpan = new TextSpan();
                                hideSpan.iStartIndex = brace[0].iStartIndex;
                                hideSpan.iStartLine = brace[0].iStartLine;
                                hideSpan.iEndIndex = brace[1].iEndIndex;
                                hideSpan.iEndLine = brace[1].iEndLine;
                                req.Sink.ProcessHiddenRegions = true;
                                req.Sink.AddHiddenRegion(hideSpan);
                             }
                             req.Sink.MatchPair(brace[0], brace[1], 1);
                         }
                         else if (brace.Length >= 3)
                             req.Sink.MatchTriple(brace[0], brace[1], brace[2], 1);
                  }
        }
                   break;
               default:
                   break;
      }
            // Must always return a valid AuthoringScope object.
            return new MyAuthoringScope();
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
