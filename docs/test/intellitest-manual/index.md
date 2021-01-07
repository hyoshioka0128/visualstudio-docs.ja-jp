---
title: 概要 | Microsoft IntelliTest 開発者テスト ツール
description: IntelliTest が自動化された透過的なテスト アプローチを使用する方法について説明します。IntelliTest は、.NET コードの候補となるテスト スイートを生成できます。
ms.custom: SEO-VS-2020
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Visual Studio IntelliTest developer testing tool
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 6853ef6040df943ac3050621a5b3a2528d599d9f
ms.sourcegitcommit: 4e28314dc2be59b4c5fd44545c0653f625e74489
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/23/2020
ms.locfileid: "97756618"
---
# <a name="overview-of-microsoft-intellitest"></a>Microsoft IntelliTest の概要

IntelliTest は早い段階でバグを発見することができ、テストのメンテナンス コストを削減します。 自動化された透過的なテスト アプローチを使用することで、IntelliTest は .NET コードのテストの候補スイートを生成できます。 テスト スイートの生成は、指定する *正確性プロパティ* によってより細かく指示することができます。 IntelliTest はテスト対象のコードの進化に伴って、テスト スイートを自動的にさらに進化させます。

> [!NOTE]
> IntelliTest は Enterprise Edition でのみ使用できます。 これは、.NET Framework を対象とする C# コードに対してサポートされています。 .NET Core と .NET Standard は現在サポートされていません。

**特性のテスト** IntelliTest では、従来の単体テストのスイートの観点から、コードの動作を決定することができます。
このようなテスト スイートは、レガシ コードや馴染みのないコードのリファクタリングに伴う複雑さへの取り組みの基盤を形成する回帰スイートとして使用できます。

**ガイドによるテスト入力の生成** IntelliTest はオープン コード分析と制約解決のアプローチを使用して、正確なテスト入力値を自動的に生成します。通常、ユーザーの介入は必要ありません。 複雑なオブジェクトの種類に対しては、ファクトリを自動的に生成します。 要件に合わせてファクトリを拡張および構成して、テスト入力の生成を指示できます。 コードでアサーションとして指定した正確性プロパティも、テスト入力生成をさらに指示するために自動的に使用されます。

**IDE の統合** IntelliTest は、Visual Studio IDE に完全に統合されています。 テスト スイートの生成中に収集されたすべての情報 (自動的に生成された入力、コードからの出力、生成されたテスト ケース、およびその成功または失敗のステータスなど) は、Visual Studio IDE 内に表示されます。 Visual Studio IDE を離れることなく、コードの修正と IntelliTest の再実行を簡単に反復することができます。
テストは単体テスト プロジェクトとしてソリューションに保存でき、保存後は Visual Studio テスト エクスプ ローラーで自動的に検出されます。

**既存のテスト手法の補完** IntelliTest を使用して、既に従っている既存のテスト手法を補完します。

テストする場合:

* プリミティブ データ、またはプリミティブ データの配列に対するアルゴリズム:
  * [パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)を記述する
