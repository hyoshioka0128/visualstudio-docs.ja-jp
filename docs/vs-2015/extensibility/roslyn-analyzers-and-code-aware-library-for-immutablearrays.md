---
title: ImmutableArrays | の roslyn アナライザーとコード対応ライブラリMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65849a3d9ad1cdd073551f96e61997fe5f91118a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "81444896"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>Roslyn アナライザーと ImmutableArrays 用コード認識ライブラリ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[.NET Compiler Platform](https://github.com/dotnet/roslyn) ("Roslyn") を使用すると、コード対応のライブラリをビルドできます。 コード対応ライブラリは、ツール (Roslyn アナライザー) を使用して、最適な方法でライブラリを使用したり、エラーを回避したりするための機能を提供します。 このトピックでは、 [NIB: 変更](https://msdn.microsoft.com/library/33f4449d-7078-450a-8d60-d9229f66bbca) できないコレクション NuGet パッケージを使用するときに、一般的なエラーをキャッチするために、実際の Roslyn アナライザーを構築する方法について説明します。 また、この例では、アナライザーによって検出されたコードの問題に対してコード修正を行う方法も示しています。 ユーザーは、Visual Studio 電球 UI にコード修正プログラムを表示し、コードの修正を自動的に適用できます。

## <a name="getting-started"></a>作業の開始
この例をビルドするには、次のものが必要です。

- Visual Studio 2015 (Express Edition ではない) 以降のバージョン。 無料の[Visual Studio Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs)を使用できます。

- [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)。 また、Visual Studio をインストールするときに、[共通ツール] の Visual Studio Extensibility Tools をオンにして SDK を同時にインストールすることもできます。 Visual Studio を既にインストールしている場合は、メインメニュー **ファイル &#124; 新しい &#124;プロジェクト...**] に移動して、左側のナビゲーションウィンドウで [C#] を選択し、[機能拡張] を選択して、この SDK をインストールすることもできます。 [**Visual Studio Extensibility Tools のインストール**] 階層リンクプロジェクトテンプレートを選択すると、SDK をダウンロードしてインストールするように求められます。

- [.NET Compiler Platform ("Roslyn") SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK)。 この SDK をインストールするには、メインメニュー **ファイル &#124; 新しい &#124; プロジェクト...**] に移動し、左側のナビゲーションウィンドウで [ **C#** ] を選択し、[ **機能拡張**] を選択します。 [**.NET COMPILER PLATFORM sdk のダウンロード**] 階層リンクプロジェクトテンプレートを選択すると、sdk をダウンロードしてインストールするように求められます。 この SDK には、 [Roslyn Syntax Visualizer](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer)が含まれています。 この非常に便利なツールは、アナライザーで検索する必要があるコードモデルの種類を確認するのに役立ちます。 Analyzer インフラストラクチャは、特定のコードモデル型に対してコードを呼び出すので、コードは必要なときにのみ実行され、関連するコードの分析にのみ集中できます。

## <a name="whats-the-problem"></a>何がそんなに問題ですか。
たとえば、ImmutableArray をサポートするライブラリを用意していると <xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName> します。 C# の開発者には、.NET 配列に関する多くの経験があります。 ただし、実装で使用される ImmutableArrays および最適化手法の性質上、次に説明するように、C# 開発者はライブラリのユーザーが破損したコードを記述することになります。 さらに、ユーザーは実行時までエラーを表示しません。これは、Visual Studio と .NET で使用される品質エクスペリエンスではありません。

ユーザーは、次のようなコードを記述することに慣れています。

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);

```

空の配列を作成して後続のコード行に入力し、コレクション初期化子構文を使用することは、C# 開発者にとって非常になじみがあります。 ただし、実行時に ImmutableArray クラッシュに対して同じコードを記述すると、次のようになります。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);

```

