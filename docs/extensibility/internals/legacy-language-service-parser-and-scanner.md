---
title: 従来の言語サービスパーサーとスキャナー |Microsoft Docs
description: 表示されているコードに関する情報を選択する従来の言語サービスパーサーとスキャナーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c4c9ee6cfec35804d7e60675342f3961dfb90c6c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99839561"
---
# <a name="legacy-language-service-parser-and-scanner"></a>従来の言語サービスのパーサーとスキャナー
パーサーは言語サービスの中核です。 Managed Package Framework (MPF) 言語クラスでは、表示されているコードに関する情報を選択する言語パーサーが必要です。 パーサーはテキストを字句トークンに分割し、型と機能によってそれらのトークンを識別します。

## <a name="discussion"></a>ディスカッション
 C# のメソッドを次に示します。

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

 この例では、トークンは単語と句読点です。 トークンの種類は次のとおりです。

|Token Name (トークン名)|トークンの種類|
|----------------|----------------|
|namespace、class、public、void、int|キーワード (keyword)|
|=|operator|
|{ } ( ) ;|delimiter|
|MyNamespace、MyClass、MyFunction、arg1、var1|identifier|
|MyNamespace|namespace|
|MyClass|class|
|MyFunction|method|
|arg1|parameter|
|var1|ローカル変数 (local variable)|

 パーサーの役割は、トークンを識別することです。 トークンによっては、複数の型を持つことができます。 パーサーによってトークンが識別された後、言語サービスでは、構文の強調表示、かっこの一致、IntelliSense 操作などの有用な機能を提供するために情報を使用できます。

## <a name="types-of-parsers"></a>パーサーの種類
 言語サービスパーサーは、コンパイラの一部として使用されるパーサーと同じではありません。 ただし、この種のパーサーでは、コンパイラパーサーと同じ方法でスキャナーとパーサーの両方を使用する必要があります。

- スキャナーは、トークンの種類を識別するために使用されます。 この情報は、構文の強調表示に使用されたり、トークンの種類をすばやく特定して、かっこの照合のような他の操作を行うために使用されます。 このスキャナーは、インターフェイスによって表され <xref:Microsoft.VisualStudio.Package.IScanner> ます。

- パーサーは、トークンの機能とスコープを記述するために使用されます。 この情報は、メソッド、変数、パラメーター、宣言などの言語要素を識別したり、コンテキストに基づいてメンバーとメソッドシグネチャのリストを提供したりするために、IntelliSense 操作で使用されます。 このパーサーは、中かっこやかっこなど、一致する言語要素のペアを検索するためにも使用されます。 このパーサーには、クラスのメソッドを使用してアクセスし <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> ます。

  言語サービスに対してスキャナーとパーサーを実装する方法は、お客様によって設定されます。 パーサーの動作と独自のパーサーの記述方法を説明するいくつかのリソースが用意されています。 また、パーサーの作成に役立つ、いくつかの無料および商用の製品が用意されています。

### <a name="the-parsesource-parser"></a>ParseSource パーサー
 コンパイラの一部として使用されるパーサー (トークンがなんらかの形式の実行可能コードに変換される) とは異なり、言語サービスパーサーはさまざまな理由やさまざまなコンテキストで呼び出すことができます。 クラスのメソッドにこの方法を実装する方法 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> は、ユーザーによって設定されます。 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッドがバックグラウンドスレッドで呼び出される可能性があることに注意してください。

