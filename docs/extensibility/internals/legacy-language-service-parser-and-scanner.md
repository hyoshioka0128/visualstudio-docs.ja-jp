---
title: レガシ言語サービスパーサとスキャナ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c87f447a4b8bca804d27aae4967f4adaf389c627
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707311"
---
# <a name="legacy-language-service-parser-and-scanner"></a>従来の言語サービスのパーサーとスキャナー
パーサーは言語サービスの中心です。 管理パッケージ フレームワーク (MPF) 言語クラスでは、表示されているコードに関する情報を選択するための言語パーサーが必要です。 パーサーはテキストを字句トークンに分離し、型と機能によってそれらのトークンを識別します。

## <a name="discussion"></a>ディスカッション
 C# メソッドを次に示します。

```csharp
namespace MyNamespace
{
    class MyClass
    {
        public void MyFunction(int arg1)
        {
            int var1 = arg1;
        }
    }
}
```

 この例では、トークンは単語と句読点です。 トークンの種類は以下の通りです。

|トークン名|トークンの種類|
|----------------|----------------|
|名前空間、クラス、パブリック、ボイド、int|キーワード (keyword)|
|=|operator|
|{ } ( ) ;|delimiter|
|名前空間、マイクラス、マイファンクション、arg1、var1|identifier|
|名前空間|namespace|
|MyClass|class|
|マイファンクション|method|
|arg1|パラメーター (parameter)|
|var1|ローカル変数 (local variable)|

 パーサーの役割は、トークンを識別することです。 トークンによっては、複数の型を持つことができます。 パーサーがトークンを識別した後、言語サービスは、構文の強調表示、かっこの一致、IntelliSense 操作などの便利な機能を提供する情報を使用できます。

## <a name="types-of-parsers"></a>パーサーの種類
 言語サービス パーサーは、コンパイラの一部として使用されるパーサーとは同じではありません。 ただし、この種のパーサーは、コンパイラ パーサーと同じ方法で、スキャナーとパーサーの両方を使用する必要があります。

- スキャナーは、トークンの種類を識別するために使用されます。 この情報は、構文の強調表示に使用されたり、トークンの種類をすばやく特定して、かっこの照合のような他の操作を行うために使用されます。 このスキャナは<xref:Microsoft.VisualStudio.Package.IScanner>インターフェイスで表されます。

- パーサーは、トークンの関数とスコープを記述するために使用されます。 この情報は、メソッド、変数、パラメーター、宣言などの言語要素を識別し、コンテキストに基づいてメンバーとメソッド シグネチャのリストを提供するために IntelliSense 操作で使用されます。 このパーサーは、中かっこやかっこなど、一致する言語要素のペアを検索するためにも使用されます。 このパーサーは、クラス内<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>のメソッドを<xref:Microsoft.VisualStudio.Package.LanguageService>介してアクセスされます。

  言語サービスのスキャナーとパーサーの実装方法は、ユーザーが行います。 パーサーのしくみや独自のパーサーの作成方法を説明するリソースがいくつか用意されています。 また、いくつかの無料および市販の製品が利用でき、パーサーの作成に役立ちます。

### <a name="the-parsesource-parser"></a>パースソースパーサー
 コンパイラの一部として使用されるパーサー (トークンが何らかの形式の実行可能コードに変換される) とは異なり、言語サービスパーサーは、さまざまな理由と多くの異なるコンテキストで呼び出すことができます。 この方法をクラスの<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドに実装する<xref:Microsoft.VisualStudio.Package.LanguageService>方法は、ユーザーが行います。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドはバックグラウンド スレッドで呼び出される可能性があることを念頭に置いておく必要があります。

