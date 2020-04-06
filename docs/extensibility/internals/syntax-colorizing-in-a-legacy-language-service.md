---
title: 従来の言語サービスでの構文の色分け |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 02723a09254255b98291cb921ae5ec091d8b9859
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704709"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>従来の言語サービスでの構文の配色変更
構文の色付けは、プログラミング言語のさまざまな要素をソース ファイルに異なる色とスタイルで表示する機能です。 この機能をサポートするには、ファイル内の字句要素またはトークンの種類を識別できるパーサーまたはスキャナーを提供する必要があります。 多くの言語では、キーワード、区切り記号 (かっこや中かっこなど) を区別し、さまざまな方法で色分けします。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[エディタと言語サービスの拡張](../../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="implementation"></a>実装
 色付けをサポートするために、マネージ パッケージ フレームワーク (MPF) には、<xref:Microsoft.VisualStudio.Package.Colorizer>インターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>を実装するクラスが含まれています。 このクラスは、 と<xref:Microsoft.VisualStudio.Package.IScanner>やり取りしてトークンと色を決定します。 スキャナーの詳細については、「[レガシ言語サービス パーサーおよびスキャナ](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」を参照してください。 次<xref:Microsoft.VisualStudio.Package.Colorizer>に、このクラスは、トークンの各文字に色情報をマークし、その情報をソース ファイルを表示するエディターに返します。

 エディターに返される色情報は、カラー化可能な項目のリストへのインデックスです。 各色付け可能な項目は、色の値と、太字や取り消し線などのフォント属性のセットを指定します。 エディターには、言語サービスで使用できる既定の色指定可能な項目のセットが用意されています。 必要な操作は、各トークンタイプに適切なカラーインデックスを指定することだけです。 ただし、トークンに指定したカスタムの色付け可能な項目とインデックスのセットを提供し、既定のリストではなく独自の色付け可能な項目のリストを参照できます。 カスタムカラーを`RequestStockColors`サポートするには、レジストリ エントリを 0 に設定`RequestStockColors`する必要があります (または、エントリをまったく指定しないでください)。 このレジストリ エントリは、ユーザー定義の属性に名前<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>付きパラメーターを使用して設定できます。 言語サービスの登録とそのオプションの設定の詳細については、「[レガシ言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください。

## <a name="custom-colorable-items"></a>カスタムの配色可能な項目
 独自の色付け可能な項目を指定するには、クラス<xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A>の<xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A>メソッドと<xref:Microsoft.VisualStudio.Package.LanguageService>メソッドをオーバーライドする必要があります。 最初のメソッドは、言語サービスがサポートするカスタムの色付け可能な項目の数を返し、2 番目のメソッドは、インデックスによってカスタムの色付け可能な項目を取得します。 カスタムの色付け可能な項目の既定のリストを作成します。 言語サービスのコンストラクターでは、各色分け可能な項目に名前を指定するだけで済みます。 Visual Studio は、ユーザーが異なる色付け可能な項目のセットを選択する場合に自動的に処理します。 この名前は **、[オプション]** ダイアログ ボックスの [**フォントと色**] プロパティ ページに表示される名前で (Visual Studio**の [ツール]** メニューから)、この名前によってユーザーがどの色をオーバーライドするかが決まります。 ユーザーの選択内容はレジストリのキャッシュに格納され、カラー名によってアクセスされます。 **[フォントと色]** プロパティ ページには、すべての色名がアルファベット順に表示されるので、各色名の前に言語名を付けてカスタム色をグループ化できます。たとえば **、" テスト言語 - コメント**" と "**テスト言語 - キーワード**" 。 または、色分け可能な項目を種類 "**コメント (テスト言語)**" と "**キーワード (テスト言語)**" でグループ化することもできます。 言語名でグループ化することが望ましい。

> [!CAUTION]
> 既存の色付け可能なアイテム名との競合を避けるために、色付け可能な項目名に言語名を含めることを強くお勧めします。

> [!NOTE]
> 開発中にいずれかの色の名前を変更した場合は、最初に色にアクセスするときに Visual Studio が作成したキャッシュをリセットする必要があります。 これを行うには、Visual Studio SDK プログラム メニューから **[エクスペリメンタル ハイブのリセット**] コマンドを実行します。

 カラー化可能な項目のリストの最初の項目は参照できません。 Visual Studio では、その項目の既定のテキストの色と属性が常に提供されます。 これを処理する最も簡単な方法は、プレースホルダの色指定可能なアイテムを最初の項目として提供することです。

### <a name="high-color-colorable-items"></a>高色色のカラーが可能なアイテム
 また、カラー対応アイテムは、インターフェイスを介して 24 ビット<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>または高色の値をサポートすることもできます。 MPF<xref:Microsoft.VisualStudio.Package.ColorableItem>クラスはインターフェイス<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem>をサポートし、24 ビットカラーは通常の色と共にコンストラクタで指定されます。 詳細については、<xref:Microsoft.VisualStudio.Package.ColorableItem> クラスのトピックを参照してください。 次の例は、キーワードとコメントに 24 ビットカラーを設定する方法を示しています。 24 ビットカラーは、ユーザーのデスクトップで 24 ビットカラーがサポートされている場合に使用されます。それ以外の場合は、通常のテキストの色が使用されます。

 これらは、言語の既定の色であることを覚えておいてください。ユーザーは、これらの色を好きなように変更できます。

### <a name="example"></a>例
 この例では、クラスを使用してカスタムの色付け可能な項目の配列<xref:Microsoft.VisualStudio.Package.ColorableItem>を宣言し、設定する方法を示します。 次の使用例は、キーワードとコメントの色を 24 ビットカラーで設定します。

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

## <a name="the-colorizer-class-and-the-scanner"></a>カラー/カラーズクラスとスキャナ
 基本<xref:Microsoft.VisualStudio.Package.LanguageService>クラスには、クラス<xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A>をインスタンス化するメソッドがあります<xref:Microsoft.VisualStudio.Package.Colorizer>。 <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>メソッドから返されるスキャナーは、クラス コンストラクターに<xref:Microsoft.VisualStudio.Package.Colorizer>渡されます。

 このメソッドは、<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>独自のバージョンのクラスで実装<xref:Microsoft.VisualStudio.Package.LanguageService>する必要があります。 この<xref:Microsoft.VisualStudio.Package.Colorizer>クラスは、スキャナーを使用して、すべてのトークンの色情報を取得します。

 スキャナーは、検出されたすべてのトークン<xref:Microsoft.VisualStudio.Package.TokenInfo>の構造を設定する必要があります。 この構造体には、トークンが占有するスパン、使用するカラー インデックス、トークンの種類、トークン トリガーなどの情報が含まれています (<xref:Microsoft.VisualStudio.Package.TokenTriggers>を参照)。 <xref:Microsoft.VisualStudio.Package.Colorizer>クラスによる色付けには、スパンとカラーインデックスのみが必要です。

 <xref:Microsoft.VisualStudio.Package.TokenInfo>構造体に格納されている色インデックスは、通常、<xref:Microsoft.VisualStudio.Package.TokenColor>列挙体の値であり、キーワードや演算子などのさまざまな言語要素に対応する多数の名前付きインデックスを提供します。 カスタムの色付け可能な項目の一覧が列挙<xref:Microsoft.VisualStudio.Package.TokenColor>体に表示されている項目と一致する場合は、列挙体を各トークンの色として使用できます。 ただし、追加の色付け可能なアイテムがある場合、または既存の値をその順序で使用しない場合は、必要に応じてカスタムの色付け可能な項目のリストを配置し、適切なインデックスをそのリストに返すことができます。 インデックスを構造体に格納する場合は、<xref:Microsoft.VisualStudio.Package.TokenColor>必ずインデックスを<xref:Microsoft.VisualStudio.Package.TokenInfo>にキャストしてください。[!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)]はインデックスのみを参照します。

### <a name="example"></a>例
 次の例は、スキャナーが 3 種類のトークンの種類 (数字、句読点、識別子) を識別する方法を示しています。 この例は説明のみを目的としており、包括的なパーサーとスキャナーの実装を表すものではありません。 文字列を返すメソッドを`Lexer``GetNextToken()`持つクラスがあることを前提としています。

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