最初のエラーは、ImmutableArray 実装が構造体を使用して基になるデータストレージをラップしているためです。 構造体に `default(T)` は、0または null のメンバーを含む構造体を返すことができるように、パラメーターなしのコンストラクターが必要です。 コードがアクセスするときに `b1.Length` 、ImmutableArray 構造体に基になるストレージ配列がないため、実行時の null 参照解除エラーが発生します。 空の ImmutableArray を作成する正しい方法は `ImmutableArray<int>.Empty` です。

 コレクション初期化子のエラーは、呼び出しのたびに ImmutableArray メソッドが新しいインスタンスを返すために発生します。 ImmutableArrays は変化しないため、新しい要素を追加すると、新しい ImmutableArray オブジェクトが返されます (これは、以前に既存の ImmutableArray を使用してパフォーマンス上の理由からストレージを共有する可能性があります)。 `b2`は、5回呼び出す前に最初の ImmutableArray をポイントするため `Add()` 、 `b2` は既定の ImmutableArray です。 また、この呼び出しの長さは、null 参照解除エラーによってもクラッシュします。 Add を手動で呼び出すことなく ImmutableArray を初期化する正しい方法は、を使用することです `ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})` 。

## <a name="finding-relevant-syntax-node-types-to-trigger-your-analyzer"></a>アナライザーをトリガーするための関連する構文ノードの種類の検索
アナライザーのビルドを開始するには、まず、検索する必要がある SyntaxNode の種類を確認します。   メニュー **ビュー &#124; 他の Windows &#124; Roslyn Syntax Visualizer**から Syntax Visualizer を起動します。

を宣言する行にエディターのキャレットを配置し `b1` ます。 構文ツリーのノードに表示されている Syntax Visualizer が表示され `LocalDeclarationStatement` ます。 このノードには、があります。このノードにはがあり、最終的にはがあり `VariableDeclaration` `VariableDeclarator` `EqualsValueClause` `ObjectCreationExpression` ます。 ノードの Syntax Visualizer ツリーをクリックすると、エディターウィンドウの構文が強調表示され、そのノードで表されるコードが表示されます。 SyntaxNode サブ型の名前は、C# 文法で使用されている名前と一致します。