> [!CAUTION]
> 構造体<xref:Microsoft.VisualStudio.Package.ParseRequest>には、オブジェクトへの参照が<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>含まれています。 この<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>オブジェクトはバックグラウンド スレッドでは使用できません。 実際、基本 MPF クラスの多くはバックグラウンド スレッドでは使用できません。 これらには<xref:Microsoft.VisualStudio.Package.Source>、 <xref:Microsoft.VisualStudio.Package.ViewFilter>、<xref:Microsoft.VisualStudio.Package.CodeWindowManager>クラス、およびビューと直接または間接的に通信するその他のクラスが含まれます。

 このパーサーは通常、ソース ファイルが最初に呼び出されたとき、または解析理由値<xref:Microsoft.VisualStudio.Package.ParseReason>が指定されたときに、ソース ファイル全体を解析します。 メソッドへの後続の<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>呼び出しは、解析されたコードの一部を処理し、前の完全な解析操作の結果を使用して、はるかに迅速に実行できます。 メソッド<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>は、 オブジェクトを介して解析操作の結果<xref:Microsoft.VisualStudio.Package.AuthoringSink>を<xref:Microsoft.VisualStudio.Package.AuthoringScope>伝達します。 この<xref:Microsoft.VisualStudio.Package.AuthoringSink>オブジェクトは、特定の解析の理由 (パラメーター リストを持つ一致するかっこやメソッド シグネチャの範囲に関する情報など) の情報を収集するために使用されます。 には<xref:Microsoft.VisualStudio.Package.AuthoringScope>、宣言とメソッド シグネチャのコレクションが用意されており、さらに [定義**に移動**] メニューの [宣言] をクリックし、[**参照へ移動**] をクリックして高度な編集オプション**を**サポートすることもできます。

### <a name="the-iscanner-scanner"></a>Iスキャナスキャナー
 また、 を実装するスキャナーも実装<xref:Microsoft.VisualStudio.Package.IScanner>する必要があります。 ただし、このスキャナーは<xref:Microsoft.VisualStudio.Package.Colorizer>クラスを通じて行ごとに動作するため、通常は実装が簡単です。 各行の先頭に、MPF は、スキャナー<xref:Microsoft.VisualStudio.Package.Colorizer>に渡される状態変数として使用する値をクラスに与えます。 各行の終わりに、スキャナは更新された状態変数を返します。 MPF は、ソース ファイルの先頭から開始しなくても、スキャナーが任意の行から解析を開始できるように、各行のこの状態情報をキャッシュします。 この高速スキャンは、1 行で、エディターは、ユーザーに高速なフィードバックを提供することができます。

## <a name="parsing-for-matching-braces"></a>一致する中かっこの解析
 この例では、ユーザーが入力した右中かっこを照合するための制御フローを示します。 このプロセスでは、色付けに使用されるスキャナーを使用して、トークンの種類と、トークンがマッチブレース操作をトリガーできるかどうかを判断します。 トリガーが見つかった場合は、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドが呼び出され、一致する中かっこが検索されます。 最後に、2 つの中かっこが強調表示されます。

 中かっこは、トリガーの名前と解析の理由で使用されていますが、このプロセスは実際の中かっこに限定されません。 一致するペアとして指定された文字のペアはサポートされます。 例としては、 \< ( と ) と >、および [ と ] が含まれます。

 言語サービスが一致する中かっこをサポートしていると仮定します。

1. ユーザーは、右中かっこ (}) を入力します。

2. 中かっこはソース ファイルのカーソルに挿入され、カーソルは 1 つずつ進みます。

3. クラス<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>内の<xref:Microsoft.VisualStudio.Package.Source>メソッドは、型付きの右中かっこで呼び出されます。

4. メソッド<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>は、現在<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>のカーソル位置<xref:Microsoft.VisualStudio.Package.Source>の直前の位置にあるトークンを取得するクラス内のメソッドを呼び出します。 このトークンは、型指定された右中かっこに対応します)。

    1. メソッド<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>は、オブジェクト<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>のメソッドを<xref:Microsoft.VisualStudio.Package.Colorizer>呼び出して、現在の行のすべてのトークンを取得します。

    2. メソッド<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>は、現在<xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A>の行の<xref:Microsoft.VisualStudio.Package.IScanner>テキストを使用してオブジェクトのメソッドを呼び出します。

    3. この<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>メソッドは、オブジェクトの<xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A>メソッドを繰<xref:Microsoft.VisualStudio.Package.IScanner>り返し呼び出して、現在の行からすべてのトークンを収集します。

    4. メソッド<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>は、クラス内のプライベート<xref:Microsoft.VisualStudio.Package.Source>メソッドを呼び出して、目的の位置を含むトークンを取得し、メソッドから取得した<xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A>トークンの一覧を渡します。

