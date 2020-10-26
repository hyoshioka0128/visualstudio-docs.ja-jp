---
title: C++ 用の Boost.Test を使用する方法
description: Boost.Test を使用し、Visual Studio で単体テストを作成します。
ms.date: 01/29/2020
ms.topic: how-to
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 34c593469a586d1314c7ee52f3aeb3ab6faf334c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85287273"
---
# <a name="how-to-use-boosttest-for-c-in-visual-studio"></a>Visual Studio で C++ 用の Boost.Test を使用する方法

Visual Studio 2017 以降、Boost.Test テスト アダプターは Visual Studio IDE に統合されています。 これは、**C++ によるデスクトップ開発**ワークロードのコンポーネントです。

![Test Adapter for Boost.Test](media/cpp-boost-component.png)

**[C++ によるデスクトップ開発]** ワークロードがインストールされていない場合は、**Visual Studio インストーラー**を開きます。 **[C++ によるデスクトップ開発]** ワークロードを選んで、 **[変更]** ボタンを選択します。

## <a name="install-boost"></a>Boost をインストールする

Boost.Test には [Boost](https://www.boost.org/) が必要です。 Boost がインストールされていない場合は、Vcpkg パッケージ マネージャーを使うことをお勧めします。

1. 「[vcpkg: Windows 用の C++ パッケージ マネージャー](/cpp/vcpkg)」の説明に従って、vcpkg をインストールします (まだない場合)。

1. Boost.Test のダイナミック ライブラリまたはスタティック ライブラリをインストールします。

    - Boost.Test のダイナミック ライブラリをインストールするには、`vcpkg install boost-test` を実行します。

       または

    - Boost.Test のスタティック ライブラリをインストールするには、`vcpkg install boost-test:x86-windows-static` を実行します。

1. `vcpkg integrate install` を実行して、ライブラリで Visual Studio を構成し、Boost のヘッダーとバイナリへのパスを組み込みます。

Visual Studio でソリューション内のテストを構成する方法を選択できます。テスト対象のプロジェクトにテスト コードを含める、またはテスト用に別のテスト プロジェクトを作成することができます。 どちらの選択肢にも長所と短所があります。

## <a name="add-tests-inside-your-project"></a>プロジェクトにテストを追加する

Visual Studio 2017 バージョン 15.6 以降、テスト用の項目テンプレートをプロジェクトに追加できます。 テストとコードの両方が同じプロジェクト内に存在します。 テスト ビルドを生成するには、別のビルド構成を作成する必要があります。 また、デバッグ ビルドとリリース ビルドからテストを除外する必要があります。

Visual Studio 2017 バージョン 15.5 には、Boost.Test に利用できる構成済みのテスト プロジェクトまたは項目テンプレートはありません。 手順に従って、別のテスト プロジェクトを作成および構成します。

### <a name="create-a-boosttest-item"></a>Boost.Test 項目を作成する

1. テスト用の *.cpp* ファイルを追加するには、**ソリューション エクスプローラー**でプロジェクト ノードを右クリックし、 **[追加]**  >  **[新規項目]** を選択します。

1. **[新しい項目の追加]** ダイアログで、 **[インストール済み]**  >  **[Visual C++]**  >  **[テスト]** を展開します。 **[Boost.Test]** を選択し、 **[追加]** を選択して、プロジェクトに *Test.cpp* を追加します。

   ![Boost.Test 項目テンプレート](media/boost_test_item_template.png)

新しい *Test.cpp* ファイルには、サンプル テスト メソッドが含まれます。 このファイルには、独自のヘッダー ファイルを含め、アプリのテストを記述することができます。

テスト ファイルでは、マクロを使用して、テスト構成の新しい `main` ルーチンを定義することもできます。 ここでプロジェクトをビルドすると、"_main は既に main.obj で定義されています。" などの LNK2005 エラーが表示されます。

### <a name="create-and-update-build-configurations"></a>ビルド構成を作成および更新する

1. テスト構成を作成するには、メニュー バーで **[ビルド]**  >  **[構成マネージャー]** を選択します。 **[構成マネージャー]** ダイアログで、 **[アクティブ ソリューション構成]** の下にあるドロップダウンを開き、 **[新規]** を選択します。 **[新しいソリューション構成]** ダイアログで、「Debug UnitTests」などの名前を入力します。 **[設定のコピー元]** で **[デバッグ]** を選択し、 **[OK]** を選択します。

1. デバッグ構成とリリース構成からテスト コードを除外します。**ソリューション エクスプローラー**で、Test.cpp ファイルを右クリックし、 **[プロパティ]** を選択します。 **[プロパティ ページ]** ダイアログで、 **[構成]** ドロップダウンの **[すべての構成]** を選択します。 **[構成プロパティ]**  >  **[全般]** を選択して、 **[ビルドから除外]** プロパティのドロップダウンを開きます。 **[はい]** を選択し、 **[適用]** を選択して変更を保存します。

1. Debug UnitTests 構成にテスト コードを含めるには、 **[プロパティ ページ]** ダイアログで、 **[構成]** ドロップダウンの **[Debug UnitTests]** を選択します。 **[ビルドから除外]** プロパティの **[いいえ]** を選択し、 **[OK]** を選択して変更を保存します。

1. Debug UnitTests 構成からメイン コードを除外します。 **ソリューション エクスプローラー**で `main` 関数が含まれるファイルを右クリックし、 **[プロパティ]** を選択します。 **[プロパティ ページ]** ダイアログで、 **[構成]** ドロップダウンの **[Debug UnitTests]** を選択します。 **[構成プロパティ]**  >  **[全般]** を選択して、 **[ビルドから除外]** プロパティのドロップダウンを開きます。 **[はい]** を選択し、 **[OK]** を選択して変更を保存します。

1. ソリューション構成を **Debug UnitTests** に設定し、**テスト エクスプローラー**でメソッドを検出できるようにプロジェクトをビルドします。

作成した構成名が "Debug" または "Release" という語で始まる限り、対応する Boost.Test ライブラリが自動的に選択されます。

項目テンプレートは、Boost.Test の単一ヘッダー バリアントを使用しますが、スタンドアロン ライブラリ バリアントを使用するように #include パスを変更できます。 詳細については、「[インクルード ディレクティブを追加する](#add-include-directives)」を参照してください。

## <a name="create-a-separate-test-project"></a>別のテスト プロジェクトを作成する

多くの場合、テストに別のプロジェクトを使用する方が簡単です。 プロジェクトに特別なテスト構成を作成する必要はありません。 または、デバッグ ビルドとリリース ビルドからテスト ファイルを除外します。

### <a name="to-create-a-separate-test-project"></a>別のテスト プロジェクトを作成するには

1. **ソリューション エクスプローラー**で、ソリューション ノードを右クリックして、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. **[新しいプロジェクトの追加]** ダイアログで、フィルター ドロップダウンの **[C++]** 、 **[Windows]** 、 **[コンソール]** を選択します。 **[コンソール アプリ]** テンプレートを選択し、 **[次へ]** を選択します。

1. プロジェクト名を設定し、 **[作成]** を選択します。

1. *.cpp* ファイル内の `main` 関数を削除します。

1. Boost.Test の単一ヘッダーまたはダイナミック ライブラリ バージョンを使用している場合は、「[インクルード ディレクティブを追加する](#add-include-directives)」に進みます。 スタティック ライブラリ バージョンを使用している場合は、追加の構成を実行する必要があります。

   a. プロジェクト ファイルを編集するには、最初にプロジェクト ファイルをアンロードします。 **ソリューション エクスプローラー**で、プロジェクト ノードを右クリックして **[プロジェクトのアンロード]** を選択します。 次に、プロジェクト ノードを右クリックして、 **[<名前\>.vcxproj の編集]** を選択します。

   b. 次に示すように、**Globals** プロパティ グループに 2 つの行を追加します。

    ```xml
    <PropertyGroup Label="Globals">
    ....
        <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
        <VcpkgEnabled>true</VcpkgEnabled>
    </PropertyGroup>
    ```

   c. *\*.vcxproj* ファイルを保存して閉じた後、プロジェクトをリロードします。

   d. **プロパティ ページ**を開くには、プロジェクト ノードを右クリックして、 **[プロパティ]** を選択します。

   e. **[C/C++]**  >  **[コード生成]** の順に展開し、 **[ランタイム ライブラリ]** を選択します。 スタティック ランタイム ライブラリをデバッグする場合は **/MTd** を、スタティック ランタイム ライブラリをリリースする場合は **/MT** を選択します。

   f. **[リンカー]**  >  **[システム]** の順に展開します。 **[サブシステム]** が **[コンソール]** に設定されていることを確認します。

   g. **[OK]** を選んで、プロパティ ページを閉じます。

## <a name="add-include-directives"></a>インクルード ディレクティブを追加する

1. テストの *.cpp* ファイルで、必要な `#include` ディレクティブを追加して、プログラムの型と関数がテスト コードに認識されるようにします。 別のテスト プロジェクトを使用している場合は、通常、プログラムはフォルダー階層内の兄弟レベルにあります。 「`#include "../"`」と入力すると IntelliSense ウィンドウが表示され、ヘッダー ファイルへの完全パスを選択できます。

   ![#include ディレクティブを追加する](media/cpp-gtest-includes.png)

   次のようにすると、スタンドアロン ライブラリを使うことができます。

   ```cpp
   #include <boost/test/unit_test.hpp>
   ```

   または、次のようにすると、単一ヘッダー バージョンを使うことができます。

   ```cpp
   #include <boost/test/included/unit_test.hpp>
   ```

   次に、`BOOST_TEST_MODULE` を定義します。

テストが**テスト エクスプローラー**で検出されるのに十分な例を次に示します。

```cpp
#define BOOST_TEST_MODULE MyTest
#include <boost/test/included/unit_test.hpp\> //single-header
#include "../MyProgram/MyClass.h" // project being tested
#include <string>

BOOST_AUTO_TEST_CASE(my_boost_test)
{
    std::string expected_value = "Bill";

    // assume MyClass is defined in MyClass.h
    // and get_value() has public accessibility
    MyClass mc;
    BOOST_CHECK(expected_value == mc.get_value());
}
```

## <a name="write-and-run-tests"></a>テストを作成して実行する

Boost テストを作成して実行する準備が整いました。 テスト マクロについては、[Boost Test ライブラリのドキュメント](https://www.boost.org/doc/libs/1_71_0/libs/test/doc/html/index.html)をご覧ください。 **テスト エクスプローラー**を使ってテストを検出、実行、グループ化する方法については、「[テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [C/C++ 用の単体テストの記述](writing-unit-tests-for-c-cpp.md)
