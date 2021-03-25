---
title: 従来の言語サービスでのアウトライン |Microsoft Docs
description: 従来の言語サービスでの非表示領域の実装によってアウトラインをサポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a56d755341aa611f0e2762f6bae8940778fe0864
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062955"
---
# <a name="outlining-in-a-legacy-language-service"></a>従来の言語サービスのアウトライン
アウトラインを使用すると、複雑なプログラムを概要やアウトラインに折りたたむことができます。 たとえば、C# では、メソッドのシグネチャのみを表示して、すべてのメソッドを1つの行に折りたたむことができます。 また、構造体とクラスを折りたたんで、構造体とクラスの名前のみを表示することもできます。 1つのメソッド内で、、、などのステートメントの最初の行のみを表示することにより、複雑なロジックを折りたたんでフロー全体を表示することができ `foreach` `if` `while` ます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [チュートリアル: アウトライン](../../extensibility/walkthrough-outlining.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="enabling-support-for-outlining"></a>アウトラインのサポートを有効にする
 `AutoOutlining`自動アウトラインを有効にするには、レジストリエントリを1に設定します。 自動アウトラインでは、隠し領域を識別してアウトライングリフを表示するために、ファイルの読み込み時または変更時にソース全体の解析が設定されます。 アウトラインは、ユーザーが手動で制御することもできます。

 レジストリエントリの値は、 `AutoOutlining` クラスのプロパティを使用して取得でき <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> <xref:Microsoft.VisualStudio.Package.LanguagePreferences> ます。 `AutoOutlining`レジストリエントリは、属性の名前付きパラメーターを使用して初期化でき <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ます (詳細について[は、「従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。

## <a name="the-hidden-region"></a>非表示領域
 アウトラインを提供するには、言語サービスが非表示領域をサポートしている必要があります。 これらは、展開または折りたたむことができるテキストの範囲です。 非表示の領域は、標準の言語シンボル (中かっこなど) またはカスタムシンボルで区切ることができます。 たとえば、C# には、 `#region` / `#endregion` 非表示の領域を区切るペアがあります。

 非表示の領域は、インターフェイスとして公開されている非表示の領域マネージャーによって管理され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> ます。

 アウトラインでは、非表示領域を使用してインターフェイスを使用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion> し、非表示領域のスパン、現在の表示状態、およびスパンが折りたたまれているときに表示されるバナーを格納します。

 言語サービスパーサーは、メソッドを使用して、 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> 非表示領域の既定の動作を持つ新しい非表示領域を追加します。一方、メソッドを使用すると、 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> アウトラインの外観と動作をカスタマイズできます。 非表示の領域が非表示の領域セッションに与えられると、は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 言語サービスの非表示領域を管理します。

 非表示の領域セッションが破棄されるタイミングを判断する必要がある場合、非表示の領域を変更する場合、または特定の非表示領域が表示されるようにする必要がある場合は、クラスからクラスを派生させ、 <xref:Microsoft.VisualStudio.Package.Source> それぞれ適切なメソッドである、、、をオーバーライドする必要があり <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A> <xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A> <xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A> ます。

### <a name="example"></a>例
 中かっこのすべてのペアに対して非表示の領域を作成する簡単な例を次に示します。 この言語では、中かっこの照合が提供され、照合する中かっこには少なくとも中かっこ ({と}) が含まれていることを前提としています。 この方法は、説明を目的としたものです。 完全な実装では、のケースを完全に処理 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> できます。 この例では、設定を一時的にに設定する方法も示して <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> `true` います。 別の方法とし `AutoOutlining` て、言語パッケージの属性に名前付きパラメーターを指定することも `ProvideLanguageServiceAttribute` できます。

 この例では、コメント、文字列、およびリテラルに対する C# の規則を前提としています。

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

## <a name="see-also"></a>こちらもご覧ください
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
