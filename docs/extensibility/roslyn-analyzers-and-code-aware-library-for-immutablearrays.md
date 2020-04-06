---
title: 不変配列の Roslyn アナライザーとコード対応ライブラリ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d6b26d27c77ecb578d8eef0807c35b8efb8581a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701389"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>不変配列の Roslyn アナライザーとコード対応ライブラリ

[.NET コンパイラ プラットフォーム](https://github.com/dotnet/roslyn)("Roslyn") は、コードに対応するライブラリを構築するのに役立ちます。 コード対応ライブラリには、ライブラリを最適な方法で使用したり、エラーを回避したりするためのツール (Roslyn アナライザー) を使用できる機能が用意されています。 このトピックでは、実際の Roslyn アナライザーを構築して[、System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable) NuGet パッケージを使用する際に一般的なエラーをキャッチする方法を示します。 この例では、アナライザーで検出されたコードの問題に対するコード修正を提供する方法も示します。 ユーザーは、Visual Studio 電球 UI でコードの修正を参照し、コードの修正プログラムを自動的に適用できます。

## <a name="get-started"></a>はじめに

この例をビルドするには、次のことが必要です。

* Visual Studio 2015 (エクスプレス エディションではない) またはそれ以降のバージョン。 無料の Visual [Studio コミュニティ エディションを](https://visualstudio.microsoft.com/vs/community/)使用できます。
* [ビジュアル スタジオ SDK](../extensibility/visual-studio-sdk.md). また、Visual Studio をインストールする際に、[**共通ツール**] の **[Visual Studio 拡張機能ツール**] をオンにして、SDK を同時にインストールすることもできます。 Visual Studio を既にインストールしている場合は、メイン メニューの **[ファイル** > **] メニューの [新しい** > **プロジェクト**] に移動し、左側のナビゲーション ペインで **[C#]** を選択し、[**機能拡張**] を選択して、この SDK をインストールすることもできます。 "Visual Studio**拡張機能ツールのインストール**" 階層リンク プロジェクト テンプレートを選択すると、SDK のダウンロードとインストールを求めるメッセージが表示されます。
* [.NET コンパイラ プラットフォーム ("Roslyn") SDK](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK). この SDK をインストールするには、メイン メニューの **[ファイル** > **] メニューの [新しい** > **プロジェクト**] に移動し、左側のナビゲーション ペインで **[C#]** を選択し、[**拡張性**] を選択します。 ".NET**コンパイラ プラットフォーム SDK**のダウンロード" プロジェクト テンプレートをダウンロードする] を選択すると、SDK のダウンロードとインストールを求めるメッセージが表示されます。 この SDK には[、Roslyn 構文ビジュアライザー](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer)が含まれています。 このツールは、アナライザーで探すコード モデルの種類を把握するのに役立ちます。 アナライザー インフラストラクチャは、特定のコード モデルの種類に対してコードを呼び出すため、コードは必要なときにのみ実行され、関連するコードの分析のみに集中できます。

## <a name="whats-the-problem"></a>何がそんなに問題ですか。

ImmutableArray (たとえば)<xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>サポートを持つライブラリを提供するとします。 C# 開発者は、.NET 配列に関して多くの経験を持っています。 ただし、実装で使用される ImmutableArrays と最適化手法の性質上、C# 開発者の直感により、次に説明するように、ライブラリのユーザーが壊れたコードを記述します。 さらに、ユーザーは、実行時までエラーを表示しません。

ユーザーは、次のようなコードの記述に精通しています。

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

空の配列を作成して後続のコード行を記述し、コレクション初期化子構文を使用することは、C# 開発者にとってわかりやすいものです。 ただし、実行時に ImmutableArray に対して同じコードを記述するとクラッシュします。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

最初のエラーは、ImmutableArray 実装が構造体を使用して基になるデータ ストレージをラップしたためです。 `default(T)`式がすべての 0 または null メンバーを持つ構造体を返すことができるように、構造体にはパラメーターなしのコンストラクターが必要です。 コードが`b1.Length`にアクセスすると、ImmutableArray 構造体に基になるストレージ配列がないため、実行時に null の逆参照エラーが発生します。 空の ImmutableArray を作成する正`ImmutableArray<int>.Empty`しい方法は です。

コレクション初期化子のエラーは、メソッドが`ImmutableArray.Add`呼び出すたびに新しいインスタンスを返すためです。 ImmutableArrays は変更されないため、新しい要素を追加すると、新しい ImmutableArray オブジェクトを取得できます (パフォーマンス上の理由から既存の ImmutableArray とストレージを共有する場合があります)。 5`b2`回呼び出す`Add()`前に最初の ImmutableArray を指すため、`b2`既定の ImmutableArray です。 この呼び出しの Length も null 逆参照エラーでクラッシュします。 手動で Add を呼び出さずに ImmutableArray`ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})`を初期化する正しい方法は、 を使用することです。

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>アナライザーをトリガーする関連する構文ノードタイプを見つける

 アナライザーの構築を開始するには、まず、検索する必要がある構文ノードの種類を確認します。 [**他** > の Windows Roslyn**構文ビジュア**ライザーを**表示** > ] メニューから**構文ビジュアライザーを**起動します。

を宣言する行にエディタのキャレットを`b1`置きます。 構文ビジュアライザーが、構文ツリーの`LocalDeclarationStatement`ノードに表示されます。 `VariableDeclaration`このノードには、 が次`VariableDeclarator`に、 を持ち、最後に`EqualsValueClause` `ObjectCreationExpression`. ノードの構文ビジュアライザー ツリーをクリックすると、エディター ウィンドウの構文が強調表示され、そのノードで表されるコードが表示されます。 SyntaxNode サブタイプの名前は、C# 文法で使用される名前と一致します。

## <a name="create-the-analyzer-project"></a>アナライザ プロジェクトの作成

メイン メニューの [**新** > **しい** > **プロジェクト**] をクリックします。 [**新しいプロジェクト**] ダイアログの左側のナビゲーション バーの **[C#** プロジェクト] で [**機能拡張**] を選択し、右側のウィンドウで **[コード修正を使用するアナライザー]** プロジェクト テンプレートを選択します。 名前を入力し、ダイアログを確認します。

テンプレートによって*DiagnosticAnalyzer.cs*ファイルが開かれます。 そのエディター バッファー タブを選択します。このファイルには、(Roslyn API 型) から派生するアナライザー クラス`DiagnosticAnalyzer`(プロジェクトに与えた名前から形成) があります。 新しいクラスには、`DiagnosticAnalyzerAttribute`コンパイラがアナライザーを検出して読み込むために、アナライザーが C# 言語に関連付けられており、宣言するクラスがあります。

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

C# コードを対象とする Visual Basic を使用してアナライザーを実装し、その逆も可能です。 アナライザーが 1 つの言語を対象とするか、またはその両方を対象とするかを選択することが、診断アナライザー属性でより重要です。 言語の詳細なモデリングを必要とする、より高度なアナライザーは、単一言語のみを対象とします。 たとえば、アナライザーで型名やパブリック メンバー名のみをチェックする場合は、Roslyn が提供する共通言語モデルを Visual Basic および C# で使用できる場合があります。 たとえば、FxCop はクラスが<xref:System.Runtime.Serialization.ISerializable>実装していることを警告しますが、クラスには<xref:System.SerializableAttribute>言語に依存しない属性を持たないので、Visual Basic と C# の両方のコードで動作します。

## <a name="initialize-the-analyzer"></a>アナライザーを初期化する

 メソッドを確認するには、クラス`DiagnosticAnalyzer`内で少し`Initialize`下にスクロールします。 コンパイラは、アナライザーをアクティブ化するときにこのメソッドを呼び出します。 このメソッドは、`AnalysisContext`アナライザーがコンテキスト情報を取得し、分析するコードの種類に応じてイベントのコールバックを登録できるようにするオブジェクトを受け取ります。

```csharp
public override void Initialize(AnalysisContext context) {}
```

このメソッドで新しい行を開き、「コンテキスト」と入力します。 をクリックして、IntelliSense のコンプリート リストを表示します。 完了リストには、さまざまな種類のイベントを処理`Register...`する方法が多数あることがわかります。 たとえば、最初のコードは、`RegisterCodeBlockAction`ブロックのコードを呼び戻します。 ブロックに登録すると、フィールドの初期化子、属性に指定された値、または省略可能なパラメーターの値のコードも呼び出されます。

別の例として`RegisterCompilationStartAction`、 は、コンパイルの開始時にコードを呼び出します。 たとえば、使用されるすべてのシンボルを収集するデータ構造を作成し、構文やシンボルに対してアナライザーが呼び出されるたびに、データ構造内の各位置に関する情報を保存できます。 コンパイル終了のために呼び戻された場合、保存したすべての場所を分析して、コードが各`using`ステートメントで使用するシンボルを報告できます。

**構文ビジュアライザー**を使用すると、コンパイラが ObjectCreationExpression を処理するときに呼び出されることを学習しました。 このコードを使用して、コールバックを設定します。

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

構文ノードに登録し、オブジェクト作成構文ノードのみを対象にフィルター処理します。 慣例により、アナライザーの作成者はアクションを登録するときにラムダを使用するため、アナライザーをステートレスに保つことができます。 Visual Studio の **[使用法から生成]** `AnalyzeObjectCreation`機能を使用して、メソッドを作成できます。 これにより、コンテキスト パラメーターの型も生成されます。

## <a name="set-properties-for-users-of-your-analyzer"></a>アナライザーのユーザーのプロパティを設定する

アナライザーが Visual Studio UI に適切に表示されるように、アナライザーを識別するために次のコード行を探して変更します。

```csharp
internal const string Category = "Naming";
```

`"Naming"` を `"API Guidance"` に変更します。

次に、**ソリューション エクスプローラ**を使用して、プロジェクト内の*Resources.resx*ファイルを見つけて開きます。 アナライザーやタイトルなどの説明を入力できます。ここでは、これらの`"Don't use ImmutableArray<T> constructor"`値をすべてに変更できます。 文字列 ({0}、{1}など) に文字列書式の引数を置き、後で`Diagnostic.Create()`呼び出すときに`params`渡す引数の配列を指定できます。

## <a name="analyze-an-object-creation-expression"></a>オブジェクト作成式の分析

この`AnalyzeObjectCreation`メソッドは、コード アナライザ フレームワークによって提供される異なる種類のコンテキストを受け取ります。 メソッド`Initialize`を`AnalysisContext`使用すると、アクション コールバックを登録してアナライザーを設定できます。 たとえば`SyntaxNodeAnalysisContext`、 には を渡`CancellationToken`すことができる が、 を渡すことができます。 ユーザーがエディタに入力を開始すると、Roslyn は、作業を保存し、パフォーマンスを向上させるために、実行中のアナライザーをキャンセルします。 別の例として、このコンテキストには、オブジェクト作成構文ノードを返す Node プロパティがあります。

構文ノード アクションをフィルター処理した型を想定できるノードを取得します。

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>アナライザーを初めて使用して Visual Studio を起動する

アナライザーをビルドして実行して Visual Studio を起動します **(F5**キーを押します)。 **ソリューション エクスプローラー**のスタートアップ プロジェクトは VSIX プロジェクトであるため、コードを実行するとコードと VSIX がビルドされ、その VSIX がインストールされた状態で Visual Studio が起動されます。 この方法で Visual Studio を起動すると、アナライザーのビルド中に Visual Studio の主な使用がテスト インスタンスの影響を受けないように、個別のレジストリ ハイブで起動します。 この方法を初めて起動すると、Visual Studio をインストールした後に最初に起動したときと同様の初期化が行われます。

コンソール プロジェクトを作成し、コンソール アプリケーション Main メソッドに配列コードを入力します。

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

変更できない NuGet`ImmutableArray`パッケージを取得し、コードに`using`ステートメントを追加する必要があるため、コードの行には波線が含まれています。 **ソリューション エクスプローラー**でプロジェクト ノードの右ポインター ボタンを押し **、[NuGet パッケージの管理**] を選択します。 NuGet マネージャーで、検索ボックスに「変更不可」と入力し、左側のウィンドウで項目**System.Collections.Immutable** **(Microsoft.Bcl.Immutable**を選択しないでください) を選択し、右側のウィンドウで **[インストール**] ボタンを押します。 パッケージをインストールすると、プロジェクト参照への参照が追加されます。

引き続き 赤い波線`ImmutableArray`が 表示されるので、その識別子にキャレットを置き **、Ctrl**+**キーを押します。** (ピリオド) をクリックして、推奨される修正メニューを表示し、`using`適切なステートメントを追加します。

**[すべて保存] と**[Visual Studio の 2 番目のインスタンスを閉じる] をクリックして、クリーンな状態にして続行します。

## <a name="finish-the-analyzer-using-edit-and-continue"></a>編集と続行を使用してアナライザを終了する

Visual Studio の最初のインスタンスで、最初の行にキャレット`AnalyzeObjectCreation`を付けて**F9**キーを押して、メソッドの先頭にブレークポイントを設定します。

**F5**を使用してアナライザーを再度起動し、Visual Studio の 2 番目のインスタンスで、前回作成したコンソール アプリケーションを再度開きます。

Roslyn コンパイラがオブジェクト作成式を見てアナライザーに呼び出されたため、ブレークポイントで Visual Studio の最初のインスタンスに戻ります。

**オブジェクト作成ノードを取得します。** **F10**キーを押`objectCreation`して変数を設定する行をステップ オーバーし、**イミディエイト ウィンドウ**で式`"objectCreation.ToString()"`を評価します。 変数が指す構文ノードは、目的のコード`"new ImmutableArray<int>()"`であることがわかります。

**T\>型オブジェクト<変更可能な配列を取得します。** 作成される型が ImmutableArray であるかどうかを確認する必要があります。 まず、この型を表すオブジェクトを取得します。 セマンティック モデルを使用して型をチェックし、正しい型を持っていることを確認し、 からの`ToString()`文字列を比較しないようにします。 関数の末尾に次のコード行を入力します。

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

メタデータ内のジェネリック型は、バックティック (') とジェネリック パラメーターの数で指定します。 あなたが見ていない理由です.メタデータ名の不\<変アレイ T>"。

セマンティック モデルには、シンボル、データ フロー、変数の有効期間などに関する質問をする、多くの便利な要素があります。Roslyn は、さまざまなエンジニアリング上の理由 (パフォーマンス、誤ったコードのモデリングなど) のために、構文ノードをセマンティック モデルから分離します。 正確な比較のために、コンパイル モデルで参照に含まれる情報を検索する必要があります。

エディター ウィンドウの左側にある黄色の実行ポインタをドラッグできます。 `objectCreation`変数を設定する行までドラッグし **、F10**を使用して新しいコード行をステップ オーバーします。 変数`immutableArrayOfType`の上にマウス ポインタを置くと、セマンティック モデルで正確な型が見つかったことがわかります。

**オブジェクト作成式の型を取得します。** "Type" は、この記事ではいくつかの方法で使用されていますが、これは "新しい Foo" 式がある場合は Foo のモデルを取得する必要があることを意味します。 オブジェクト作成式の型を取得して、それが ImmutableArray\<T>型かどうかを確認する必要があります。 セマンティック モデルをもう一度使用して、オブジェクト作成式の型シンボル (ImmutableArray) のシンボル情報を取得します。 関数の末尾に次のコード行を入力します。

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

アナライザーはエディタバッファ内の不完全なコードや正しくないコードを処理する必要があるため (たとえば、`using`ステートメントが欠落している場合など`symbolInfo`)、. `null` 分析を完了するには、シンボル情報オブジェクトから名前付き型 (INamedTypeSymbol) を取得する必要があります。

**[タイプ] を比較します。** 検索対象の T のオープン ジェネリック型があり、コード内の型は具象ジェネリック型であるため、その型の構築元 (オープン ジェネリック型) のシンボル情報をクエリし、その結果を と`immutableArrayOfTType`比較します。 メソッドの最後に次を入力します。

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**診断を報告します。** 診断の報告は非常に簡単です。 Initialize メソッドの前に定義されているプロジェクト テンプレートで作成された規則を使用します。 コード内のこのような状況はエラーであるため、Rule を初期化した行を変更して、(`DiagnosticSeverity.Warning`緑色の波線) を`DiagnosticSeverity.Error`(赤い波線) に置き換えることができます。 Rule の残りの部分は、チュートリアルの最初の近くで編集したリソースから初期化されます。 また、オブジェクト作成式の型指定の場所である波線の位置を報告する必要があります。 ブロックに次のコード`if`を入力します。

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

関数は次のようになります (形式が異なる可能性があります)。

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

ブレークポイントを削除して、アナライザーが動作していることを確認します (Visual Studio の最初のインスタンスに戻るのを停止します)。 実行ポインタをメソッドの先頭にドラッグし **、F5**キーを押して実行を続行します。 Visual Studio の 2 番目のインスタンスに戻ると、コンパイラはコードの再確認を開始し、アナライザーを呼び出します。 下に波線が表示されます`ImmutableType<int>`。

## <a name="adding-a-code-fix-for-the-code-issue"></a>コードの問題に対する "コード修正" を追加する

開始する前に、Visual Studio の 2 番目のインスタンスを閉じ、Visual Studio の最初のインスタンス (アナライザーを開発している場所) でデバッグを停止します。

**新しいクラスを追加します。** **ソリューション エクスプローラー**でプロジェクト ノードのショートカット メニュー (右のポインター ボタン) を使用し、新しい項目を追加することを選択します。 という`BuildCodeFixProvider`クラスを追加します。 このクラスは`CodeFixProvider`から派生する必要があり、 **Ctrl**+を使用する必要があります **。** (ピリオド) を指定すると、正しい`using`ステートメントを追加するコード修正が呼び出されます。 このクラスには`ExportCodeFixProvider`属性を付ける必要があり、`using``LanguageNames`列挙型を解決するためにステートメントを追加する必要があります。 次のコードを含むクラス ファイルが必要です。

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**派生メンバーをスタブアウトします。** 次に、エディタのキャレット`CodeFixProvider`を識別子に配置し **、Ctrl**+**キーを押します。** (ピリオド) を使用して、この抽象基本クラスの実装をスタブアウトします。 これにより、プロパティとメソッドが生成されます。

**プロパティを実装します。** プロパティの`FixableDiagnosticIds`本文に次の`get`コードを入力します。

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn は、単なる文字列であるこれらの識別子を照合することによって診断と修正をまとめます。 プロジェクト テンプレートによって診断 ID が生成され、変更は自由です。 プロパティのコードは、アナライザー クラスから ID を返すだけです。

**メソッドはコンテキストを受け取ります。** コード修正は複数の診断に適用される場合や、コード行に複数の問題が発生する可能性があるため、コンテキストは重要です。 「コンテキスト」と入力した場合。 メソッドの本文では、IntelliSense の入力候補リストに役立つメンバーが表示されます。 何かが修正をキャンセルしたいかどうかを確認できるキャンセルトークンメンバーがあります。 多数の有用なメンバーを持ち、プロジェクトとソリューション モデル オブジェクトに到達できるドキュメント メンバーがあります。 診断を報告したときに指定されたコードの場所の開始と終了である Span メンバーがあります。

**メソッドを非同期にします。** 最初に行う必要があるのは、生成されたメソッド宣言を`async`メソッドに修正することです。 抽象クラスの実装をスタブアウトするためのコード修正には、メソッドがを返す場合`async`でもキーワードは`Task`含みません。

**構文ツリーのルートを取得します。** コードを変更するには、コード修正によって行った変更を含む新しい構文ツリーを生成する必要があります。 を呼び`Document`出`GetSyntaxRootAsync`すコンテキストからの が必要です。 これは、ディスクからファイルを取得し、解析し、Roslyn コード モデルを構築するなど、構文ツリーを取得するための不明な作業があるため、非同期メソッドです。 Visual Studio UI は、この時間の間に`async`応答する必要があります。 メソッドのコード行を次のように置き換えます。

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**問題のあるノードを見つけます。** コンテキストの範囲を渡しますが、見つけたノードは変更する必要のあるコードではない可能性があります。 報告された診断では、型識別子 (波線が属していた場所) の範囲のみが提供されますが、`new`オブジェクト作成式全体を置き換える必要があります。 メソッドに次のコードを追加します (**および Ctrl**+**を使用します)。** にステートメントを`using`追加します`ObjectCreationExpressionSyntax`):

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**電球 UI のコード修正を登録します。** コード修正プログラムを登録すると、Roslyn は Visual Studio 電球 UI に自動的に接続します。 エンド ユーザーは、 **Ctrl を**+使用できることを確認**できます。** アナライザーが不正`ImmutableArray<T>`なコンストラクタを使用する波線を引くとき(ピリオド)。 コード修正プロバイダは問題が発生した場合にのみ実行されるため、探していたオブジェクト作成式があると仮定できます。 context パラメーターから、`RegisterCodeFixAsync`メソッドの最後に次のコードを追加することで、新しいコード修正を登録できます。

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

エディタのキャレットを識別子に配置し`CodeAction`、 **Ctrl**+を使用する必要**があります。** (ピリオド) をクリックして`using`、この型に対して適切なステートメントを追加します。

`ChangeToImmutableArrayEmpty`次に、エディタのキャレットを識別子に配置し、 **Ctrl**+を使用**します。** このメソッドスタブを生成します。

最後に追加したコード スニペットは、見つかった問題の種類`CodeAction`の診断 ID と a を渡すことによって、コード修正を登録します。 この例では、このコードで修正される診断 ID は 1 つしかないので、診断 ID 配列の最初の要素を渡すだけです。 `CodeAction`を作成するときに、電球 UI がコード修正の説明として使用するテキストを渡します。 また、キャンセルトークンを受け取り、新しいドキュメントを返す関数を渡します。 新しいドキュメントには、新しい構文ツリーがあり、 を呼び出`ImmutableArray.Empty`す修正プログラムが適用されたコードが含まれています。 このコード スニペットは、オブジェクト作成ノードとコンテキストのドキュメントを閉じることができるように、ラムダを使用します。

**新しい構文ツリーを構築します。** 先ほど`ChangeToImmutableArrayEmpty`生成したスタブのメソッドに、コード行を入力します。 `ImmutableArray<int>.Empty;` **構文ビジュアライザー**ツール ウィンドウをもう一度表示すると、この構文が SimpleMemberAccessExpression ノードであることがわかります。 このメソッドは、新しいドキュメントを構築して返す必要があります。

最初の`ChangeToImmutableArrayEmpty`変更は、コード`async`ジェネレーター`Task<Document>`がメソッドを非同期にする必要があるため、前に追加することです。

メソッドが次のようになるように、本体に次のコードを入力します。

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

識別子にエディタのキャ`SyntaxGenerator`レットを入れて、 **Ctrl**+**を使用する必要があります。** (ピリオド) をクリックして`using`、この型に対して適切なステートメントを追加します。

このコードでは`SyntaxGenerator`、 を使用して新しいコードを作成するのに便利な型です。 コードの問題があるドキュメントのジェネレーターを取得した後、アクセス`ChangeToImmutableArrayEmpty`する`MemberAccessExpression`メンバーを持つ型を渡し、メンバーの名前を文字列として渡す を呼び出します。

次に、メソッドはドキュメントのルートを取得し、一般的なケースでは任意の処理を伴う可能性があるため、コードはこの呼び出しを待機し、キャンセル トークンを渡します。 Roslyn コード モデルは、.NET 文字列を操作するのと同じように、変更できません。文字列を更新すると、新しい文字列オブジェクトが返されます。 を呼び`ReplaceNode`出すと、新しいルート ノードが返されます。 構文ツリーの大部分は共有されますが (変更できないため)、`objectCreation``memberAccess`ノードはノードに置き換えられ、構文ツリーのルートまでのすべての親ノードも置き換えられます。

## <a name="try-your-code-fix"></a>コード修正を試す

**F5 キー**を押して、Visual Studio の 2 番目のインスタンスでアナライザーを実行できるようになりました。 以前に使用したコンソール プロジェクトを開きます。 これで、新しいオブジェクト作成式が の`ImmutableArray<int>`場所に電球が表示されます。 Ctrl キーを押すと **、 Ctrl キーを****押す**+ (ピリオド)、コードの修正が表示され、電球 UI で自動的に生成されたコードの違いプレビューが表示されます。 ロスリンはあなたのためにこれを作成します。

**プロのヒント:** Visual Studio の 2 番目のインスタンスを起動しても、コード修正で電球が表示されない場合は、Visual Studio コンポーネント キャッシュをクリアする必要があります。 キャッシュをクリアすると、Visual Studio はコンポーネントを再調査する必要があるため、Visual Studio は最新のコンポーネントを選択する必要があります。 最初に、Visual Studio の 2 番目のインスタンスをシャットダウンします。 次に、**エクスプローラー**で *、%LOCALAPPDATA%\マイクロソフト\VisualStudio\16.0Roslyn\\*に移動します。 (「16.0」は、バージョンからバージョンに変更されます。サブディレクトリを削除*します*。

## <a name="talk-video-and-finish-code-project"></a>ビデオを話し、コードプロジェクトを終了する

この例は、[この講演](https://channel9.msdn.com/events/Build/2015/3-725)で詳しく説明されています。 この講演では、作業アナライザーを紹介し、それを構築する方法について説明します。

完成したコードは[、こちらからご覧いただけます](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)。 サブ フォルダー *DoNotUseImimtableArrayCollectionInitializer*と*DoNotUseImmutableArrayCtor*はそれぞれ、問題を見つけるための C# ファイルと、Visual Studio 電球 UI に表示されるコード修正を実装する C# ファイルを持っています。 完成したコードは、型\<オブジェクトを何度も何度も取得しないように、もう少し抽象化>。 このクラスは、入れ子になった登録済みアクションを使用して、サブアクション (オブジェクトの作成の分析およびコレクション初期化の分析) が実行されるたびに使用できるコンテキストに型オブジェクトを保存します。

## <a name="see-also"></a>関連項目

* [\\\ビルド2015トーク](https://channel9.msdn.com/events/Build/2015/3-725)
* [GitHub で完了したコード](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [GitHub のいくつかの例は、3 種類のアナライザーにグループ化されています。](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [GitHub OSS サイトのその他のドキュメント](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [GitHub のロズリン アナライザーで実装された FxCop ルール](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
