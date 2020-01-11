---
title: コード カバレッジを使用した、テストされるプロジェクトのコード割合の確認 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- code coverage
ms.assetid: 800fc739-acd2-4242-84cb-1d83b4d82cf9
caps.latest.revision: 38
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 737311167fc1f444d5c0f8a5d2c27e2fe321da75
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851249"
---
# <a name="using-code-coverage-to-determine-how-much-code-is-being-tested"></a>コード カバレッジを使用した、テストされるプロジェクトのコード割合の確認
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

単体テストなどのコード化されたテストによって実際にテストされるプロジェクトのコードの割合を調べるには、Visual Studio のコード カバレッジ機能を使用できます。 バグから効果的に保護するには、コードの大部分を "カバー" するようにテストを実行する必要があります。

 コード カバレッジ分析は、マネージド (CLI) コードにもアンマネージド (ネイティブ) コードにも適用できます。

 コード カバレッジは、テスト エクスプローラーを使用してテスト メソッドを実行する場合のオプションです。 結果テーブルには、各アセンブリ、クラス、およびメソッドで実行されたコードの割合が表示されます。 また、ソース エディターには、どのコードがテストされたかが表示されます。

 ![コードカバレッジの結果と色分け](../test/media/codecoverage1.png "CodeCoverage1")

 **Requirements**

- Visual Studio Enterprise

### <a name="to-analyze-code-coverage-on-unit-tests-in-test-explorer"></a>テスト エクスプローラーで単体テストのコード カバレッジを分析するには

1. **[テスト]** メニューの **[コード カバレッジの分析]** を選択します。

2. 実行された行を表示するには、![[コード カバレッジの色分けを表示] アイコン](../test/media/codecoverage-showcoloringicon.png "CodeCoverage-ShowColoringIcon") **[コード カバレッジの色分けを表示]** を選択します。

     色を変更したり太字を使用したりする場合は、 **[ツール]** 、 **[オプション]** 、 **[環境]** 、 **[フォントおよび色]** 、 **[設定の表示: テキスト エディター]** の順に選択します。 **[表示項目]** でカバレッジ項目を調整します。

3. 結果が低カバレッジを示していた場合は、コードのどの部分が実行されていないかを調べ、その部分をカバーするテストをさらに作成します。 開発チームは、通常、約 80% のコード カバレッジを目標にします。 状況によっては、より低いカバレッジでも許容されます。 たとえば、一部のコードが標準テンプレートから生成される場合は、より低いカバレッジでも許容されます。

> [!TIP]
> 正確な結果を得るには、次の点に注意します。
>
> - コンパイラの最適化がオフになっていることを確認します。
>
>   アンマネージ (ネイティブ) コードを操作している場合は、デバッグ ビルドを使用します。
>   - 各アセンブリのシンボル (.pdb) ファイルが生成されていることを確認します。
>
>   期待した結果が得られない場合は、「[トラブルシューティング コード カバレッジ](../test/troubleshooting-code-coverage.md)」を参照してください。 を確認しています。 コードを更新した後は、コード カバレッジを忘れずに再度実行します。 コードの変更後やテストの実行後に、カバレッジ結果とコードの色分けは自動的には更新されません。

## <a name="reporting-in-blocks-or-lines"></a>ブロック単位または行単位で報告する
 コード カバレッジは、*ブロック*単位でカウントされます。 ブロックは、エントリ ポイントと終了ポイントを 1 つだけ持つ、コードの部分です。  プログラムの制御フローがテストの実行中にブロックを通過すると、そのブロックはカバー済みとしてカウントされます。 ブロックが使用された回数は、結果には影響しません。

 テーブル ヘッダーで **[列の追加と削除]** を選択して、結果を行単位で表示することもできます。 テストの実行がコードのいずれかの行内のすべてのコード ブロックを処理すると、1 行としてカウントされます。 実行されたコード ブロックと実行されなかったコード ブロックが行内に含まれている場合は、部分行としてカウントされます。

 行単位での割合の方が、ソース コードで見ることができるフラグメントのサイズに正確に対応するため、一部のユーザーは行単位でのカウントを選びます。 計算の長いブロックは、複数の行にわたっていても、1 つのブロックとしてカウントされます。

