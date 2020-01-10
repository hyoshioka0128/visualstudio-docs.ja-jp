---
title: ImmutableArrays | の roslyn アナライザーとコード対応ライブラリMicrosoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8665a37e4afd387ff4f77a8bdb5da430d773ae1d
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75848720"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>ImmutableArrays 用の roslyn アナライザーとコード対応ライブラリ

[.NET Compiler Platform](https://github.com/dotnet/roslyn) ("Roslyn") を使用すると、コード対応のライブラリをビルドできます。 コード対応ライブラリは、ツール (Roslyn アナライザー) を使用して、最適な方法でライブラリを使用したり、エラーを回避したりするための機能を提供します。 このトピックでは、[システムコレクション](https://www.nuget.org/packages/System.Collections.Immutable)の NuGet パッケージを使用するときに、一般的なエラーをキャッチするために、実際の Roslyn アナライザーを構築する方法について説明します。 また、この例では、アナライザーによって検出されたコードの問題に対してコード修正を行う方法も示しています。 ユーザーは、Visual Studio 電球 UI にコード修正プログラムを表示し、コードの修正を自動的に適用できます。

## <a name="get-started"></a>作業開始

この例をビルドするには、次のものが必要です。

* Visual Studio 2015 (Express Edition ではない) 以降のバージョン。 無料の[Visual Studio Community Edition](https://visualstudio.microsoft.com/vs/community/)を使用できます。
* [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。 また、Visual Studio をインストールするときに、 **[共通ツール]** の**Visual Studio Extensibility Tools**をオンにして SDK を同時にインストールすることもできます。 Visual Studio を既にインストールしている場合は、メインメニュー**ファイル** > **新しい** > **プロジェクト**に移動し、左側のナビゲーションウィンドウ**C#** で **[拡張機能]** を選択して、この SDK をインストールすることもできます。 **[Visual Studio Extensibility Tools のインストール]** 階層リンクプロジェクトテンプレートを選択すると、SDK をダウンロードしてインストールするように求められます。
* [.NET Compiler Platform ("Roslyn") SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK)。 この SDK をインストールするには、メインメニュー**ファイル** > **新しい** > **プロジェクト** に移動し**C#** 、左側のナビゲーションウィンドウで **拡張機能** を選択します。 **[.NET COMPILER PLATFORM sdk のダウンロード]** 階層リンクプロジェクトテンプレートを選択すると、sdk をダウンロードしてインストールするように求められます。 この SDK には、 [Roslyn Syntax Visualizer](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer)が含まれています。 この便利なツールを使用すると、アナライザーでどのような種類のコードモデルを検索する必要があるかを判断できます。 Analyzer インフラストラクチャは、特定のコードモデル型に対してコードを呼び出すので、コードは必要なときにのみ実行され、関連するコードの分析にのみ集中できます。

## <a name="whats-the-problem"></a>何がそんなに問題ですか。

たとえば、ImmutableArray (<xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>) などのサポートを含むライブラリを提供するとします。 C#開発者にとっては、.NET 配列について多くの経験があります。 ただし、実装で使用される ImmutableArrays および最適化手法の性質上、developer C# intuitions では、次に説明するように、ライブラリのユーザーが破損したコードを記述することになります。 さらに、ユーザーは実行時までエラーを表示しません。これは、Visual Studio と .NET で使用される品質エクスペリエンスではありません。

ユーザーは、次のようなコードを記述することに慣れています。

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

空の配列を作成して後続のコード行に入力し、コレクション初期化子構文C#を使用することは、開発者にとってよく知られています。 ただし、実行時に ImmutableArray クラッシュに対して同じコードを記述すると、次のようになります。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

最初のエラーは、ImmutableArray 実装が構造体を使用して基になるデータストレージをラップしているためです。 構造体は、パラメーターのないコンストラクターを持つ必要があります。これにより、`default(T)` 式は、すべての0または null メンバーを含む構造体を返すことができます。 コードが `b1.Length`にアクセスするときに、ImmutableArray 構造体に基になるストレージ配列がないため、実行時の null 参照解除エラーが発生します。 空の ImmutableArray を作成する正しい方法は `ImmutableArray<int>.Empty`です。

`ImmutableArray.Add` メソッドは、呼び出しごとに新しいインスタンスを返すため、コレクション初期化子のエラーが発生します。 ImmutableArrays は変化しないため、新しい要素を追加すると、新しい ImmutableArray オブジェクトが返されます (これは、以前に既存の ImmutableArray を使用してパフォーマンス上の理由からストレージを共有する可能性があります)。 `b2` は `Add()` 5 回呼び出す前に最初の ImmutableArray を指しているため、`b2` は既定の ImmutableArray になります。 また、この呼び出しの長さは、null 参照解除エラーによってもクラッシュします。 Add を手動で呼び出すことなく ImmutableArray を初期化する正しい方法は、`ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})`を使用することです。

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>アナライザーをトリガーするための関連する構文ノードの種類の検索

 アナライザーのビルドを開始するには、まず、検索する必要がある SyntaxNode の種類を確認します。 メニュー**ビュー** > **他の Windows** > **roslyn Syntax Visualizer**から**Syntax Visualizer**を起動します。

`b1`を宣言する行にエディターのキャレットを置きます。 構文ツリーの `LocalDeclarationStatement` ノードに表示されている Syntax Visualizer が表示されます。 このノードには `VariableDeclaration`があります。このノードには、`VariableDeclarator`があり、その後には `EqualsValueClause`があり、最後に `ObjectCreationExpression`があります。 ノードの Syntax Visualizer ツリーをクリックすると、エディターウィンドウの構文が強調表示され、そのノードで表されるコードが表示されます。 SyntaxNode サブタイプの名前は、 C#文法で使用されている名前と一致します。

## <a name="create-the-analyzer-project"></a>Analyzer プロジェクトを作成する

メインメニューから、[**ファイル** > **新しい** > **プロジェクト**] を選択します。 **新しいプロジェクト** ダイアログで、 **C#** 左側のナビゲーションバーの プロジェクト の下にある **拡張機能** をクリックし、右側のウィンドウで **アナライザー with Code Fix** プロジェクトテンプレートを選択します。 名前を入力し、ダイアログを確認します。

このテンプレートは、 *DiagnosticAnalyzer.cs*ファイルを開きます。 [エディターバッファー] タブを選択します。このファイルには、`DiagnosticAnalyzer` (Roslyn API 型) から派生したアナライザークラス (プロジェクトに指定した名前の形式) があります。 新しいクラスには、アナライザーが使用されC#ていることを宣言する `DiagnosticAnalyzerAttribute` があります。これにより、コンパイラがアナライザーを検出して読み込むことができます。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

コードを対象C#とする Visual Basic を使用してアナライザーを実装できます。また、その逆も可能です。 DiagnosticAnalyzerAttribute では、アナライザーが1つの言語を対象とするか、またはその両方を対象とするかを選択することが重要です。 言語の詳細なモデリングを必要とする洗練されたアナライザーは、1つの言語のみを対象にすることができます。 たとえば、アナライザーが型名またはパブリックメンバー名のみをチェックする場合は、Visual Basic とC#で共通言語モデルの Roslyn プランを使用することができます。 たとえば、FxCop は、クラスが <xref:System.Runtime.Serialization.ISerializable>を実装していることを警告しますが、<xref:System.SerializableAttribute> 属性は言語に依存せず、Visual Basic C#とコードの両方に対して機能します。

## <a name="initialize-the-analyzer"></a>アナライザーの初期化

 `DiagnosticAnalyzer` クラスの少し下にスクロールして、`Initialize` メソッドを表示します。 コンパイラは、アナライザーをアクティブ化するときにこのメソッドを呼び出します。 メソッドは `AnalysisContext` オブジェクトを受け取ります。これにより、アナライザーはコンテキスト情報を取得し、分析するコードの種類のイベントのコールバックを登録できます。

```csharp
public override void Initialize(AnalysisContext context) {}
```

このメソッドで新しい行を開き、「context」と入力します。 IntelliSense の入力候補一覧を表示します。 入力候補一覧には、さまざまな種類のイベントを処理するための `Register...` メソッドが多数あります。 たとえば、1つ目の `RegisterCodeBlockAction`は、ブロックのコードにコールバックします。これは通常、中かっこの間のコードです。 ブロックに登録すると、フィールドの初期化子、属性に与えられた値、または省略可能なパラメーターの値をコードにコールバックすることもできます。

別の例として、`RegisterCompilationStartAction`はコンパイルの開始時にコードにコールバックします。これは、さまざまな場所で状態を収集する必要がある場合に便利です。 データ構造を作成して、使用するすべてのシンボルを収集することができます。また、アナライザーが構文やシンボルに対してコールバックされるたびに、データ構造内の各場所に関する情報を保存することができます。 コンパイルの終了によってコールバックが呼び出されたときに、保存したすべての場所を分析して、コードが各 `using` ステートメントからどのシンボルを使用しているかをレポートできます。

**Syntax Visualizer**を使用して、コンパイラが Objectfrom 式を処理するときに呼び出すことを学習しました。 このコードを使用して、コールバックを設定します。

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

構文ノードに登録し、オブジェクト作成構文ノードのみをフィルター処理します。 慣例により、アナライザーの作成者はアクションを登録するときにラムダを使用します。これにより、アナライザーをステートレスに保つことができます。 Visual Studio の [**使用法から生成]** 機能を使用して、`AnalyzeObjectCreation` メソッドを作成できます。 これにより、正しい種類のコンテキストパラメーターも生成されます。

## <a name="set-properties-for-users-of-your-analyzer"></a>アナライザーのユーザーのプロパティを設定する

アナライザーが Visual Studio UI に適切に表示されるように、次のコード行を探して変更し、アナライザーを識別します。

```csharp
internal const string Category = "Naming";
```

変更`"Naming"`に`"API Guidance"`します。

次に、**ソリューションエクスプローラー**を使用して、プロジェクト内の*リソース .resx*ファイルを見つけて開きます。 アナライザー、タイトルなどの説明を入力できます。ここでは、これらのすべての値を `"Don't use ImmutableArray<T> constructor"` に変更できます。 文字列形式の引数を文字列に含めることができます ({0}、{1}など)。後で `Diagnostic.Create()`を呼び出すときに、渡される引数の `params` 配列を指定できます。

## <a name="analyze-an-object-creation-expression"></a>オブジェクト作成式の分析

`AnalyzeObjectCreation` メソッドは、コードアナライザーフレームワークによって提供されるさまざまな種類のコンテキストを受け取ります。 `Initialize` メソッドの `AnalysisContext` を使用すると、アクションコールバックを登録してアナライザーを設定できます。 たとえば、`SyntaxNodeAnalysisContext`には、渡すことができる `CancellationToken` があります。 ユーザーがエディターで入力を開始すると、Roslyn はアナライザーの実行をキャンセルして作業を保存し、パフォーマンスを向上させます。 もう1つの例として、このコンテキストには、オブジェクト作成構文ノードを返す Node プロパティがあります。

ノードを取得します。これは、構文ノードアクションをフィルター処理した型であると想定できます。

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>初めてアナライザーを使用して Visual Studio を起動する

アナライザーをビルドして実行して Visual Studio を起動します ( **F5**キーを押します)。 **ソリューションエクスプローラー**のスタートアッププロジェクトは vsix プロジェクトであるため、コードを実行すると、コードと vsix がビルドされ、その vsix がインストールされた状態で Visual Studio が起動します。 この方法で Visual Studio を起動すると、別のレジストリハイブで起動します。これにより、Visual Studio の主な使用は、アナライザーのビルド中にテストインスタンスの影響を受けないようになります。 この方法を初めて起動すると、Visual studio をインストールした後に Visual Studio を初めて起動したときと同様に、いくつかの初期化が行われます。

コンソールプロジェクトを作成し、コンソールアプリケーションの Main メソッドに配列コードを入力します。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

変更できない NuGet パッケージを取得し、コードに `using` ステートメントを追加する必要があるため、`ImmutableArray` を持つコード行には波線が表示されます。 **ソリューションエクスプローラー**のプロジェクトノードで右のポインターボタンをクリックし、 **[NuGet パッケージの管理]** を選択します。 NuGet マネージャーで、検索ボックスに「不変」と入力し、左側のウィンドウで**項目 [変更不可]** **を選択**して、右側のウィンドウにある **[インストール]** ボタンをクリックします。 パッケージをインストールすると、プロジェクト参照への参照が追加されます。

`ImmutableArray`の下に赤い波線が表示されるので、その識別子にキャレットを置き、 **ctrl**+を押し**ます。** (ピリオド) をクリックして修正候補メニューを表示し、適切な `using` ステートメントを追加します。

**すべてを保存し**、Visual Studio の2番目のインスタンスを閉じて、続行するためのクリーンな状態にします。

## <a name="finish-the-analyzer-using-edit-and-continue"></a>エディットコンティニュを使用してアナライザーを終了する

Visual Studio の最初のインスタンスで、`AnalyzeObjectCreation` メソッドの先頭にブレークポイントを設定します。そのためには、最初の行で、 **F9**キーを押します。

**F5 キー**を押して再度アナライザーを起動し、Visual Studio の2番目のインスタンスで、最後に作成したコンソールアプリケーションを再度開きます。

Roslyn コンパイラによってオブジェクト作成式が表示され、アナライザーに呼び出されるため、ブレークポイントで Visual Studio の最初のインスタンスに戻ります。

**オブジェクトの作成ノードを取得します。** **F10**キーを押して `objectCreation` 変数を設定する行をステップオーバーし、[**イミディエイト] ウィンドウ**で式 `"objectCreation.ToString()"`を評価します。 変数が指す構文ノードがコード `"new ImmutableArray<int>()"`であり、探しているものだけであることがわかります。

**ImmutableArray < T\> Type オブジェクトを取得します。** 作成される型が ImmutableArray であるかどうかを確認する必要があります。 まず、この型を表すオブジェクトを取得します。 セマンティックモデルを使用して型を確認し、正確な型があることを確認します。文字列を `ToString()`と比較することはできません。 関数の末尾に次のコード行を入力します。

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

メタデータには、バッククォート (') とジェネリックパラメーターの数を使用してジェネリック型を指定します。 そのため、"...ImmutableArray\<T > "をメタデータ名にします。

セマンティックモデルには多くの便利な機能があり、シンボル、データフロー、変数の有効期間などに関する質問を行うことができます。Roslyn は、さまざまなエンジニアリング上の理由 (パフォーマンス、モデリングに誤りのあるコードなど) に対して、セマンティックモデルから構文ノードを分離します。 コンパイルモデルで、参照に含まれている情報を検索して正確な比較を行う必要があります。

エディターウィンドウの左側には、黄色の実行ポインターをドラッグできます。 `objectCreation` 変数を設定する行までドラッグし、 **F10**キーを使用して新しいコード行をステップオーバーします。 `immutableArrayOfType`変数の上にマウスポインターを置くと、セマンティックモデルで正確な型が見つかったことがわかります。

**オブジェクト作成式の型を取得します。** この記事では、"Type" をいくつかの方法で使用しますが、これは "新しい Foo" 式がある場合は、Foo のモデルを取得する必要があることを意味します。 オブジェクト作成式の型を取得して、それが ImmutableArray\<T > 型であるかどうかを確認する必要があります。 セマンティックモデルを再度使用して、オブジェクト作成式の型シンボル (ImmutableArray) のシンボル情報を取得します。 関数の末尾に次のコード行を入力します。

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

アナライザーは、エディターバッファー内の不完全または不適切なコードを処理する必要があるため (たとえば、`using` ステートメントが存在しない場合)、`symbolInfo` が `null`されているかどうかを確認する必要があります。 分析を完了するには、シンボル情報オブジェクトから名前付きの型 (INamedTypeSymbol) を取得する必要があります。

**型を比較します。** 探しているオープンジェネリック型 T があり、コードの型は具象ジェネリック型であるため、型の構築元 (オープンジェネリック型) のシンボル情報に対してクエリを実行し、その結果を `immutableArrayOfTType`と比較します。 メソッドの最後に、次のように入力します。

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**診断を報告します。** 診断の報告は非常に簡単です。 生成されたルールは、Initialize メソッドの前に定義されているプロジェクトテンプレートで使用します。 コード内のこの状況はエラーであるため、初期化されたルールの行を変更して、`DiagnosticSeverity.Warning` (緑の波線) を `DiagnosticSeverity.Error` (赤の波線) に置き換えることができます。 ルールの残りの部分では、チュートリアルの最初の部分で編集したリソースを初期化します。 また、波線の場所を報告する必要もあります。これは、オブジェクト作成式の型指定の場所です。 `if` ブロックに次のコードを入力します。

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
    var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as
        INamedTypeSymbol;
    if (symbolInfo != null &&
        symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
    {
        context.ReportDiagnostic(
            Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
    }
}
```

アナライザーが動作していることを確認できるように、ブレークポイントを削除します (Visual Studio の最初のインスタンスに戻るまで停止します)。 実行ポインターをメソッドの先頭にドラッグし、 **F5**キーを押して実行を続行します。 Visual Studio の2番目のインスタンスに戻ると、コンパイラによってコードの検証が開始され、アナライザーが呼び出されます。 `ImmutableType<int>`の下に波線が表示できます。

## <a name="adding-a-code-fix-for-the-code-issue"></a>コードの問題に対する "コード修正" の追加

開始する前に、Visual Studio の2番目のインスタンスを閉じ、Visual Studio の最初のインスタンス (アナライザーを開発している場所) でデバッグを停止します。

**新しいクラスを追加します。** **ソリューションエクスプローラー**のプロジェクトノードのショートカットメニュー (右ポインターボタン) を使用して、新しい項目の追加を選択します。 `BuildCodeFixProvider`というクラスを追加します。 このクラスは `CodeFixProvider`から派生する必要があり、 **Ctrl**+を使用する必要があり**ます。** (ピリオド) を実行して、正しい `using` ステートメントを追加するコード修正を呼び出します。 このクラスには、`ExportCodeFixProvider` 属性で注釈を付ける必要があります。また、`LanguageNames` 列挙型を解決するには `using` ステートメントを追加する必要があります。 クラスファイルには、次のコードが含まれている必要があります。

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**派生したメンバーをスタブします。** 次に、エディターのキャレットを識別子 `CodeFixProvider` に配置し、 **ctrl**+を押し**ます。** (ピリオド) を使用して、この抽象基本クラスの実装をスタブします。 これにより、プロパティとメソッドが生成されます。

**プロパティを実装します。** `FixableDiagnosticIds` プロパティの `get` 本体に次のコードを入力します。

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn は、単純に文字列であるこれらの識別子を照合することで、診断と修正をまとめます。 プロジェクトテンプレートによって診断 ID が生成され、自由に変更できるようになりました。 プロパティのコードは、アナライザークラスからの ID のみを返します。

**RegisterCodeFixAsync メソッドはコンテキストを受け取ります。** コード修正は複数の診断に適用される可能性があるため、または1行のコードで複数の問題が発生する可能性があるため、コンテキストは重要です。 「コンテキスト」と入力します。 メソッドの本体では、IntelliSense の入力候補一覧に、役に立つメンバーがいくつか表示されます。 修正をキャンセルする必要があるかどうかを確認できる CancellationToken メンバーがあります。 多くの便利なメンバーを持つドキュメントメンバーがあり、プロジェクトおよびソリューションモデルオブジェクトにアクセスできます。 これには、診断を報告したときに指定されたコードの場所の開始と終了を示すスパンメンバーがあります。

**メソッドを非同期にします。** 最初に実行する必要があるのは、生成されたメソッド宣言を `async` メソッドに修正することです。 メソッドが `Task`を返す場合でも、抽象クラスの実装をスタブするコード修正では、`async` キーワードは含まれません。

**構文ツリーのルートを取得します。** コードを変更するには、コード修正によって変更された新しい構文ツリーを生成する必要があります。 `GetSyntaxRootAsync`を呼び出すには、コンテキストから `Document` が必要です。 これは非同期メソッドです。構文ツリーを取得するための不明な作業があります。たとえば、ディスクからのファイルの取得、解析、およびそのための Roslyn コードモデルのビルドなどです。 この時間内に Visual Studio UI の応答性を向上させる必要があります。このとき、`async` が有効になります。 メソッドのコード行を次のコードに置き換えます。

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**問題のあるノードを見つけます。** コンテキストのスパンを渡しますが、見つけたノードは、変更する必要のあるコードではない可能性があります。 報告された診断では、(波線が属している) 型識別子のスパンのみが提供されていましたが、オブジェクト作成式全体を置き換える必要があります。これには、先頭に `new` キーワードを含め、末尾にかっこを追加する必要があります。 メソッドに次のコードを追加します (および、 **Ctrl**+を使用し**ます。** `ObjectCreationExpressionSyntax`の `using` ステートメントを追加するには:

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**電球 UI のコード修正を登録します。** コード修正を登録すると、Roslyn が Visual Studio 電球 UI に自動的にプラグインされます。 エンドユーザーには、 **Ctrl**+を使用できることが表示され**ます。** (期間) アナライザーが正しくない `ImmutableArray<T>` コンストラクターで使用する場合は、を使用します。 コード修正プロバイダーは問題が発生した場合にのみ実行されるため、探しているオブジェクト作成式があると仮定できます。 Context パラメーターから、`RegisterCodeFixAsync` メソッドの最後に次のコードを追加することで、新しいコード修正を登録できます。

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

エディターのキャレットを識別子に配置し、`CodeAction`してから、 **Ctrl**+を使用する必要があり**ます。** (ピリオド) を入力して、この型に適した `using` ステートメントを追加します。

次に、エディターのキャレットを `ChangeToImmutableArrayEmpty` 識別子に配置し、 **Ctrl**+を使用し**ます。** ここでも、このメソッドのスタブを生成します。

最後に追加したこのコードスニペットは、`CodeAction` と、見つかった問題の種類の診断 ID を渡すことによって、コード修正を登録します。 この例では、このコードが修正プログラムを提供する診断 ID が1つだけであるため、診断 Id の配列の最初の要素を渡すだけで済みます。 `CodeAction`を作成するときに、電球の UI がコード修正の説明として使用するテキストを渡します。 また、CancellationToken を受け取り、新しいドキュメントを返す関数も渡します。 新しいドキュメントには、`ImmutableArray.Empty`を呼び出す修正コードを含む新しい構文ツリーがあります。 このコードスニペットでは、ラムダを使用して、objectCreation ノードとコンテキストのドキュメントを閉じることができます。

**新しい構文ツリーを構築します。** 先ほど生成したスタブがある `ChangeToImmutableArrayEmpty` メソッドで、コードの行を入力します: `ImmutableArray<int>.Empty;`。 **Syntax Visualizer**ツールウィンドウを再度表示した場合は、この構文が SimpleMemberAccessExpression ノードであることがわかります。 このメソッドでは、このメソッドを作成して新しいドキュメントに返す必要があります。

`ChangeToImmutableArrayEmpty` の最初の変更は `Task<Document>` 前に `async` を追加することです。これは、コードジェネレーターがメソッドを非同期にする必要がないためです。

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

`SyntaxGenerator` 識別子にエディターのキャレットを置き、 **Ctrl**+を使用する必要があり**ます。** (ピリオド) を入力して、この型に適した `using` ステートメントを追加します。

このコードは `SyntaxGenerator`を使用します。これは、新しいコードを構築するための便利な型です。 コードの問題が発生したドキュメントのジェネレーターを取得した後、`ChangeToImmutableArrayEmpty` は `MemberAccessExpression`を呼び出し、アクセスするメンバーを持つ型を渡し、メンバーの名前を文字列として渡します。

次に、メソッドはドキュメントのルートをフェッチします。これには、一般的なケースでは任意の処理が含まれる可能性があるため、コードはこの呼び出しを待機し、キャンセルトークンを渡します。 Roslyn コードモデルは、.NET 文字列を使用する場合のように、変更できません。文字列を更新すると、新しい文字列オブジェクトが返されます。 `ReplaceNode`を呼び出すと、新しいルートノードが返されます。 ほとんどの構文ツリーは変更できないため共有されていますが、`objectCreation` ノードは `memberAccess` ノード、および構文ツリールートまでのすべての親ノードに置き換えられます。

## <a name="try-your-code-fix"></a>コードを修正してみてください

**F5**キーを押して、Visual Studio の2番目のインスタンスでアナライザーを実行できるようになりました。 前に使用したコンソールプロジェクトを開きます。 これで、新しいオブジェクト作成式が `ImmutableArray<int>`の場所に電球が表示されます。 **Ctrl**+を押し**ます。** (ピリオド) をクリックすると、コードの修正が表示され、電球の UI に自動的に生成されたコードの相違のプレビューが表示されます。 これは、roslyn によって作成されます。

**Pro ヒント:** Visual Studio の2番目のインスタンスを起動したときに、コードの修正を含む電球が表示されない場合は、Visual Studio コンポーネントキャッシュをクリアする必要があります。 キャッシュをクリアすると、Visual Studio によってコンポーネントが再検証されるため、Visual Studio は最新のコンポーネントを選択する必要があります。 最初に、Visual Studio の2番目のインスタンスをシャットダウンします。 次に、 **Windows エクスプローラー**で、 *%LOCALAPPDATA%\Microsoft\VisualStudio\16.0Roslyn\\* に移動します。 ("16.0" は、Visual Studio を使用してバージョン間で変更されます)。サブディレクトリ*Componentmodelcache*を削除します。

## <a name="talk-video-and-finish-code-project"></a>ビデオと完了コードプロジェクトの説明

この例については[、この後](https://channel9.msdn.com/events/Build/2015/3-725)で開発し、説明します。 このチュートリアルでは、作業アナライザーについて説明し、その構築について説明します。

完成したすべてのコードを[ここで](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)確認できます。 サブフォルダー *DoNotUseImmutableArrayCollectionInitializer*と*DoNotUseImmutableArrayCtor*にはそれぞれ、 C#問題を検出するためのC#ファイルと、Visual Studio 電球の UI に表示されるコード修正プログラムを実装するファイルがあります。 完成したコードは、ImmutableArray\<T > type オブジェクトを何度もフェッチしないように、もう少し抽象化されています。 入れ子になった登録済みのアクションを使用して、サブアクション (オブジェクトの分析の分析とコレクションの分析の分析) を実行するたびに使用可能なコンテキストに型オブジェクトを保存します。

## <a name="see-also"></a>関連項目

* [\\、ビルド2015のトーク](https://channel9.msdn.com/events/Build/2015/3-725)
* [GitHub の完成したコード](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [3種類のアナライザーにグループ化された GitHub のいくつかの例](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [GitHub OSS サイトのその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [GitHub で Roslyn アナライザーを使用して実装された FxCop 規則](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