> [!CAUTION]
> 構造体には、 <xref:Microsoft.VisualStudio.Package.ParseRequest> オブジェクトへの参照が含まれてい <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。 この <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> オブジェクトをバックグラウンドスレッドで使用することはできません。 実際、基本 MPF クラスの多くをバックグラウンドスレッドで使用することはできません。 これには <xref:Microsoft.VisualStudio.Package.Source> 、、、の各クラス、 <xref:Microsoft.VisualStudio.Package.ViewFilter> <xref:Microsoft.VisualStudio.Package.CodeWindowManager> およびビューと直接または間接的に通信するその他のクラスが含まれます。

 このパーサーは、通常、最初に呼び出されたとき、またはの解析理由値が指定されたときに、ソースファイル全体を解析し <xref:Microsoft.VisualStudio.Package.ParseReason> ます。 メソッドへの後続の呼び出しで <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> は、解析されたコードの一部を処理します。前の完全解析操作の結果を使用することにより、より短時間で実行できます。 メソッドは、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> オブジェクトとオブジェクトを使用して解析操作の結果を通信し <xref:Microsoft.VisualStudio.Package.AuthoringSink> <xref:Microsoft.VisualStudio.Package.AuthoringScope> ます。 オブジェクトは、特定の解析の理由に関する <xref:Microsoft.VisualStudio.Package.AuthoringSink> 情報を収集するために使用されます。たとえば、パラメーターリストを持つ一致する中かっこまたはメソッドのシグネチャの範囲に関する情報などです。 には、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 宣言とメソッドシグネチャのコレクションが用意されています。また、[高度な編集に進む] オプション ([**定義へ**]、[ **宣言へ**]、[ **参照へジャンプ**]) もサポートされています。

### <a name="the-iscanner-scanner"></a>IScanner スキャナー
 を実装するスキャナーも実装する必要があり <xref:Microsoft.VisualStudio.Package.IScanner> ます。 ただし、このスキャナーはクラスによって1行ずつ実行されるため、 <xref:Microsoft.VisualStudio.Package.Colorizer> 通常は実装が簡単です。 各行の先頭で、MPF は、 <xref:Microsoft.VisualStudio.Package.Colorizer> スキャナーに渡される状態変数として使用する値をクラスに提供します。 各行の最後で、更新された状態変数がスキャナーから返されます。 MPF は各行のこの状態情報をキャッシュするため、スキャナーは、ソースファイルの先頭から開始することなく、任意の行から解析を開始できます。 この1行の高速スキャンにより、エディターはユーザーに迅速なフィードバックを提供できます。

## <a name="parsing-for-matching-braces"></a>一致する中かっこの解析
 この例は、ユーザーが入力した右中かっこと照合するための制御フローを示しています。 このプロセスでは、色付けに使用されるスキャナーを使用して、トークンの種類と、トークンが対応する中かっこの操作をトリガーできるかどうかを判断します。 トリガーが見つかった場合は、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> メソッドが呼び出され、対応する中かっこが検索されます。 最後に、2つの中かっこが強調表示されます。

 トリガーの名前と解析の理由で中かっこが使用されている場合でも、このプロセスは実際の中かっこに限定されません。 一致するペアとして指定されている文字のペアはすべてサポートされています。 例として、(and)、 \< and > 、および [and] があります。

 言語サービスでは、対応する中かっこがサポートされているものとします。

1. ユーザーは、右中かっこ (}) を入力します。

2. 中かっこは、ソースファイルのカーソル位置に挿入され、カーソルは1つ進められます。

3. <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A>クラスのメソッド <xref:Microsoft.VisualStudio.Package.Source> は、型指定された右中かっこで呼び出されます。

4. メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> クラスのメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> 現在の <xref:Microsoft.VisualStudio.Package.Source> カーソル位置の直前の位置にあるトークンを取得します。 このトークンは、型指定された右中かっこに対応します)。

    1. メソッドは、オブジェクトのメソッドを呼び出して、 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> 現在の <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> 行の <xref:Microsoft.VisualStudio.Package.Colorizer> すべてのトークンを取得します。

    2. メソッドは、 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> 現在の <xref:Microsoft.VisualStudio.Package.IScanner> 行のテキストを使用して、オブジェクトのメソッドを呼び出します。

    3. メソッドは、 <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> オブジェクトのメソッドを繰り返し呼び出して、現在の <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> <xref:Microsoft.VisualStudio.Package.IScanner> 行からすべてのトークンを収集します。

    4. メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> クラスのプライベートメソッドを呼び出し <xref:Microsoft.VisualStudio.Package.Source> て、目的の位置を含むトークンを取得し、メソッドから取得したトークンのリストを渡し <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> ます。