## <a name="managing-code-coverage-results"></a>コード カバレッジの結果を管理する
 [コード カバレッジの結果] ウィンドウには、通常、最新の実行の結果が表示されます。 結果は、テスト データを変更したり、テストの一部だけを実行したりすると、そのたびに異なります。

 コード カバレッジ ウィンドウを使用して、以前の結果や、他のコンピューター上で取得した結果を表示することもできます。

 いくつかの実行 (たとえば、異なるテスト データを使用した実行) の結果をマージできます。

- **以前の結果のセットを表示するには**、それをドロップダウン メニューから選択します。 メニューには一時的な一覧が表示され、新しいソリューションを開くとクリアされます。

- **以前のセッションの結果を表示するには**、 **[コード カバレッジの結果のインポート]** を選択し、ソリューションの TestResults フォルダーに移動して、.coverage ファイルをインポートします。

     .coverage ファイルの生成後、ソース コードを変更した場合は、カバレッジの色分けが正しくない場合があります。

- **結果をテキストとして読みやすくするには**、 **[コード カバレッジの結果のエクスポート]** を選択します。 他のツールで処理したり電子メールで簡単に送信したりすることができる、読める形式の .coveragexml ファイルが生成されます。

- **結果を他のユーザーに送信するには**、.coverage ファイルまたはエクスポートされた .coveragexml ファイルを送信します。 受け取ったユーザーは、ファイルをインポートできます。 同じバージョンのソース コードを持っていれば、カバレッジの色分けも表示できます。

## <a name="merging-results-from-different-runs"></a>さまざまな実行による結果をマージする
 状況によっては、テスト データに応じて、コード内の異なるブロックが使用されます。 そのため、異なるテスト実行の結果を結合する必要がある場合があります。

 たとえば、入力が "2" のテストを実行したときに、特定の関数の 50% がカバーされるとします。 入力を "-2" にして再度テストを実行すると、カバレッジの色分けビューで、関数の残りの 50% がカバーされていることがわかるとします。 ここで、2 つのテスト実行の結果をマージすると、レポートやカバレッジの色分けビューで、関数の 100% がカバーされたことが表示されます。

 そのためには、![[コード カバレッジ] ウィンドウの [マージ] ボタンのアイコン](../test/media/codecoverage-mergeicon.png "CodeCoverage-MergeIcon") **[コード カバレッジの結果のマージ]** を使用します。 最新の実行またはインポートされた結果を任意の組み合わせで選択できます。 エクスポートされた結果を結合する場合は、まず、それらをインポートする必要があります。

 マージ操作の結果を保存するには、 **[コード カバレッジの結果のエクスポート]** を使用します。

### <a name="limitations-in-merging"></a>マージの制限事項

- バージョンが異なるコードのカバレッジ データをマージすると、結果は個別に表示され、結合はされません。 完全に結合された結果を取得するには、同じビルドのコードを使用し、テスト データだけを変更します。

- エクスポートしてからインポートされた結果ファイルをマージした場合は、行単位の結果のみを表示でき、ブロック単位の結果は表示できません。 行データを表示するには、 **[列の追加と削除]** コマンドを使用します。

- ASP.NET プロジェクトのテスト結果をマージした場合は、個別のテストの結果は表示されますが、結合された結果は表示されません。 このようになるのは、ASP.NET の成果物自体だけです。他のアセンブリの結果は結合されます。

## <a name="excluding-elements-from-the-code-coverage-results"></a>コード カバレッジの結果から要素を除外する
 コードがテキスト テンプレートから生成された場合のように、コード内の特定の要素をカバレッジのスコアから除外する必要があることがあります。 その場合は、コード要素であるクラス、構造体、メソッド、プロパティ、プロパティ set または get アクセス操作子、およびイベントに、属性 `System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverage` を追加します。 クラスを除外しても、派生クラスは除外されないことに注意してください。

 例:

