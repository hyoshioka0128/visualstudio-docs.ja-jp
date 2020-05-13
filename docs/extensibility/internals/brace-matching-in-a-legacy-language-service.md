---
title: 従来の言語サービスでのブレースのマッチング |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- brace matching
- language services [managed package framework], brace matching
ms.assetid: 4e3d0a70-f22f-49dd-92d8-edf48ab62b52
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0081be3e3ab5a53f7d85f77475d4288aa5c87092
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709819"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>従来の言語サービスでのブレースのマッチング
かっこの一致は、かっこや中かっこなど、一緒に出現する必要がある言語要素を開発者が追跡するのに役立ちます。 開発者が右中かっこを入力すると、左中かっこが強調表示されます。

 ペアとトリプルと呼ばれる 2 つまたは 3 つの共に発生する要素を照合できます。 トリプルは、3 つの共に発生する要素のセットです。 たとえば、C# では、ステートメント`foreach`はトリプル`foreach()`、、、、`{`および`}`を形成します。 右中かっこを入力すると、3 つの要素すべてが強調表示されます。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 かっこの一致を実装する新しい方法の詳細については、「[チュートリアル: 一致するかっこを表示](../../extensibility/walkthrough-displaying-matching-braces.md)する 」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 この<xref:Microsoft.VisualStudio.Package.AuthoringSink>クラスは、 メソッドと メソッドを<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A>使用<xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A>してペアとトリプルの両方をサポートします。

## <a name="implementation"></a>実装
 言語サービスは、言語で一致したすべての要素を識別し、一致するすべてのペアを見つける必要があります。 これは通常、一致する<xref:Microsoft.VisualStudio.Package.IScanner>言語を検出し、メソッドを<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>使用して要素を一致させることによって実現されます。

 この<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>メソッドは、スキャナーを呼び出して、行をトークン化し、キャレットの直前にトークンを返します。 スキャナーは、現在のトークンのトークン トリガー値を設定することで、言語要素の<xref:Microsoft.VisualStudio.Package.TokenTriggers>ペアが見つかったことを示します。 メソッド<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>は、メソッド<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>を呼び出し、<xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A>解析理由の値を指定<xref:Microsoft.VisualStudio.Package.ParseReason>してメソッドを呼び出して、一致する言語要素を見つけます。 一致する言語要素が見つかると、両方の要素が強調表示されます。

 中かっこを入力すると中かっこの強調表示が行われますの詳細については、「[従来の言語サービス のパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」の「*解析操作の例*」を参照してください。

## <a name="enable-support-for-brace-matching"></a>かっこの一致のサポートを有効にする
 この<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>属性は、クラスの対応するプロパティを設定する<xref:Microsoft.VisualStudio.Package.LanguagePreferences>MatchBraces、MatchBracesAtCaret、および**ShowMatchingBrace**レジストリ エントリを設定できます。 **MatchBraces** **MatchBracesAtCaret** 言語設定プロパティは、ユーザーが設定することもできます。

|レジストリ エントリ|プロパティ|説明|
|--------------------|--------------|-----------------|
|マッチブレース|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|かっこの一致を有効にします。|
|マッチブレイスアットカレト|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|キャレットが移動する場合に、ブレースの一致を有効にします。|
|マッチングブレースを表示します。|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|一致するブレースを強調表示します。|

## <a name="match-conditional-statements"></a>条件ステートメントの一致
 、 `if`、 `else if` `else` `#if` `#elif`、 、 、 、 、 、 などの条件ステートメントを、一致する区切り記号と同じ方法で照合できます。 `#else` `#endif` クラスをサブクラス化<xref:Microsoft.VisualStudio.Package.AuthoringSink>し、テキスト範囲と区切り文字を一致する要素の内部配列に追加できるメソッドを提供できます。

## <a name="set-the-trigger"></a>トリガーの設定
 次の例は、かっこ、中かっこ、および四角かっこを検出し、スキャナーでそのトリガーを設定する方法を示しています。 クラス<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>の<xref:Microsoft.VisualStudio.Package.Source>メソッドはトリガーを検出し、パーサーを呼び出して一致するペアを見つけます (この記事の「*一致を見つける*」セクションを参照)。 この例は、説明のみを目的とします。 この例では、スキャナーに、テキスト`GetNextToken`行からトークンを識別して返すメソッドが含まれていることを前提としています。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private const string braces = "()[]{}";
        private Lexer lex;

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar) && token.Length > 0)
                {
                    if (braces.IndexOf(firstChar) != -1)
                    {
                        tokenInfo.Trigger = TokenTriggers.MatchBraces;
                    }
                }
            }
            return foundToken;
        }
```

## <a name="match-the-braces"></a>中かっこを一致させる
 言語要素`{ }`、、および を照合し`( )``[ ]`、その範囲をオブジェクトに追加する簡単な例を<xref:Microsoft.VisualStudio.Package.AuthoringSink>次に示します。 この方法は、ソース コードを解析する場合に推奨される方法ではありません。それは説明の目的のためだけである。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class Parser
    {
         private IList<TextSpan[]> m_braces;
         public IList<TextSpan[]> Braces
         {
             get { return m_braces; }
         }
         private void AddMatchingBraces(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             if IsMatch(braceSpan1, braceSpan2)
                 m_braces.Add(new TextSpan[] { braceSpan1, braceSpan2 });
         }

         private bool IsMatch(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             //definition for matching here
          }
    }

    public class TestLanguageService : LanguageService
    {
         Parser parser = new Parser();
         Source source = (Source) this.GetSource(req.FileName);

         private AuthoringScope ParseSource(ParseRequest req)
         {
             if (req.Sink.BraceMatching)
             {
                 if (req.Reason==ParseReason.MatchBraces)
                 {
                     foreach (TextSpan[] brace in parser.Braces)
                     {
                         req.Sink.MatchPair(brace[0], brace[1], 1);
                     }
                 }
             }
             return new TestAuthoringScope();
         }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービス機能](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービス パーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