## <a name="creating-the-analyzer-project"></a>Analyzer プロジェクトの作成
メインメニューから、[ **ファイル &#124; 新規 &#124; プロジェクト**] を選択します。 [ **新しいプロジェクト** ] ダイアログの左側のナビゲーションバーで、[ **C#** プロジェクト] の下にある [機能拡張] を選択し、右側のウィンドウで [コード修正プロジェクトテンプレート **を含むアナライザー** ] を選択します。 名前を入力し、ダイアログを確認します。

このテンプレートは、DiagnosticAnalyzer.cs ファイルを開きます。 [エディターバッファー] タブを選択します。このファイルには、( `DiagnosticAnalyzer` Roslyn API 型) から派生したアナライザークラス (プロジェクトに指定した名前の形式) が含まれています。 新しいクラスでは、アナライザー `DiagnosticAnalyzerAttribute` が C# 言語に関連していることを宣言することで、コンパイラがアナライザーを検出して読み込むようにします。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

C# コードを対象とする Visual Basic を使用してアナライザーを実装できます。また、その逆も可能です。 DiagnosticAnalyzerAttribute では、アナライザーが1つの言語を対象とするか、またはその両方を対象とするかを選択することが重要です。 言語の詳細なモデリングを必要とする洗練されたアナライザーは、1つの言語のみを対象にすることができます。 たとえば、アナライザーが型名またはパブリックメンバー名のみをチェックする場合は、Visual Basic と C# 全体で共通言語モデルの Roslyn プランを使用することができます。 たとえば、FxCop は、クラスがを実装していることを警告し <xref:System.Runtime.Serialization.ISerializable> ますが、クラスには言語に依存せず、 <xref:System.SerializableAttribute> Visual Basic と C# の両方のコードに対して機能します。

## <a name="initalizing-the-analyzer"></a>アナライザーの初期化
クラスの少し下にスクロールし `DiagnosticAnalyzer` て、メソッドを表示し `Initialize` ます。 コンパイラは、アナライザーをアクティブ化するときにこのメソッドを呼び出します。 メソッドは、 `AnalysisContext` アナライザーがコンテキスト情報を取得し、分析するコードの種類のイベントのコールバックを登録できるようにするオブジェクトを受け取ります。

```csharp
public override void Initialize(AnalysisContext context) {}
```

このメソッドで新しい行を開き、「context」と入力します。 Intellisense の入力候補一覧を表示します。 入力候補一覧には、 `Register…` さまざまな種類のイベントを処理するためのメソッドが多数あります。 たとえば、1つ目のは、 `RegisterCodeBlockAction` ブロックのコードにコールバックします。これは通常、中かっこの間のコードです。 ブロックに登録すると、フィールドの初期化子、属性に与えられた値、または省略可能なパラメーターの値をコードにコールバックすることもできます。

もう1つの例として、は `RegisterCompilationStartAction` コンパイルの開始時にコードにコールバックします。これは、さまざまな場所で状態を収集する必要がある場合に便利です。 データ構造を作成して、使用するすべてのシンボルを収集することができます。また、アナライザーが構文やシンボルに対してコールバックされるたびに、データ構造内の各場所に関する情報を保存することができます。 コンパイルの終了によってコールバックが呼び出されたときに、保存したすべての場所を分析して、コードが各ステートメントから使用するシンボルを報告でき `using` ます。

**Syntax Visualizer**を使用して、コンパイラが Objectfrom 式を処理するときに呼び出すことを学習しました。 このコードを使用して、コールバックを設定します。

```csharp

context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

構文ノードに登録し、オブジェクト作成構文ノードのみをフィルター処理します。 慣例により、アナライザーの作成者はアクションを登録するときにラムダを使用します。これにより、アナライザーをステートレスに保つことができます。 Visual Studio の [ **使用法から生成]** 機能を使用して、メソッドを作成でき `AnalyzeObjectCreation` ます。 これにより、正しい種類のコンテキストパラメーターも生成されます。

## <a name="setting-properties-for-users-of-your-analyzer"></a>アナライザーのユーザーのプロパティの設定
アナライザーが Visual Studio UI に適切に表示されるように、次のコード行を探して変更し、アナライザーを識別します。

```csharp
internal const string Category = "Naming";
```

`"Naming"` を `"API Guidance"` に変更します。

次に、 **ソリューションエクスプローラー**を使用して、プロジェクト内のリソース .resx ファイルを見つけて開きます。 アナライザー、タイトルなどの説明を入力できます。ここでは、これらのすべての値をに変更でき `“Don’t use ImmutableArray<T> constructor”` ます。 文字列形式の引数を文字列に含めることができます (やなど {0} {1} )。後でを呼び出すときに `Diagnostic.Create()` 、渡す引数の params 配列を渡すことができます。

## <a name="analyzing-an-object-creation-expression"></a>オブジェクト作成式の分析
メソッドは、 `AnalyzeObjectCreation` コードアナライザーフレームワークによって提供されるさまざまな種類のコンテキストを受け取ります。 Initialize メソッド `AnalysisContext` を使用すると、アクションコールバックを登録してアナライザーを設定できます。 たとえば、には、を `SyntaxNodeAnalysisContext` `CancellationToken` 渡すことができるがあります。 ユーザーがエディターで入力を開始すると、Roslyn はアナライザーの実行をキャンセルして作業を保存し、パフォーマンスを向上させます。 もう1つの例として、このコンテキストには、オブジェクト作成構文ノードを返す Node プロパティがあります。

ノードを取得します。これは、構文ノードアクションをフィルター処理した型であると想定できます。

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launching-visual-studio-with-your-analyzer-the-first-time"></a>初めてアナライザーを使用して Visual Studio を起動する
アナライザーをビルドして実行して Visual Studio を起動します ( **F5**キーを押します)。 **ソリューションエクスプローラー**のスタートアッププロジェクトは vsix プロジェクトであるため、コードを実行すると、コードと vsix がビルドされ、その vsix がインストールされた状態で Visual Studio が起動します。 この方法で Visual Studio を起動すると、別のレジストリハイブで起動します。これにより、Visual Studio の主な使用は、アナライザーのビルド中にテストインスタンスの影響を受けないようになります。 この方法を初めて起動すると、Visual studio をインストールした後に Visual Studio を初めて起動したときと同様に、いくつかの初期化が行われます。

 コンソールプロジェクトを作成し、コンソールアプリケーションの Main メソッドに配列コードを入力します。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);

```

のコード行には、 `ImmutableArray` 変更できない NuGet パッケージを取得し、ステートメントをコードに追加する必要があるため、波線が付き `using` ます。 **ソリューションエクスプローラー**のプロジェクトノードで右のポインターボタンを押し、[ **NuGet パッケージの管理**] を選択します。 NuGet マネージャーで、検索ボックスに「不変」と入力し、左側のウィンドウで項目 "system.string" を選択して、右側のウィンドウで [インストール] ボタンをクリックします ("Microsoft.................................. パッケージをインストールすると、プロジェクト参照への参照が追加されます。

の下に赤い波線が表示されるので、 `ImmutableArray` その識別子にキャレットを置き、 **ctrl +.** キーを押します。 (ピリオド) をクリックして修正候補メニューを表示し、適切なステートメントを追加し `using` ます。

**すべてを保存し** 、Visual Studio の2番目のインスタンスを閉じて、続行するためのクリーンな状態にします。

## <a name="finishing-the-analyzer-using-edit-and-continue"></a>エディットコンティニュを使用してアナライザーを終了する
Visual Studio の最初のインスタンスで、メソッドの先頭にブレークポイントを設定します。そのためには、 `AnalyzeObjectCreation` 最初の行にあるキャレットを使用して、 **F9** キーを押します。

**F5 キー**を押して再度アナライザーを起動し、Visual Studio の2番目のインスタンスで、前回作成したコンソールアプリケーションを再度開きます。

Roslyn コンパイラによってオブジェクト作成式が表示され、アナライザーに呼び出されるため、ブレークポイントで Visual Studio の最初のインスタンスに戻ります。

**オブジェクトの作成ノードを取得します。** F10 キーを押して変数を設定する行をステップオーバーし、[ `objectCreation` **イミディエイト] ウィンドウ**で式を評価し**F10** `“objectCreation.ToString()”` ます。 変数が指す構文ノードがコードであり、探しているものだけであることがわかり `"new ImmutableArray<int>()"` ます。

**ImmutableArray \<T> Type オブジェクトを取得します。** 作成される型が ImmutableArray であるかどうかを確認する必要があります。 まず、この型を表すオブジェクトを取得します。 セマンティックモデルを使用して型を確認し、正確な型があることを確認し、ToString () の文字列を比較しません。 関数の末尾に次のコード行を入力します。

```csharp

var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");

```

Backquotes (') とジェネリックパラメーターの数を使用して、メタデータにジェネリック型を指定します。 そのため、"...\<T>メタデータ名に ImmutableArray "を指定します。

セマンティックモデルには多くの便利な機能があり、シンボル、データフロー、変数の有効期間などに関する質問を行うことができます。Roslyn は、さまざまなエンジニアリング上の理由 (パフォーマンス、モデリングに誤りのあるコードなど) に対して、セマンティックモデルから構文ノードを分離します。 コンパイルモデルで、参照に含まれている情報を検索して正確な比較を行う必要があります。

エディターウィンドウの左側には、黄色の実行ポインターをドラッグできます。 変数を設定する行までドラッグし、 `objectCreation` **F10**キーを使用して新しいコード行をステップオーバーします。 変数の上にマウスポインターを置くと `immutableArrayOfType` 、セマンティックモデルで正確な型が見つかったことがわかります。

**オブジェクト作成式の型を取得します。** この記事では、"Type" をいくつかの方法で使用しますが、これは "新しい Foo" 式がある場合は、Foo のモデルを取得する必要があることを意味します。 ImmutableArray 型であるかどうかを確認するために、オブジェクト作成式の型を取得する必要があり \<T> ます。 セマンティックモデルを再度使用して、オブジェクト作成式の型シンボル (ImmutableArray) のシンボル情報を取得します。 関数の末尾に次のコード行を入力します。

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type) as INamedTypeSymbol;

```

アナライザーは、エディターバッファー内の不完全または正しくないコードを処理する必要があるため (たとえば、ステートメントが存在しない場合)、があるかどうかを `using` 確認する必要があり `symbolInfo` `null` ます。 分析を完了するには、シンボル情報オブジェクトから名前付きの型 (INamedTypeSymbol) を取得する必要があります。

**型を比較します。** 探しているオープンジェネリック型の T があり、コードの型は具象ジェネリック型であるため、型の構築元 (オープンジェネリック型) のシンボル情報に対してクエリを実行し、その結果をと比較し `immutableArrayOfTType` ます。 メソッドの最後に、次のように入力します。

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**診断を報告します。** 診断の報告は非常に簡単です。 生成されたルールは、Initialize メソッドの前に定義されているプロジェクトテンプレートで使用します。 コード内のこのような状況ではエラーが発生するため、初期化されたルールの行を (赤の波線) で置き換えることができ `DiagnosticSeverity.Warning` `DiagnosticSeverity.Error` ます。 ルールの残りの部分では、チュートリアルの最初の部分で編集したリソースを初期化します。 また、オブジェクト作成式の型指定の場所である、波線の場所も報告する必要があります。 次のコードをブロックに入力し `if` ます。

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

関数は次のようになります (たとえば、形式が異なる場合があります)。

```csharp
private void AnalyzeObjectCreation(SyntaxNodeAnalysisContext context)
{
    var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
    var immutableArrayOfTType =
        context.SemanticModel
               .Compilation
               .GetTypeByMetadataName(
                   "System.Collections.Immutable.ImmutableArray`1");
    var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type) as
        INamedTypeSymbol;
    if (symbolInfo != null &&
        symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
    {
        context.ReportDiagnostic(
            Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
    }
}

```

アナライザーが動作していることを確認できるように、ブレークポイントを削除します (Visual Studio の最初のインスタンスに戻るまで停止します)。 実行ポインターをメソッドの先頭にドラッグし、 **F5** キーを押して実行を続行します。 Visual Studio の2番目のインスタンスに戻ると、コンパイラによってコードの検証が開始され、アナライザーが呼び出されます。 の下に波線が表示でき `ImmutableType<int>` ます。

## <a name="adding-a-code-fix-for-the-code-issue"></a>コードの問題に対する "コード修正" の追加
開始する前に、Visual Studio の2番目のインスタンスを閉じ、Visual Studio の最初のインスタンス (アナライザーを開発している場所) でデバッグを停止します。

**新しいクラスを追加します。** ソリューションエクスプローラーのプロジェクトノードのショートカットメニュー (右ポインターボタン) を使用して、新しい項目の追加を選択します。 という名前のクラスを追加 `BuildCodeFixProvider` します。 このクラスはから派生する必要があり、 `CodeFixProvider` CTRL + を使用する必要があり **ます。** (ピリオド) を呼び出して、正しいステートメントを追加するコード修正プログラムを呼び出し `using` ます。 このクラスには、属性で注釈を付ける必要があります。また、このクラスには、 `ExportCodeFixProvider` 列挙型を解決するためのステートメントを追加する必要があり `using` `LanguageNames` ます。 クラスファイルには、次のコードが含まれている必要があります。

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}

```

**派生したメンバーをスタブします。** 次に、エディターのキャレットを識別子に配置 `CodeFixProvider` し、 **ctrl +** キーを押します。 (ピリオド) を使用して、この抽象基本クラスの実装をスタブします。 これにより、プロパティとメソッドが生成されます。

**プロパティを実装します。** `FixableDiagnosticIds`プロパティの `get` 本文に次のコードを入力します。

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn は、単純に文字列であるこれらの識別子を照合することで、診断と修正をまとめます。 プロジェクトテンプレートによって診断 ID が生成され、自由に変更できるようになりました。 プロパティのコードは、アナライザークラスからの ID のみを返します。

**RegisterCodeFixAsync メソッドはコンテキストを受け取ります。** コード修正は複数の診断に適用される可能性があるため、または1行のコードで複数の問題が発生する可能性があるため、コンテキストは重要です。 「コンテキスト」と入力します。 メソッドの本体では、Intellisense の入力候補一覧に、役に立つメンバーがいくつか表示されます。 修正をキャンセルする必要があるかどうかを確認できる CancellationToken メンバーがあります。 多くの便利なメンバーを持つドキュメントメンバーがあり、プロジェクトおよびソリューションモデルオブジェクトにアクセスできます。 これには、診断を報告したときに指定されたコードの場所の開始と終了を示すスパンメンバーがあります。

**メソッドを非同期にします。** 最初に実行する必要があるのは、生成されたメソッド宣言をメソッドとして修正することです `async` 。 `async`メソッドがを返す場合でも、抽象クラスの実装をスタブするコード修正では、キーワードは含まれません `Task` 。

**構文ツリーのルートを取得します。** コードを変更するには、コード修正によって変更された新しい構文ツリーを生成する必要があります。 `Document`コンテキストからを呼び出すためのが必要 `GetSyntaxRootAsync` です。 これは非同期メソッドです。構文ツリーを取得するための不明な作業があります。たとえば、ディスクからのファイルの取得、解析、およびそのための Roslyn コードモデルのビルドなどです。 この期間中、Visual Studio UI の応答性を向上させる必要があります。これは、を使用してを有効にし `async` ます。 メソッドのコード行を次のコードに置き換えます。

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**問題のあるノードを見つけます。** コンテキストのスパンを渡しますが、見つけたノードは、変更する必要のあるコードではない可能性があります。 報告された診断では、(波線が属している) 型識別子のスパンのみが提供されていましたが、オブジェクト作成式全体を置き換える必要があります。これには、 `new` 先頭の keywoard と末尾のかっこを含めます。 メソッドに次のコードを追加します (および **CTRL +.** にステートメントを追加するには、次のようにし `using` `ObjectCreationExpressionSyntax` ます。

```csharp

var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

 **電球 UI のコード修正を登録します。** コード修正を登録すると、Roslyn が Visual Studio 電球 UI に自動的にプラグインされます。 エンドユーザーには、CTRL + を使用できることが表示され **ます。** (期間) アナライザーが正しくないコンストラクターを使用している場合は、 `ImmutableArray<T>` を使用します。 コード修正プロバイダーは問題が発生した場合にのみ実行されるため、探しているオブジェクト作成式があると仮定できます。 コンテキストパラメーターから、メソッドの末尾に次のコードを追加することで、新しいコード修正を登録でき `RegisterCodeFixAsync` ます。

```csharp

context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

エディターのキャレットを識別子に配置して `CodeAction` から、 **CTRL キーを押しながら**を使用する必要があります。 (ピリオド) を入力して、 `using` この型に適切なステートメントを追加します。

次に、エディターのキャレットを識別子に配置 `ChangeToImmutableArrayEmpty` し、 **CTRL キーを押しながら**を使用します。 ここでも、このメソッドのスタブを生成します。

最後に追加したこのコードスニペットは、 `CodeAction` という問題の種類の診断 ID を渡すことによって、コード修正を登録します。 この例では、このコードが修正プログラムを提供する診断 ID が1つだけであるため、診断 Id の配列の最初の要素を渡すだけで済みます。 を作成するときに、 `CodeAction` 電球の UI がコード修正の説明として使用するテキストを渡します。 また、CancellationToken を受け取り、新しいドキュメントを返す関数も渡します。 新しいドキュメントには、を呼び出す修正コードを含む新しい構文ツリーがあり `ImmutableArray.Empty` ます。 このコードスニペットでは、ラムダを使用して、objectCreation ノードとコンテキストのドキュメントを閉じることができます。

**新しい構文ツリーを構築します。** `ChangeToImmutableArrayEmpty`先ほど生成したスタブがあるメソッドで、コード行を入力します `ImmutableArray<int>.Empty;` 。 Syntax Visualizer ツールウィンドウを再度表示した場合は、この構文が SimpleMemberAccessExpression ノードであることがわかります。 このメソッドでは、このメソッドを作成して新しいドキュメントに返す必要があります。

最初にを `ChangeToImmutableArrayEmpty` 追加するのは `async` 、 `Task<Document>` コードジェネレーターがメソッドを非同期にする必要がないためです。

本体に次のコードを入力して、メソッドが次のようになるようにします。

```csharp

private async Task<Document> ChangeToImmutableArrayEmpty(
    ObjectCreationExpressionSyntax objectCreation, Document document,
    CancellationToken c)
{
    var generator = SyntaxGenerator.GetGenerator(document);
    var memberAccess =
        generator.MemberAccessExpression(objectCreation.Type, "Empty");
    var oldRoot = await document.GetSyntaxRootAsync(c);
    var newRoot = oldRoot.ReplaceNode(objectCreation, memberAccess);
    return document.WithSyntaxRoot(newRoot);
}
```

エディターのキャレットを識別子に配置し、CTRL + を使用する必要があり `SyntaxGenerator` **ます。** (ピリオド) を入力して、 `using` この型に適切なステートメントを追加します。

このコードでは、を使用します `SyntaxGenerator` 。これは、新しいコードを構築するための非常に便利な型です。 コードの問題があるドキュメントのジェネレーターを取得した後、はを `ChangeToImmutableArrayEmpty` 呼び出し `MemberAccessExpression` 、アクセスするメンバーを持つ型を渡し、メンバーの名前を文字列として渡します。

次に、メソッドはドキュメントのルートをフェッチします。これには、一般的なケースでは任意の処理が含まれる可能性があるため、コードはこの呼び出しを待機し、キャンセルトークンを渡します。 Roslyn コードモデルは、.NET 文字列を使用する場合のように、変更できません。文字列を更新すると、新しい文字列オブジェクトが返されます。 を呼び出すと `ReplaceNode` 、新しいルートノードが返されます。 ほとんどの構文ツリーは変更できないため共有されていますが、 `objectCreation` ノードはノードに置き換えられ、 `memberAccess` すべての親ノードが構文ツリールートまで置き換えられます。

## <a name="trying-your-code-fix"></a>コードを修正しています
**F5**キーを押して、Visual Studio の2番目のインスタンスでアナライザーを実行できるようになりました。 前に使用したコンソールプロジェクトを開きます。 電球が表示され、新しいオブジェクトの作成式がになり `ImmutableArray<int>` ます。 Ctrl キーを押し **ながら** (ピリオド) をクリックすると、コードの修正が表示され、電球の UI に自動的に生成されたコードの相違のプレビューが表示されます。 これは、roslyn によって作成されます。

Pro ヒント: Visual Studio の2番目のインスタンスを起動したときに、コードの修正を含む電球が表示されない場合は、Visual Studio コンポーネントキャッシュをクリアする必要がある場合があります。 キャッシュをクリアすると、Visual Studio によってコンポーネントが再検証されるため、Visual Studio は最新のコンポーネントを選択する必要があります。 最初に、Visual Studio の2番目のインスタンスをシャットダウンします。 次に、Windows エクスプローラーで、ユーザーディレクトリ (c:\users \\<userid) にアクセス \> して AppData\Local\Microsoft\VisualStudio\14.0Roslyn を検索し \\ ます。 このディレクトリで、サブディレクトリ ComponentModelCache を削除します。 "14" は、Visual Studio を使用してバージョンをバージョンに変更します。

## <a name="talk-video-and-finish-code-project"></a>ビデオと完了コードプロジェクトの説明
この例については [、この後](https://channel9.msdn.com/events/Build/2015/3-725)で開発し、説明します。 このチュートリアルでは、作業アナライザーについて説明し、その構築について説明します。

完成したすべてのコードを [ここで](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)確認できます。 サブフォルダー DoNotUseImmutableArrayCollectionInitializer と DoNotUseImmutableArrayCtor にはそれぞれ、問題を見つけるための C# ファイルと、Visual Studio 電球 UI に表示されるコード修正を実装する C# ファイルがあります。 完成したコードでは、ImmutableArray type オブジェクトが過剰にフェッチされないように、もう少し抽象化されてい \<T> ます。 入れ子になった登録済みのアクションを使用して、サブアクション (オブジェクトの分析の分析とコレクションの分析の分析) を実行するたびに使用可能なコンテキストに型オブジェクトを保存します。

## <a name="see-also"></a>参照
[ \\ \ ビルド 2015](https://channel9.msdn.com/events/Build/2015/3-725)github での 
 [コード完成したコード](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)の作成 github で  
 のいくつかの例については[、3種類のアナライザーにグループ化](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)された github  
 [OSS サイト](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)の  
 [FxCop 規則 github の roslyn アナライザーを使用](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)して実装します。