5. メソッド<xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>は、メソッドから返されるトークン<xref:Microsoft.VisualStudio.Package.TokenTriggers>のトークン トリガー フラグを<xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A>検索します。つまり、右中かっこを表すトークン)。

6. トリガーフラグ<xref:Microsoft.VisualStudio.Package.TokenTriggers>が見つかった場合は、クラス<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>内のメソッド<xref:Microsoft.VisualStudio.Package.Source>が呼び出されます。

7. この<xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A>メソッドは、解析理由の値を使用して解析<xref:Microsoft.VisualStudio.Package.ParseReason>操作を開始します。 この操作は、最終的に<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>クラスのメソッド<xref:Microsoft.VisualStudio.Package.LanguageService>を呼び出します。 非同期解析が有効になっている場合、メソッドの<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>この呼び出しはバックグラウンド スレッドで発生します。

8. 解析操作が終了すると、`HandleMatchBracesResponse`<xref:Microsoft.VisualStudio.Package.Source>クラス内で内部完了ハンドラー (コールバック メソッドとも呼ばれます) が呼び出されます。 この呼び出しは、<xref:Microsoft.VisualStudio.Package.LanguageService>パーサーではなく、基本クラスによって自動的に行われます。

9. この`HandleMatchBracesResponse`メソッドは、オブジェクトに格納されているオブジェクトから範囲<xref:Microsoft.VisualStudio.Package.AuthoringSink>のリストを<xref:Microsoft.VisualStudio.Package.ParseRequest>取得します。 (スパンは、<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>ソース ファイル内の行と文字の範囲を指定する構造体です。この範囲のリストには、通常、開始中かっこと右中かっこにそれぞれ 1 つずつ、2 つの範囲が含まれています。

10. メソッド`HandleBracesResponse`は、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A><xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>オブジェクトに格納されているオブジェクトのメソッドを<xref:Microsoft.VisualStudio.Package.ParseRequest>呼び出します。 これは、指定された範囲を強調表示します。

11. プロパティ<xref:Microsoft.VisualStudio.Package.LanguagePreferences><xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>が有効な場合、`HandleBracesResponse`メソッドは、一致する範囲に囲まれているテキストを取得し、その範囲の最初の 80 文字をステータス バーに表示します。 この方法に、一<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>致するペアに付随する言語要素が含まれている場合に最適です。 詳細については、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> プロパティを参照してください。

12. 完了しました。

### <a name="summary"></a>まとめ
 一致する中かっこ操作は、通常、言語要素の単純なペアに制限されます。 `if(...)`三重 (""""" と`{`""`}``else``{``}`"、""""、""""、"") の照合など、より複雑な要素は、単語補完操作の一部として強調表示できます。 たとえば、"else" という単語が終了すると、一致する`if`" " ステートメントを強調表示できます。 一連の`if`/`else if`ステートメントがある場合は、一致する中かっこと同じメカニズムを使用して、すべてのステートメントを強調表示できます。 基本<xref:Microsoft.VisualStudio.Package.Source>クラスは、次のように、既にこれをサポートしています: スキャナーは、カーソル位置の<xref:Microsoft.VisualStudio.Package.TokenTriggers>前にあるトークンのトリガー値<xref:Microsoft.VisualStudio.Package.TokenTriggers>と組み合わせたトークン トリガー値を返す必要があります。

 詳細については、「[レガシ言語サービスでのブレースの照合](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)」を参照してください。

## <a name="parsing-for-colorization"></a>色付けの解析
 ソース コードの色付けは簡単で、トークンの種類を識別し、その型に関する色情報を返すだけです。 この<xref:Microsoft.VisualStudio.Package.Colorizer>クラスは、エディターとスキャナーの間の仲介役として機能し、すべてのトークンに関するカラー情報を提供します。 この<xref:Microsoft.VisualStudio.Package.Colorizer>クラスは、<xref:Microsoft.VisualStudio.Package.IScanner>オブジェクトを使用して行の色付けに役立ち、ソース ファイル内のすべての行の状態情報を収集します。 MPF 言語サービス クラスでは、<xref:Microsoft.VisualStudio.Package.Colorizer>インターフェイスを介してのみスキャナーと通信するため、クラスをオーバーライドする<xref:Microsoft.VisualStudio.Package.IScanner>必要はありません。 インターフェイスを実装するオブジェクトを指定するには<xref:Microsoft.VisualStudio.Package.IScanner>、クラスの<xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A>メソッドをオーバーライドします<xref:Microsoft.VisualStudio.Package.LanguageService>。

 スキャナー<xref:Microsoft.VisualStudio.Package.IScanner>には、メソッドを介してソース コードの<xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A>行が与えられます。 <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A>このメソッドの呼び出しは、行のトークンが使い果たされるまで、行の次のトークンを取得するために繰り返されます。 色付けの場合、MPF はすべてのソース コードを一連の行として扱います。 したがって、スキャナーは、ソースがラインとして来てに対処できる必要があります。 さらに、任意のラインはいつでもスキャナーに渡すことができます、そして唯一の保証は、スキャナがスキャンされるラインの前にラインから状態変数を受け取ることです。

 この<xref:Microsoft.VisualStudio.Package.Colorizer>クラスは、トークン トリガーを識別するためにも使用されます。 これらのトリガーは、特定のトークンが単語補完や一致中かっこなどのより複雑な操作を開始できることを MPF に伝えます。 このようなトリガを識別するには、高速で任意の場所で発生する必要があるため、スキャナーはこのタスクに最適です。

 詳細については、「[従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)」を参照してください。

## <a name="parsing-for-functionality-and-scope"></a>機能とスコープの解析
 機能とスコープの解析には、単に検出されるトークンの種類を特定するだけの作業よりも多くの労力が必要です。 パーサーは、トークンの種類だけでなく、トークンが使用される機能も識別する必要があります。 たとえば、識別子は単なる名前ですが、言語では、コンテキストに応じて、クラス、名前空間、メソッド、または変数の名前を識別子に指定できます。 トークンの一般的な型は識別子である場合がありますが、識別子は識別子の内容と定義場所に応じて他の意味を持つ場合もあります。 この識別では、パーサーが解析される言語についてより広範な知識を持っている必要があります。 ここがクラスの<xref:Microsoft.VisualStudio.Package.AuthoringSink>出番です。 この<xref:Microsoft.VisualStudio.Package.AuthoringSink>クラスは、識別子、メソッド、対応する言語ペア (中かっこやかっこなど)、言語トリプル (言語ペアに似ていますが、" "`foreach()`" "`{`" と " "`}`という部分など ) に関する情報を収集します。 さらに、デバッガーを読み込<xref:Microsoft.VisualStudio.Package.AuthoringSink>む必要がないように、ブレークポイントの初期検証で使用されるコード識別をサポートするクラスをオーバーライドし、プログラムがデバッグ中に自動的にローカル変数とパラメーターを表示し、デバッガーが提示する適切なローカル変数とパラメーターを特定するパーサーを必要とする**自動**デバッグ ウィンドウを使用できます。

 オブジェクト<xref:Microsoft.VisualStudio.Package.AuthoringSink>はオブジェクトの一部としてパーサーに<xref:Microsoft.VisualStudio.Package.ParseRequest>渡され、新しいオブジェクトが<xref:Microsoft.VisualStudio.Package.AuthoringSink>作成されるたびに新<xref:Microsoft.VisualStudio.Package.ParseRequest>しいオブジェクトが作成されます。 さらに、このメソッド<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>は、さまざまな<xref:Microsoft.VisualStudio.Package.AuthoringScope>IntelliSense 操作を処理するために使用されるオブジェクトを返す必要があります。 オブジェクト<xref:Microsoft.VisualStudio.Package.AuthoringScope>は、構文解析の理由に応じて、宣言のリストとメソッドのリストを保持します。 クラス<xref:Microsoft.VisualStudio.Package.AuthoringScope>を実装する必要があります。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)
- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
