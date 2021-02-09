---
title: 従来の言語サービスの構文色分け |Microsoft Docs
description: 従来の言語サービスで構文の色付けをサポートする方法については、構文要素またはトークンの種類を識別できるパーサーまたはスキャナーを用意する方法に関するページを参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 14fc4a44a85171d209ec227f20e47775b34be22d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898261"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>従来の言語サービスでの構文の配色変更
構文の色づけは、プログラミング言語のさまざまな要素を異なる色やスタイルのソースファイルに表示する機能です。 この機能をサポートするには、ファイル内の字句要素またはトークンの種類を識別できるパーサーまたはスキャナーを用意する必要があります。 多くの言語では、キーワード、区切り記号 (かっこや中かっこなど)、コメントを区別するためにさまざまな方法で色分けしています。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 詳細については、「 [エディターと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="implementation"></a>実装
 色付けをサポートするために、マネージパッケージフレームワーク (MPF) には、 <xref:Microsoft.VisualStudio.Package.Colorizer> インターフェイスを実装するクラスが含まれてい <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> ます。 このクラスは、と対話して <xref:Microsoft.VisualStudio.Package.IScanner> トークンと色を決定します。 スキャナーの詳細については、「 [従来の言語サービスパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」を参照してください。 次に、クラスは、 <xref:Microsoft.VisualStudio.Package.Colorizer> トークンの各文字に色情報をマークし、その情報をソースファイルを表示するエディターに返します。

 エディターに返されるカラー情報は、装飾項目の一覧のインデックスです。 各装飾項目は、カラー値と、太字や取り消し線などのフォント属性のセットを指定します。 このエディターには、言語サービスで使用できる既定の装飾項目のセットが用意されています。 必要なのは、トークンの種類ごとに適切な色のインデックスを指定することだけです。 ただし、カスタム装飾項目のセットと、トークン用に提供するインデックスを指定し、既定のリストではなく、独自の装飾項目のリストを参照することができます。 また、 `RequestStockColors` カスタムの色をサポートするには、レジストリエントリを0に設定する (またはエントリをまったく指定しない) 必要があり `RequestStockColors` ます。 このレジストリエントリは、名前付きパラメーターを使用して <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> ユーザー定義属性に設定できます。 言語サービスの登録とそのオプションの設定の詳細については、「 [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください。

## <a name="custom-colorable-items"></a>カスタムの配色可能な項目
 独自のカスタム装飾アイテムを指定するには、クラスのメソッドとメソッドをオーバーライドする必要があり <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> ます。 最初のメソッドは、言語サービスがサポートするカスタム装飾項目の数を返します。2番目のメソッドは、インデックスを使用してカスタム装飾項目を取得します。 カスタム装飾項目の既定の一覧を作成します。 言語サービスのコンストラクターでは、各装飾項目に名前を指定するだけで済みます。 ユーザーが別の装飾項目のセットを選択した場合は、Visual Studio によって自動的に処理されます。 この名前は、[**オプション**] ダイアログボックス (Visual Studio の [**ツール**] メニューから利用可能) の [**フォントおよび色**] プロパティページに表示されます。この名前によって、ユーザーが上書きした色が決まります。 ユーザーの選択は、レジストリのキャッシュに格納され、色の名前によってアクセスされます。 [ **フォントおよび色** ] プロパティページには、すべての色名がアルファベット順に一覧表示されるため、各色の名前の前に使用する言語名を使用して、カスタムの色をグループ化できます。たとえば、"**Testlanguage-Comment**" や "**Testlanguage-Keyword**" などです。 または、「**Comment (testlanguage)**」と「**Keyword (testlanguage)**」と入力して、装飾項目をグループ化することもできます。 言語名でグループ化することをお勧めします。

> [!CAUTION]
> 既存の装飾項目名との競合を避けるために、装飾項目名に言語名を含めることを強くお勧めします。

> [!NOTE]
> 開発中にいずれかの色の名前を変更した場合は、最初に色にアクセスしたときに Visual Studio によって作成されたキャッシュをリセットする必要があります。 これを行うには、Visual Studio SDK の [プログラム] メニューから [ **実験用ハイブのリセット** ] コマンドを実行します。

 装飾項目の一覧の最初の項目が参照されないことに注意してください。 Visual Studio では、常に、その項目の既定のテキストの色と属性が提供されます。 これを処理する最も簡単な方法は、プレースホルダー装飾 item を最初の項目として指定することです。

### <a name="high-color-colorable-items"></a>High Color 装飾 Items
 装飾項目では、インターフェイスを使用して、24ビットまたは高色の値をサポートすることもでき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> ます。 MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> クラスはインターフェイスをサポートし、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> 24 ビットの色は通常の色と共にコンストラクターで指定されます。 詳細については、<xref:Microsoft.VisualStudio.Package.ColorableItem> クラスのトピックを参照してください。 次の例は、キーワードとコメントに24ビットの色を設定する方法を示しています。 24ビット色は、ユーザーのデスクトップで24ビットカラーがサポートされている場合に使用されます。それ以外の場合は、通常のテキストの色が使用されます。

 これらは言語の既定の色であることに注意してください。ユーザーは、必要に応じてこれらの色を変更できます。

### <a name="example"></a>例
 この例では、クラスを使用してカスタム装飾項目の配列を宣言および設定する方法の1つを示し <xref:Microsoft.VisualStudio.Package.ColorableItem> ます。 この例では、24ビットカラーを使用して、キーワードとコメントの色を設定します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private ColorableItem[] m_colorableItems;

        TestLanguageService() : base()
        {
            m_colorableItems = new ColorableItem[] {
                new ColorableItem("TestLanguage - Text",
                                  "Text",
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.Empty,
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT),
                new ColorableItem("TestLanguage - Keyword",
                                  "Keyword",
                                  COLORINDEX.CI_MAROON,
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,
                                  System.Drawing.Color.FromArgb(192,32,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_BOLD),
                new ColorableItem("TestLanguage - Comment",
                                  "Comment",
                                  COLORINDEX.CI_DARKGREEN,
                                  COLORINDEX.CI_LIGHTGRAY,
                                  System.Drawing.Color.FromArgb(32,128,32),
                                  System.Drawing.Color.Empty,
                                  FONTFLAGS.FF_DEFAULT)
                // ...
                // Add as many colorable items as you want to support.
            };
        }
    }
}
```

## <a name="the-colorizer-class-and-the-scanner"></a>Colorizer クラスとスキャナー
 基底 <xref:Microsoft.VisualStudio.Package.LanguageService> クラスには、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> クラスを instantiantes するメソッドがあり <xref:Microsoft.VisualStudio.Package.Colorizer> ます。 メソッドから返されるスキャナーは、 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> クラスコンストラクターに渡され <xref:Microsoft.VisualStudio.Package.Colorizer> ます。

 独自のバージョンのクラスでメソッドを実装する必要があり <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> ます。 クラスは、スキャナーを使用して、 <xref:Microsoft.VisualStudio.Package.Colorizer> すべてのトークンカラー情報を取得します。

 スキャナーは、 <xref:Microsoft.VisualStudio.Package.TokenInfo> 検出されたすべてのトークンの構造を設定する必要があります。 この構造体には、トークンが占有する範囲、使用する色インデックス、トークンの種類、トークントリガー (「」を参照) などの情報が含まれてい <xref:Microsoft.VisualStudio.Package.TokenTriggers> ます。 クラスによる色付けに必要なのは、span と color インデックスだけです <xref:Microsoft.VisualStudio.Package.Colorizer> 。

 構造体に格納されているカラーインデックス <xref:Microsoft.VisualStudio.Package.TokenInfo> は、通常、列挙型の値です。この値には、 <xref:Microsoft.VisualStudio.Package.TokenColor> キーワードや演算子など、さまざまな言語要素に対応する複数の名前付きインデックスが用意されています。 カスタム装飾 items リストが列挙に示されている項目と一致する場合は、 <xref:Microsoft.VisualStudio.Package.TokenColor> 列挙体を各トークンの色としてのみ使用できます。 ただし、追加の装飾項目がある場合、または既存の値をその順序で使用しない場合は、必要に応じてカスタム装飾項目リストを配置し、そのリストに適切なインデックスを返すことができます。 構造に格納する場合は、インデックスをにキャストするだけで済み <xref:Microsoft.VisualStudio.Package.TokenColor> <xref:Microsoft.VisualStudio.Package.TokenInfo> ます。はインデックスのみを表示し [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] ます。

### <a name="example"></a>例
 次の例では、スキャナーが3種類のトークンを識別する方法を示します。数値、句読点、識別子 (数字または句読点ではないもの) です。 この例は、説明を目的としたものであり、包括的なパーサーとスキャナーの実装を表しているわけではありません。 これは、文字列を返すメソッドを持つクラスがあることを前提としてい `Lexer` `GetNextToken()` ます。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    private Lexer lex;

    public class TestScanner : IScanner
    {
        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                }
                else if (Char.IsNumber(firstChar))
                {
                    tokenInfo.Type = TokenType.Literal;
                    tokenInfo.Color = TokenColor.Number;
                }
                else
                {
                    tokenInfo.Type = TokenType.Identifier;
                    tokenInfo.Color = TokenColor.Identifier;
                }
            }
            return foundToken;
        }
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