```csharp

using System.Diagnostics.CodeAnalysis;
...
public class ExampleClass1
{
    [ExcludeFromCodeCoverage]
    void ExampleMethod() {...}

    [ExcludeFromCodeCoverage] // exclude property
    int ExampleProperty1
    { get {...} set{...}}

    int ExampleProperty2
    {
        get
        {
            ...
        }
        [ExcludeFromCodeCoverage] // exclude setter
        set
        {
            ...
        }
    }

}
[ExcludeFromCodeCoverage]
class ExampleClass2 { ... }

```

```vb
Imports System.Diagnostics.CodeAnalysis

Class ExampleClass1
    <ExcludeFromCodeCoverage()>
    Public Sub ExampleSub1()
        ...
    End Sub

    ' Exclude property
    < ExcludeFromCodeCoverage()>
    Property ExampleProperty1 As Integer
        ...
    End Property

    ' Exclude setter
    Property ExampleProperty2 As Integer
        Get
            ...
        End Get
        <ExcludeFromCodeCoverage()>
        Set(ByVal value As Integer)
            ...
        End Set
    End Property
End Class

<ExcludeFromCodeCoverage()>
Class ExampleClass2
...
End Class

```

```cpp#
// A .cpp file compiled as managed (CLI) code.
using namespace System::Diagnostics::CodeAnalysis;
...
public ref class ExampleClass1
{
  public:
    [ExcludeFromCodeCoverage]
    void ExampleFunction1() { ... }

    [ExcludeFromCodeCoverage]
    property int ExampleProperty2 {...}

    property int ExampleProperty2 {
      int get() { ... }
     [ExcludeFromCodeCoverage]
      void set(int value) { ...  }
   }

}

[ExcludeFromCodeCoverage]
public ref class ExampleClass2
{ ... }

```

### <a name="excluding-elements-in-native-c-code"></a>ネイティブ C++ コード内の要素を除外する
 C++ コードでアンマネージ (ネイティブ) 要素を除外するには:

```cpp

#include <CodeCoverage\CodeCoverage.h>
...

// Exclusions must be compiled as unmanaged (native):
#pragma managed(push, off)

// Exclude a particular function:
ExcludeFromCodeCoverage(Exclusion1, L"MyNamespace::MyClass::MyFunction");

// Exclude all the functions in a particular class:
ExcludeFromCodeCoverage(Exclusion2, L"MyNamespace::MyClass2::*");

// Exclude all the functions generated from a particular template:
ExcludeFromCodeCoverage(Exclusion3, L"*::MyFunction<*>");

// Exclude all the code from a particular .cpp file:
ExcludeSourceFromCodeCoverage(Exclusion4, L"*\\unittest1.cpp");

// After setting exclusions, restore the previous managed/unmanaged state:
#pragma managed(pop)

```

 以下のマクロを使用します。

 `ExcludeFromCodeCoverage(` *ExclusionName* `, L"` *FunctionName* `");`

 `ExcludeSourceFromCodeCoverage(` *ExclusionName* `, L"` *sourcefilepath* `");`

- *ExclusionName* は任意の一意の名前です。

- *FunctionName* は完全修飾関数名です。 ワイルドカードを含めることができます。 たとえば、クラスのすべての関数を除外するには、`MyNamespace::MyClass::*` と記述します。

- *SourceFilePath* は .cpp ファイルのローカル パスまたは UNC パスです。 ワイルドカードを含めることができます。 たとえば、`\\MyComputer\Source\UnitTests\*.cpp` と記述すると、特定のディレクトリ内のすべてのファイルが除外されます。

- `#include <CodeCoverage\CodeCoverage.h>`

- 除外マクロの呼び出しは、いずれかの名前空間またはクラス内ではなく、グローバル名前空間に配置します。

- 除外は単体テスト コード ファイルまたはアプリケーション コード ファイル内に配置できます。

- 除外は、コンパイラ オプションを設定するか、`#pragma managed(off)` を使用して、アンマネージ (ネイティブ) コードとしてコンパイルする必要があります。

> [!NOTE]
> C++/CLI コード内の関数を除外するには、関数に `[System::Diagnostics::CodeAnalysis::ExcludeFromCodeCoverage]` 属性を適用します。 これは、C# の場合と同じです。