* コンパイラなどの複雑なデータに対するアルゴリズム:
  * まず、IntelliTest でデータの抽象表現を生成してから、それをアルゴリズムにフィードする
  * IntelliTest で[カスタム オブジェクトの作成](input-generation.md#objects)とデータの不変性を使用してインスタンスを構築してから、アルゴリズムを呼び出す
* データ コンテナー:
  * [パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)を記述する
  * IntelliTest で[カスタム オブジェクトの作成](input-generation.md#objects)とデータの不変性を使用してインスタンスを構築してから、コンテナーのメソッドを呼び出し、不変性を再チェックする
  * パラメーター値に応じて、実装の異なるメソッドを呼び出す[パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)を記述する
* 既存のコード ベース:
  * Visual Studio の IntelliTest ウィザードを使用して、[パラメーター化した単体テスト (PUT)](test-generation.md#parameterized-unit-testing) のセットを生成して開始する

## <a name="the-hello-world-of-intellitest"></a>IntelliTest の Hello World

IntelliTest はテスト済みのプログラムに関連する入力を検索します。つまり、これを使用して有名な **Hello World!** 文字列を生成できます。 これは、C# MSTest ベースのテスト プロジェクトを作成し、**Microsoft.Pex.Framework** への参照を追加していることを前提としています。 別のテスト フレームワークを使用している場合は、C# クラス ライブラリを作成し、プロジェクトの設定方法に関するテスト フレームワークのドキュメントを参照してください。

次の例は、**value** という名前のパラメーターで 2 つの制約を作成して、IntelliTest が必要な文字列を生成できるようにします。

```csharp
using System;
using Microsoft.Pex.Framework;
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public partial class HelloWorldTest {
    [PexMethod]
    public void HelloWorld([PexAssumeNotNull]string value) {
        if (value.StartsWith("Hello")
            && value.EndsWith("World!")
            && value.Contains(" "))
            throw new Exception("found it!");
    }
}
```

コンパイルして実行すると、IntelliTest は次のようなテストのセットを生成します。

1. ""
2. "\0\0\0\0\0"
3. "Hello"
4. "\0\0\0\0\0\0"
5. "Hello\0"
6. "Hello\0\0"
7. "Hello\0World!"
8. "Hello World!"

> [!NOTE]
> ビルドの問題については、Microsoft.VisualStudio.TestPlatform.TestFramework と Microsoft.VisualStudio.TestPlatform.TestFramework.Extensions の参照を Microsoft.VisualStudio.QualityTools.UnitTestFramework への参照に置き換えてみてください。

生成されたテストが保存される場所については、「[IntelliTest でのコードの単体テストの生成](../../test/generate-unit-tests-for-your-code-with-intellitest.md)」を参照してください。 生成されたテスト コードには、次のコードのようなテストを含める必要があります。

```csharp
[TestMethod]
[PexGeneratedBy(typeof(global::HelloWorldTest))]
[PexRaisedException(typeof(Exception))]
public void HelloWorldThrowsException167()
{
    this.HelloWorld("Hello World!");
}
```

とても簡単ですね。

その他のリソース:
  * [Channel 9 ビデオ](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Intellitest)を見る
  * この [MSDN マガジンに記載されている概要](/archive/msdn-magazine/2015/february/visual-studio-2015-build-better-software-with-smart-unit-tests)を読む

## <a name="important-attributes"></a>重要な属性

* [PexClass](attribute-glossary.md#pexclass): **PUT** を含む型をマークします。
* [PexMethod](attribute-glossary.md#pexmethod): **PUT** をマークします。
* [PexAssumeNotNull](attribute-glossary.md#pexassumenotnull): null 以外のパラメーターをマークします。

```csharp
using Microsoft.Pex.Framework;

[..., PexClass(typeof(Foo))]
public partial class FooTest {
    [PexMethod]
    public void Bar([PexAssumeNotNull]Foo target, int i) {
        target.Bar(i);
    }
}
```

* [PexAssemblyUnderTest](attribute-glossary.md#pexassemblyundertest): テスト プロジェクトをプロジェクトにバインドします。
* [PexInstrumentAssembly](attribute-glossary.md#pexinstrumentassemblyattribute): インストルメント化するアセンブリを指定します。

```csharp
[assembly: PexAssemblyUnderTest("MyAssembly")] // also instruments "MyAssembly"
[assembly: PexInstrumentAssembly("Lib")]
```

## <a name="important-static-helper-classes"></a><a name="helper-classes"></a> 重要な静的ヘルパー クラス

* [PexAssume](static-helper-classes.md#pexassume): 前提事項 (入力フィルター) を評価します。
* [PexAssert](static-helper-classes.md#pexassert): アサーションを評価します。
* [PexChoose](static-helper-classes.md#pexchoose): 新しい選択項目 (追加入力) を生成します。
* [PexObserve](static-helper-classes.md#pexobserve): ライブ値を生成されたテストに記録します。

```csharp
[PexMethod]
void StaticHelpers(Foo target) {
    PexAssume.IsNotNull(target);

    int i = PexChoose.Value<int>("i");
    string result = target.Bar(i);

    PexObserve.ValueForViewing<string>("result", result);
    PexAssert.IsNotNull(result);
}
```

## <a name="limitations"></a>制限事項

このセクションでは、IntelliTest の制限事項について説明します。

* [非決定論的](#nondeterminism)
* [コンカレンシー](#concurrency)
* [ネイティブ .NET コード](#native-code)
* [プラットフォーム](#platform)
* [Language](#language)
* [シンボリック推論](#symbolic-reasoning)
* [スタック トレース](#incorrect-stack-traces)

### <a name="nondeterminism"></a>非決定論的

IntelliTest は、分析対象のプログラムが決定論的であると仮定します。 そうでない場合、IntelliTest は探索の範囲に達するまでサイクルを繰り返します。

プログラムが IntelliTest が制御できない入力に依存している場合、IntelliTest はそのプログラムを非決定論的と見なします。

IntelliTest は、[パラメーター化した単体テスト](test-generation.md#parameterized-unit-testing)に提供された入力と、[PexChoose](static-helper-classes.md#pexchoose) から取得された入力を制御します。
その意味で、アンマネージ コードまたはインストルメント化されていないコードへの呼び出しの結果も、インストルメント化されたプログラムの "入力" として見なされますが、IntelliTest はそれらを制御できません。 プログラムの制御フローがこれらの外部ソースからの特定の値に依存している場合、IntelliTest はれまでにカバーされていない領域に向かってプログラムを "誘導" することはできません。

さらに、プログラムの再実行時に外部ソースからの値が変わる場合は、そのプログラムは非決定論的と見なされます。 このような場合、IntelliTest はプログラムの実行に対する制御を失い、検索が非効率的になります。

これが発生しても、はっきりとわからない場合があります。 次に例を示します。

* **GetHashCode()** メソッドの結果は、アンマネージ コードによって提供され、予測できません。
* **System.Random** クラスは、現在のシステム時刻を使用して正確にランダムな値を提供します。
* **System.DateTime** クラスは、IntelliTest の制御下にない現在の時刻を提供します。

### <a name="concurrency"></a>コンカレンシー

IntelliTest はマルチスレッド プログラムを処理しません。

### <a name="native-code"></a>[ネイティブ コード]

IntelliTest は、**P/Invoke** を通じて呼び出される x86 命令などのネイティブ コードを理解しません。 これらの呼び出しを[制約ソルバー](input-generation.md#constraint-solver)に渡すことができる制約に変換する方法もわかりません。
.NET コードの場合でも、分析できるのはインストルメント化されたコードのみです。 IntelliTest は、リフレクション ライブラリを含む **mscorlib** の特定の部分をインストルメント化できません。 **DynamicMethod** はインストルメント化できません。

提案される回避策は、動的アセンブリ内でこのようなメソッドが配置されている種類のテスト モードを持つことです。 ただし、一部のメソッドがインストルメント化されない場合でも、IntelliTest はできるだけ多くのインストルメント化されたコードをカバーしようとします。

### <a name="platform"></a>プラットフォーム

IntelliTest は、X86、32 ビットの .NETframework でのみサポートされます。

### <a name="language"></a>言語

原則として、IntelliTest は .NET 言語で記述された任意の .NET プログラムを分析できますが、 Visual Studio では、C# のみサポートします。

### <a name="symbolic-reasoning"></a>シンボリック推論

IntelliTest は自動[制約ソルバー](input-generation.md#constraint-solver)を使用して、テストとテスト対象のプログラムに関連する値を判断します。 ただし、制約ソルバーの機能は、今までそうだったように、限定されており、これは今後も変わらないでしょう。

### <a name="incorrect-stack-traces"></a>スタック トレースの誤り

IntelliTest はインストルメント化された各メソッドで "rethrow" 例外をキャッチするため、スタック トレースの行番号は正しくなくなります。 これは "rethrow" 命令の設計による制限です。

## <a name="further-reading"></a>関連項目

* [初心者向けのブログ記事](https://devblogs.microsoft.com/devops/introducing-smart-unit-tests/)
* [IntelliTest でのコードの単体テストの生成](../../test/generate-unit-tests-for-your-code-with-intellitest.md)