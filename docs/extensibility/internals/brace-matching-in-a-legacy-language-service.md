---
title: 従来の言語サービスでの中かっこの照合 |Microsoft Docs
description: 従来の言語サービスでの中かっこの照合について説明します。これは、かっこや中かっこなど、一緒に出現する必要がある言語要素を追跡するのに役立ちます。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 7d9f93f0081d45e986ab6845cdaee53209b84e13
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190006"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>従来の言語サービスでの中かっこの照合
かっこの照合により、開発者は、かっこや中かっこなど、一緒に出現する必要がある言語要素を追跡できます。 開発者が右中かっこを入力すると、左中かっこが強調表示されます。

 2つまたは3つの同時実行要素 (ペアと3要素と呼ばれます) を一致させることができます。 3要素は、3つの同時実行要素のセットです。 たとえば、C# では、ステートメントは、、、 `foreach` およびの3つのを形成し `foreach()` `{` `}` ます。 右中かっこを入力すると、3つの要素がすべて強調表示されます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 かっこの一致を実装する新しい方法の詳細については、「 [チュートリアル: 一致する中かっこの表示](../../extensibility/walkthrough-displaying-matching-braces.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

 クラスは、メソッドとメソッドを使用して、 <xref:Microsoft.VisualStudio.Package.AuthoringSink> ペアと3要素の両方をサポートし <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A> ます。

## <a name="implementation"></a>実装
 言語サービスでは、言語で一致したすべての要素を識別し、一致するすべてのペアを見つける必要があります。 通常、これを行うには、を実装して、 <xref:Microsoft.VisualStudio.Package.IScanner> 一致する言語を検出し、メソッドを使用して <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 要素を照合します。

 メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> スキャナーを呼び出して行をトークン化し、カレットの直前にトークンを返します。 スキャナーは、現在のトークンにのトークントリガー値を設定することによって、言語要素のペアが見つかったことを示してい <xref:Microsoft.VisualStudio.Package.TokenTriggers> ます。 メソッドは、メソッドを呼び出します。メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A> 解析理由値を指定してメソッドを呼び出し、 <xref:Microsoft.VisualStudio.Package.ParseReason> 一致する言語要素を検索します。 一致する言語要素が見つかると、両方の要素が強調表示されます。

 中かっこの強調表示をトリガーする方法の詳細については、「[従来の言語サービスパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」の「*解析操作の例*」セクションを参照してください。

## <a name="enable-support-for-brace-matching"></a>中かっこの照合のサポートを有効にする
 属性では、 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> クラスの対応するプロパティを設定する **matchbraces**、 **MatchBracesAtCaret**、および **ShowMatchingBrace** レジストリエントリを設定でき <xref:Microsoft.VisualStudio.Package.LanguagePreferences> ます。 言語設定のプロパティは、ユーザーが設定することもできます。

|レジストリ エントリ|プロパティ|説明|
|--------------------|--------------|-----------------|
|MatchBraces|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|中かっこの照合を有効にします。|
|MatchBracesAtCaret|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|キャレットの移動に合わせて中かっこの照合を有効にします。|
|ShowMatchingBrace|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|対応する中かっこを強調表示します。|

## <a name="match-conditional-statements"></a>一致する条件ステートメント
 、、およびなどの条件付きステートメントを一致させることができ `if` `else if` `else` `#if` `#elif` ます。また、 `#else` `#endif` 区切り記号と同じ方法で、、、、を使用することもできます。 クラスをサブクラス化 <xref:Microsoft.VisualStudio.Package.AuthoringSink> し、区切り記号だけでなくテキスト範囲を一致する要素の内部配列に追加できるメソッドを提供できます。

## <a name="set-the-trigger"></a>トリガーを設定する
 次の例では、一致するかっこ、中かっこ、中かっこを検出し、スキャナーでトリガーを設定する方法を示します。 クラスのメソッドは、 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> <xref:Microsoft.VisualStudio.Package.Source> トリガーを検出し、パーサーを呼び出して一致するペアを検索します (この記事の「 *一致の検索* 」セクションを参照してください)。 この例は、説明を目的としたものです。 スキャナーには、 `GetNextToken` テキスト行からトークンを識別して返すメソッドが含まれていることを前提としています。

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

## <a name="match-the-braces"></a>中かっこと一致します
 言語要素、 `{ }` 、およびを照合し、それらの `( )` `[ ]` 範囲をオブジェクトに追加するための簡略化された例を次に示し <xref:Microsoft.VisualStudio.Package.AuthoringSink> ます。 この方法は、ソースコードを解析するために推奨される方法ではありません。これは説明を目的としたものです。

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
- [従来の言語サービスパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