### <a name="including-or-excluding-additional-elements"></a>追加の要素を含めるか除外する
 コード カバレッジ分析の対象となるのは、読み込まれ、.dll または .exe ファイルと同じディレクトリ内の .pdb ファイルを利用できるアセンブリだけです。 そのため、状況によっては、適切な .pdb ファイルのコピーを取得することによって、対象となるアセンブリのセットを拡張できます。

 .runsettings ファイルを記述すると、コード カバレッジ分析の対象としてどのアセンブリと要素を選択するかをより詳細に制御できます。 たとえば、クラスに属性を追加せずに、特定の種類のアセンブリを除外できます。 詳細については、「[コード カバレッジ分析のカスタマイズ](../test/customizing-code-coverage-analysis.md)」を参照してください。

## <a name="analyzing-code-coverage-in-the-build-service"></a>ビルド サービスでコード カバレッジを分析する
 コードをチェックインすると、テストがビルド サーバー上で、他のチーム メンバーによる他のすべてのテストと共に実行されます。 (まだ設定していない場合は、「[ビルドプロセスでのテストの実行](https://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38)」を参照してください)。ビルドサービスでコードカバレッジを分析すると便利です。これにより、プロジェクト全体のカバレッジを最新で包括的に把握できます。 これには、自動化されたシステム テストと、通常は開発用コンピューターでは実行しない、その他のコード化されたテストも含まれます。

1. チーム エクスプローラーで、 **[ビルド]** を開き、ビルド定義を追加または編集します。

2. **[プロセス]** ページで **[自動テスト]** 、 **[テスト ソース]** 、 **[実行設定]** の順に展開します。 **[実行設定の種類]** を **[コード カバレッジの有効化]** に設定します。

    複数のテスト ソース定義がある場合は、各定義に対してこの手順を繰り返します。

   - <em>ただし、* *[実行設定の種類]</em>* というフィールドはありません。*

      **[自動テスト]** の下の **[テスト アセンブリ]** を選択し、行の末尾の省略記号 ( **[...]** ) ボタンを選択します。 **[テストの実行の追加と編集]** ダイアログ ボックスで、 **[テスト ランナー]** の下の **[Visual Studio テスト ランナー]** を選択します。

   ![コードカバレッジのビルド定義の設定](../test/media/codecoverage-plaincc.png "CodeCoverage-plainCC")

   ビルドの実行後、コード カバレッジの結果はテスト実行にアタッチされ、ビルドの概要に表示されます。

## <a name="analyzing-code-coverage-in-a-command-line"></a>コマンド ラインでコード カバレッジを分析する
 コマンド ラインからテストを実行するには、vstest.console.exe を使用します。 コード カバレッジは、このユーティリティのオプションです。 詳細については、「[VSTest.Console.exe のコマンド ライン オプション](https://msdn.microsoft.com/library/52e1689d-b1a8-4589-bd98-99a55acd0a11)」を参照してください。

1. Visual Studio 開発者コマンド プロンプトを起動します。

     Windows の **[スタート]** メニューで **[すべてのプログラム]** 、 **[Microsoft Visual Studio]** 、 **[Visual Studio Tools]** 、 **[開発者コマンド プロンプト]** の順に選択します。

2. 実行:

     `vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage`

## <a name="troubleshooting"></a>トラブルシューティング
 コード カバレッジの結果が表示されない場合は、「[トラブルシューティング コード カバレッジ](../test/troubleshooting-code-coverage.md)」を参照してください。

## <a name="external-resources"></a>外部リソース

### <a name="guidance"></a>ガイダンス
 [Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 2 章: 単体テスト: 内部のテスト](https://msdn.microsoft.com/library/jj159340.aspx)

## <a name="see-also"></a>参照
 [コードカバレッジ分析のカスタマイズ](../test/customizing-code-coverage-analysis.md)コード[カバレッジ](../test/troubleshooting-code-coverage.md)[の単体テストコードのテスト](../test/unit-test-your-code.md)