5. メソッドは、 <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> <xref:Microsoft.VisualStudio.Package.TokenTriggers> メソッドから返されたトークン、 <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> つまり、右中かっこを表すトークンのトークントリガーフラグを検索します。

6. のトリガーフラグが見つかった場合 <xref:Microsoft.VisualStudio.Package.TokenTriggers> は、 <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> クラスのメソッド <xref:Microsoft.VisualStudio.Package.Source> が呼び出されます。

7. メソッドは、解析 <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> の理由値をとして解析操作を開始し <xref:Microsoft.VisualStudio.Package.ParseReason> ます。 この操作 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> では、最終的にクラスのメソッドを呼び出し <xref:Microsoft.VisualStudio.Package.LanguageService> ます。 非同期解析が有効になっている場合、メソッドへのこの呼び出しは <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> バックグラウンドスレッドで発生します。

8. 解析操作が完了すると、という内部完了ハンドラー (コールバックメソッドとも呼ばれ `HandleMatchBracesResponse` ます) がクラスで呼び出され <xref:Microsoft.VisualStudio.Package.Source> ます。 この呼び出しは、 <xref:Microsoft.VisualStudio.Package.LanguageService> パーサーによってではなく、基本クラスによって自動的に行われます。

9. メソッドは、 `HandleMatchBracesResponse` <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトに格納されているオブジェクトから範囲のリストを取得し <xref:Microsoft.VisualStudio.Package.ParseRequest> ます。 (スパンは、 <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> ソースファイル内の行と文字の範囲を指定する構造体です)。この範囲の一覧には、通常、左中かっこと終わりかっこの2つの範囲が含まれています。

10. メソッドは、 `HandleBracesResponse` <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> オブジェクトに格納されているオブジェクトに対してメソッドを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Package.ParseRequest> ます。 これにより、指定された範囲が強調表示されます。

11. <xref:Microsoft.VisualStudio.Package.LanguagePreferences>プロパティが有効になっている場合 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> 、メソッドは、 `HandleBracesResponse` 一致するスパンに含まれるテキストを取得し、そのスパンの最初の80文字をステータスバーに表示します。 これは、メソッドに、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 一致するペアに付随する言語要素が含まれている場合に最適です。 詳細については、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> プロパティを参照してください。

12. 完了しました。

### <a name="summary"></a>まとめ
 通常、対応する中かっこの演算は、単純な言語要素のペアに限定されます。 3要素の一致 (""、""、""、""、"" など) など、より複雑な要素を、 `if(...)` `{` `}` `else` `{` `}` 単語入力補完操作の一部として強調表示することができます。 たとえば、"else" という単語が終了した場合、対応する " `if` " ステートメントを強調表示できます。 一連のステートメントがある場合は `if` / `else if` 、対応するかっこと同じメカニズムを使用してすべてのステートメントを強調表示できます。 <xref:Microsoft.VisualStudio.Package.Source>基本クラスでは、次のように、この機能が既にサポートされています。スキャナーは、トークントリガーの値と、 <xref:Microsoft.VisualStudio.Package.TokenTriggers> <xref:Microsoft.VisualStudio.Package.TokenTriggers> カーソル位置の前にあるトークンのトリガー値を返す必要があります。

 詳細については、「 [従来の言語サービスでの中かっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)」を参照してください。

