---
title: C/C++ 用の単体テストの記述
description: CTest、Boost.Test、Google Test など、さまざまなテスト フレームワークを使用し、Visual Studio で C++ 単体テストを記述します。
ms.date: 09/27/2019
ms.topic: conceptual
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: 69b4f38ae43bacd5324b30a3970047b39c32fe99
ms.sourcegitcommit: 669fc9e397476d7a1d2cda5999710d415f7d6e4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74688860"
---
# <a name="write-unit-tests-for-cc-in-visual-studio"></a>Visual Studio で C/C++ 用の単体テストを作成する

他の言語と同じように、C++ についても、 **[テスト エクスプローラー]** ウィンドウを使って単体テストを作成して実行できます。 **テスト エクスプローラー**の使い方については、「[テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)」をご覧ください。

> [!NOTE]
> Live Unit Testing、コード化された UI テスト、IntelliTest などの一部の機能は、C++ についてはサポートされていません。

Visual Studio には次の C++ テスト フレームワークが含まれており、追加のダウンロードは必要ありません。

- C++ 用の Microsoft 単体テスト フレームワーク
- Google Test
- Boost.Test
- CTest

インストールされているフレームワークに加えて、Visual Studio 内で使いたいどのようなフレームワークについても、独自のテスト アダプターを作成できます。 テスト アダプターは、単体テストを **[テスト エクスプローラー]** ウィンドウと統合できます。 [Visual Studio Marketplace](https://marketplace.visualstudio.com) では複数のサードパーティ製アダプターを利用できます。 詳細については、「[サードパーティ製の単体テスト フレームワークをインストールする](install-third-party-unit-test-frameworks.md)」をご覧ください。

**Visual Studio 2017 以降 (Professional および Enterprise)**

C++ 単体テスト プロジェクトでは [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md) がサポートされています。

**Visual Studio 2017 以降 (すべてのエディション)** :

- **Google Test アダプター**は、**C++ によるデスクトップ開発**ワークロードの既定のコンポーネントとして含まれます。 このアダプターには、**ソリューション エクスプローラー**のソリューション ノードの **[新しいプロジェクトの追加]** 右クリック メニューでソリューションに追加できるプロジェクト テンプレートと、 **[ツール]**  >  **[オプション]** で構成できるオプションがあります。 詳細については、[Visual Studio での Google Test の使用](how-to-use-google-test-for-cpp.md)に関する記事をご覧ください。

- **Boost.Test** は、**C++ によるデスクトップ開発**ワークロードの既定のコンポーネントとして含まれます。 **テスト エクスプローラー**とは統合されていますが、現時点ではプロジェクト テンプレートがないので、手動で構成する必要があります。 詳細については、[Visual Studio での Boost.Test の使用](how-to-use-boost-test-for-cpp.md)に関する記事をご覧ください。

- **CTest** のサポートは、**C++ によるデスクトップ開発**ワークロードの一部である **C++ CMake ツール** コンポーネントで組み込まれます。 ただし、CTest と**テスト エクスプローラー**の統合はまだ完全ではありません。 詳細については、[Visual Studio での CTest の使用](how-to-use-ctest-for-cpp.md)に関する記事をご覧ください。

**Visual Studio 2015 以前**

Google Test アダプターと Boost.Test アダプターは、それぞれ、Visual Studio Marketplace の「[Test Adapter for Boost.Test](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforBoostTest)」(Boost.Test 用テスト アダプター) および「[Test Adapter for Google Test](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforGoogleTest)」(Google Test 用テスト アダプター) でダウンロードできます。

## <a name="basic-test-workflow"></a>テストの基本的なワークフロー

以下のセクションでは、C++ の単体テストを始めるための基本的な手順を示します。 基本的な構成は、Microsoft と Google どちらのテスト フレームワークでもよく似ています。 Boost.Test では、テスト プロジェクトを手動で作成することが必要です。

::: moniker range="vs-2019"

### <a name="create-a-test-project-in-visual-studio-2019"></a>Visual Studio 2019 でテスト プロジェクトを作成する

テスト対象のコードと同じソリューション内にある 1 つまたは複数のテスト プロジェクトでテストを実行します。 既存のソリューションに新しいテスト プロジェクトを追加するには、**ソリューション エクスプローラー**でソリューション ノードを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** の順に選びます。 **[言語]** を C++ に設定し、検索ボックスに "test" と入力します。 次の図は、**C++ によるデスクトップ開発**ワークロードと **UWP 開発**ワークロードがインストールされている場合に選ぶことができるテスト プロジェクトです。

![Visual Studio 2019 の C++ テスト プロジェクト](media/vs-2019/cpp-new-test-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

### <a name="create-a-test-project-in-visual-studio-2017"></a>Visual Studio 2017 でテスト プロジェクトを作成する

テスト対象のコードと同じソリューション内にある 1 つまたは複数のテスト プロジェクトでテストを実行します。 既存のソリューションに新しいテスト プロジェクトを追加するには、**ソリューション エクスプローラー**でソリューション ノードを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** の順に選びます。 次に、左側のウィンドウで **[Visual C++] > [テスト]** を選び、中央のウィンドウでプロジェクトの種類のいずれかを選びます。 次の図は、**C++ によるデスクトップ開発**ワークロードがインストールされている場合に選ぶことができるテスト プロジェクトです。

![C++ テスト プロジェクト](media/cpp-new-test-project.png)

::: moniker-end

### <a name="create-references-to-other-projects-in-the-solution"></a>ソリューション内の他のプロジェクトへの参照を作成する

テスト コードがテスト対象プロジェクト内の関数にアクセスできるようにするには、テスト プロジェクト内のプロジェクトへの参照を追加します。 **ソリューション エクスプローラー**でプロジェクト ノードを右クリックして、 **[追加]**  >  **[参照]** を選びます。 ダイアログで、テストするプロジェクトを選びます。

![参照の追加](media/cpp-add-ref-test-project.png)

### <a name="link-to-object-or-library-files"></a>オブジェクトまたはライブラリ ファイルのリンク

テストする関数がテスト コードでエクスポートされない場合は、出力された .obj ファイルまたは .lib ファイルをテスト プロジェクトの依存関係に追加できます。 「[オブジェクト ファイルまたはライブラリ ファイルにテストをリンクするには](/visualstudio/test/how-to-use-microsoft-test-framework-for-cpp#same_project)」を参照してください。

### <a name="add-include-directives-for-header-files"></a>ヘッダー ファイルの #include ディレクティブを追加する

次に、単体テストの *.cpp* ファイルで、テスト対象の型および関数が宣言されているヘッダー ファイルの `#include` ディレクティブを追加します。 「`#include "`」と入力すると、IntelliSense がアクティブ化して選択を支援します。 他のすべてのヘッダーについて繰り返します。

![インクルード ディレクティブを追加する](media/cpp-add-includes-test-project.png)

ソース ファイル内の各 include ステートメントに完全なパスを入力しなくても済むように、必要なフォルダーを **[プロジェクト]**  >  **[プロパティ]**  >  **[C/C++]**  >  **[全般]**  >  **[追加のインクルード ディレクトリ]** に追加します。

### <a name="write-test-methods"></a>テスト メソッドを作成する

> [!NOTE]
> ここでは、C/C++ の Microsoft 単体テスト フレームワークの構文を示します。 詳細については、「[Microsoft.VisualStudio.TestTools.CppUnitTestFramework API リファレンス](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)」を参照してください。 Google Test については、[Google Test の入門](https://github.com/google/googletest/blob/master/googletest/docs/primer.md)に関するドキュメントをご覧ください。 Boost.Test については、「[Boost Test library: The unit test framework](https://www.boost.org/doc/libs/1_46_0/libs/test/doc/html/utf.html)」 (Boost Test ライブラリ: 単体テスト フレームワーク) を参照してください。

テスト プロジェクトの *.cpp* ファイルには、テスト コード記述方法の例として、スタブ クラスとメソッドの定義が含まれます。 シグネチャで TEST_CLASS および TEST_METHOD マクロが使われていることに注意してください。これにより、 **[テスト エクスプローラー]** ウィンドウでメソッドを見つけることができます。

![インクルード ディレクティブを追加する](media/cpp-write-test-methods.png)

TEST_CLASS と TEST_METHOD は、[Microsoft ネイティブ テスト フレームワーク](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)の一部です。 **テスト エクスプローラー**は、サポートされている他のフレームワークのテスト メソッドも同様の方法で検出します。

TEST_METHOD は void を返します。 テスト結果を生成するには、`Assert` クラスの静的メソッドを使って、期待される結果に対して実際の結果をテストします。 次の例では、`MyClass` に `std::string` を受け取るコンストラクターがあるものとします。 コンストラクターが期待どおりにクラスを初期化することを次のようにテストできます。

```cpp
TEST_METHOD(TestClassInit)
{
    std::string name = "Bill";
    MyClass mc(name);
    Assert::AreEqual(name, mc.GetName());
}
```

前の例では、`Assert::AreEqual` の呼び出しの結果によって、テストが成功か失敗かが決まります。 Assert クラスには、予想される結果と実際の結果を比較するためのメソッドが他にも多く含まれています。

テスト メソッドに "*特徴*" を追加して、テストの所有者、優先度、他の情報を指定できます。 その後、これらの値を使って、**テスト エクスプローラー**でテストの並べ替えやグループ化を行うことができます。 詳細については、「[テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)」を参照してください。

### <a name="run-the-tests"></a>テストを実行

1. **[テスト]** メニューで、 **[Windows]** 、 **[テスト エクスプローラー]** の順に選択します。 次の図は、テストがまだ実行されていないテスト プロジェクトです。

   ![テスト実行前のテスト エクスプローラー](media/cpp-test-explorer.png)

   > [!NOTE]
   > CTest と**テスト エクスプローラー**の統合はまだ利用できません。 CTest のテストは CMake のメイン メニューから実行します。

1. ウィンドウに一部のテストしか表示されない場合は、次の方法でテスト プロジェクトをビルドします。**ソリューション エクスプローラー**で、該当するノードを右クリックし、 **[ビルド]** または **[リビルド]** を選択します。

1. **テスト エクスプローラー**で、 **[すべて実行]** を選択するか、または実行する特定のテストを選択します。 ブレークポイントを有効にした場合のデバッグ モードでのテストの実行など他のオプションについては、テストを右クリックします。 すべてのテストを実行すると、ウィンドウに成功したテストと失敗したテストが示されます。

![テスト実行後のテスト エクスプローラー](media/cpp-test-explorer-passed.png)

失敗したテストについては、原因の診断に役立つ詳細がメッセージで提供されます。 失敗したテストを右クリックして **[選択したテストのデバッグ]** を選び、障害が発生した関数をステップ実行できます。

**テスト エクスプローラー**の使い方については、「[テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)」をご覧ください。

単体テストに関するベスト プラクティスについては、「[単体テストの基本](unit-test-basics.md)」をご覧ください

## <a name="use-codelens"></a>CodeLens を使用する

**Visual Studio 2017 以降 (Professional および Enterprise エディション)**

[CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md) を使用すると、コード エディターを開いたままで単体テストの状態をすばやく確認できます。 次の中の任意の方法で、C++ 単体テスト プロジェクト用に CodeLens を初期化できます。

- テスト プロジェクトまたはソリューションを編集してビルドします。
- プロジェクトまたはソリューションをリビルドします。
- **テスト エクスプローラー** ウィンドウからテストを実行します。

**CodeLens** が初期化されたら、各単体テストの上にテストの状態アイコンが表示されます。

![C++ の CodeLens アイコン](media/cpp-test-codelens-icons.png)

アイコンをクリックして詳細を表示するか、単体テストを実行またはデバッグします。

![C++ の CodeLens の実行およびデバッグ](media/cpp-test-codelens-run-debug.png)

## <a name="see-also"></a>関連項目

- [コードの単体テスト](unit-test-your-code.md)