## <a name="parsing-for-colorization"></a>色付けの解析
 色分けソースコードは簡単です。トークンの種類を特定し、その型に関する色情報を返すだけです。 クラスは、 <xref:Microsoft.VisualStudio.Package.Colorizer> エディターとスキャナー間の仲介役として機能し、すべてのトークンに関する色情報を提供します。 クラスは、オブジェクトを使用して、 <xref:Microsoft.VisualStudio.Package.Colorizer> <xref:Microsoft.VisualStudio.Package.IScanner> 行を色分けしたり、ソースファイル内のすべての行の状態情報を収集したりします。 MPF 言語サービスクラスでは、 <xref:Microsoft.VisualStudio.Package.Colorizer> インターフェイスを介してのみスキャナーと通信するため、クラスをオーバーライドする必要はありません <xref:Microsoft.VisualStudio.Package.IScanner> 。 <xref:Microsoft.VisualStudio.Package.IScanner>クラスのメソッドをオーバーライドすることによって、インターフェイスを実装するオブジェクトを指定し <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> <xref:Microsoft.VisualStudio.Package.LanguageService> ます。

 <xref:Microsoft.VisualStudio.Package.IScanner>スキャナーには、メソッドを使用してソースコードの行が指定されてい <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> ます。 メソッドの呼び出し <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> は、行がトークンを使い果たすまで行の次のトークンを取得するために繰り返されます。 色付けの場合、MPF はすべてのソースコードを行のシーケンスとして扱います。 そのため、スキャナーは、ソースを行として扱うことができる必要があります。 また、任意の行をいつでもスキャナーに渡すことができ、保証されるのは、スキャナーがスキャン対象の行の前の状態変数を受け取ることだけです。

 クラスは、 <xref:Microsoft.VisualStudio.Package.Colorizer> トークントリガーを識別するためにも使用されます。 これらのトリガーは、特定のトークンが単語の補完や対応する中かっこなどのより複雑な操作を開始できることを MPF に伝えます。 このようなトリガーは高速である必要があり、任意の場所に配置する必要があるため、スキャナーはこのタスクに最適です。

 詳細については、「 [従来の言語サービスの構文色分け](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)」を参照してください。

## <a name="parsing-for-functionality-and-scope"></a>機能とスコープの解析
 機能とスコープの解析には、発生したトークンの種類を特定するだけではなく、より多くの労力が必要になります。 パーサーは、トークンの種類だけでなく、トークンを使用する機能も識別する必要があります。 たとえば、識別子は単なる名前ですが、お使いの言語では、コンテキストに応じて、クラス、名前空間、メソッド、または変数の名前を識別子として使用できます。 トークンの一般的な型は識別子である場合がありますが、識別子の内容や定義されている場所によっては、識別子に他の意味がある場合もあります。 この id を設定するには、解析対象の言語についての豊富な知識をパーサーに追加する必要があります。 ここ <xref:Microsoft.VisualStudio.Package.AuthoringSink> で、クラスが登場します。 クラスは、 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 識別子、メソッド、一致する言語のペア (中かっこやかっこなど)、言語の3要素 ("" "、" "など、3つの部分がある点を除いて、言語のペアに似ています) に関する情報を収集し `foreach()` `{` `}` ます。 さらに、クラスをオーバーライドして <xref:Microsoft.VisualStudio.Package.AuthoringSink> コード id をサポートすることもできます。これは、デバッガーを読み込む必要がないように、ブレークポイントを事前に検証するために使用されます。 **また、** プログラムがデバッグされているときに、パーサーがデバッガーによって表示されるローカル変数とパラメーターを識別する必要があります。

 オブジェクトは <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトの一部としてパーサーに渡され、新しいオブジェクトが作成されるたびに <xref:Microsoft.VisualStudio.Package.ParseRequest> 新しい <xref:Microsoft.VisualStudio.Package.AuthoringSink> オブジェクトが作成され <xref:Microsoft.VisualStudio.Package.ParseRequest> ます。 また、メソッドは、 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> <xref:Microsoft.VisualStudio.Package.AuthoringScope> さまざまな IntelliSense 操作を処理するために使用されるオブジェクトを返す必要があります。 オブジェクトは、 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 解析の理由に応じて、宣言のリストとメソッドのリストを保持します。これらのメソッドのいずれかに設定されます。 <xref:Microsoft.VisualStudio.Package.AuthoringScope>クラスを実装する必要があります。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)
- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
