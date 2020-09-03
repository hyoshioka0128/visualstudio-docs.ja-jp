---
title: ストア アプリ用の Visual C++ DLL の単体テスト | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 24afc90a-8774-4699-ab01-6602a7e6feb2
caps.latest.revision: 15
author: alexhomer1
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9d5f86eb40e1401f98a4c66d0b971fb006762cc1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659695"
---
# <a name="unit-testing-a-visual-c-dll-for-store-apps"></a>ストア アプリ用の Visual C++ DLL の単体テスト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、Windows ストア アプリの C++ DLL の単体テストを作成する方法の 1 つについて説明します。RooterLib DLL は、指定した数値の平方根の概算を計算する関数を実装することによって、微積分の限界理論の不明瞭なメモリを示します。 この DLL を、ユーザーが数学で実行できる楽しい作業を提示する Windows ストア アプリに組み込むことができます。

 このトピックでは、開発の第一歩として単体テストを使用する方法を示します。 この方法ではまず、テスト対象のシステムの特定の動作を検証するテスト メソッドを作成し、テストに合格するコードを記述します。 後述する手順の順序を変更することにより、この方法を逆にして、テストするコードを最初に記述し、単体テストを作成することができます。

 このトピックでは、テストする単体テストと DLL に 1 つの Visual Studio ソリューションと個別のプロジェクトも作成します。 また、DLL プロジェクトに単体テストを直接含めることも、単体テストと DLL ごとに個別のソリューションを作成することもできます。 使用できる構造体のヒントについては、「[テスト エクスプローラーを使用した既存の C++ アプリケーションの単体テスト](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)」をご覧ください。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
 このトピックでは、次のタスクを実行します。

 [ソリューションと単体テストプロジェクトを作成する](#BKMK_Create_the_solution_and_the_unit_test_project)

 [テストエクスプローラーでテストが実行されていることを確認する](#BKMK_Verify_that_the_tests_run_in_Test_Explorer)

 [DLL プロジェクトをソリューションに追加する](#BKMK_Add_the_DLL_project_to_the_solution)

 [Dll プロジェクトにテストプロジェクトを結合する](#BKMK_Couple_the_test_project_to_the_dll_project)

 [テストを繰り返し増やして成功させる](#BKMK_Iteratively_augment_the_tests_and_make_them_pass)

 [失敗したテストのデバッグ](#BKMK_Debug_a_failing_test)

 [テストを変更せずにコードをリファクタリングする](#BKMK_Refactor_the_code_without_changing_tests)

## <a name="create-the-solution-and-the-unit-test-project"></a><a name="BKMK_Create_the_solution_and_the_unit_test_project"></a> ソリューションと単体テスト プロジェクトを作成する

1. **[ファイル]** メニューの **[新規作成]** をポイントし、**[新しいプロジェクト]** をクリックします。

2. [新しいプロジェクト] ダイアログで **[インストール済み]**、**[Visual C++]** の順に展開し、**[Windows ストア]** を選択します。 プロジェクト テンプレートの一覧の **[単体テスト ライブラリ (Windows ストア アプリ)]** をクリックします。

     ![C&#43;&#43; 単体テストライブラリを作成する](../test/media/ute-cpp-windows-unittestlib-create.png "UTE_Cpp_windows_UnitTestLib_Create")

3. プロジェクトに `RooterLibTests` という名前を付けます。場所を指定します。ソリューションに `RooterLib` という名前を付けます。 **[ソリューションのディレクトリを作成]** チェックボックスがオンになっていることを確認します。

     ![ソリューション、プロジェクト名、および場所の指定](../test/media/ute-cpp-windows-unittestlib-createspecs.png "UTE_Cpp_windows_UnitTestLib_CreateSpecs")

4. 新しいプロジェクトで、**unittest1.cpp** を開きます。

     ![unittest1.cpp](../test/media/ute-cpp-windows-unittest1-cpp.png "UTE_Cpp_windows_unittest1_cpp")

     次の点に注意してください。

    - 各テストは `TEST_METHOD(YourTestName){...}` を使用して定義されます。

         従来の関数の署名を記述する必要はありません。 署名は、マクロ TEST_METHOD によって作成されます。 マクロは、void を返すインスタンス関数を生成します。 また、テスト メソッドに関する情報を返す静的関数も生成します。 この情報により、テスト エクスプ ローラーはメソッドを見つけます。

    - テスト メソッドは、 `TEST_CLASS(YourClassName){...}`を使用してクラスにグループ化されます。

         テストが実行されると、各テスト クラスのインスタンスが作成されます。 テスト メソッドが呼び出される順序は決まっていません。 各モジュール、クラス、またはメソッドの前後に呼び出される特殊なメソッドを定義することができます。 詳細については、MSDN ライブラリの「[Microsoft.VisualStudio.TestTools.CppUnitTestFramework の使用](../test/using-microsoft-visualstudio-testtools-cppunittestframework.md)」をご覧ください。

## <a name="verify-that-the-tests-run-in-test-explorer"></a><a name="BKMK_Verify_that_the_tests_run_in_Test_Explorer"></a> テストがテスト エクスプローラーで実行されることを確認する

1. 幾らかのテスト コードを挿入します。

    ```cpp
    TEST_METHOD(TestMethod1)
    {
        Assert::AreEqual(1,1);
    }
    ```

     `Assert` クラスは、テスト メソッドで結果を確認するために使用するいくつかの静的メソッドを提供することに注意してください。

2. **[テスト]** メニューの **[実行]** をポイントし、 **[すべて実行]** をクリックします。

     テスト プロジェクトがビルドされ、実行されます。 テスト エクスプローラーのウィンドウが表示され、テストが **[成功したテスト]** に表示されます。 ウィンドウの下部の [概要] ウィンドウに、選択したテストに関する詳細情報が表示されます。

     ![テスト エクスプローラー](../test/media/ute-cpp-testexplorer-testmethod1.png "UTE_Cpp_TestExplorer_TestMethod1")

## <a name="add-the-dll-project-to-the-solution"></a><a name="BKMK_Add_the_DLL_project_to_the_solution"></a> DLL プロジェクトをソリューションに追加する

1. ソリューション エクスプローラーでソリューション名を選択します。 ショートカット メニューの **[追加]** をポイントし、**[新しいプロジェクトの追加]** を選択します。

     ![RooterLib プロジェクトの作成](../test/media/ute-cpp-windows-rooterlib-create.png "UTE_Cpp_windows_RooterLib_Create")

2. **[新しいプロジェクトの追加]** ダイアログ ボックスの **[DLL (Windows ストア アプリ)]** を選択します。

3. **RooterLib.h** ファイルに次のコードを追加します。

    ```cpp
    // The following ifdef block is the standard way of creating macros which make exporting
    // from a DLL simpler. All files within this DLL are compiled with the ROOTERLIB_EXPORTS
    // symbol defined on the command line. This symbol should not be defined on any project
    // that uses this DLL. This way any other project whose source files include this file see
    // ROOTERLIB_API functions as being imported from a DLL, whereas this DLL sees symbols
    // defined with this macro as being exported.
    #ifdef ROOTERLIB_EXPORTS
    #define ROOTERLIB_API  __declspec(dllexport)
    #else
    #define ROOTERLIB_API __declspec(dllimport)
    #endif //ROOTERLIB_EXPORTS

    class ROOTERLIB_API CRooterLib {
    public:
        CRooterLib(void);
        double SquareRoot(double v);
    };
    ```

     コメントは、dll の開発者だけでなく、プロジェクトで DLL を参照するユーザーにも ifdef ブロックについて説明しています。 DLL のプロジェクト プロパティを使用して、コマンド ラインに ROOTERLIB_EXPORTS シンボルを追加できます。

     `CRooterLib` クラスは、コンストラクターと `SqareRoot` エスティメーターのメソッドを宣言します。

4. コマンド ラインに ROOTERLIB_EXPORTS のシンボルを追加します。

    1. ソリューションエクスプローラーで、 **RooterLib** プロジェクトを選択し、ショートカットメニューの [ **プロパティ** ] をクリックします。

         ![プロプロセッサ シンボル定義の追加](../test/media/ute-cpp-windows-addpreprocessorsymbol.png "UTE_Cpp_windows_AddPreprocessorSymbol")

    2. RooterLib の [プロパティ ページ] ダイアログ ボックスで **[構成プロパティ]** 、 **[C++]** の順に展開し、 **[プリプロセッサ]** を選択します。

    3. **[プリプロセッサの定義]\<Edit...> ボックスの一覧の** [ **]** を選択し、 [プリプロセッサの定義] ダイアログ ボックスに `ROOTERLIB_EXPORTS` を追加します。

5. 宣言された関数の最小限の実装を追加します。 **RooterLib.cpp** を開き、次のコードを追加します。

    ```
    // constructor
    CRooterLib::CRooterLib()
    {
    }

    // Find the square root of a number.
    double CRooterLib::SquareRoot(double v)
    {
        return 0.0;
    }

    ```

## <a name="couple-the-test-project-to-the-dll-project"></a><a name="BKMK_Couple_the_test_project_to_the_dll_project"></a> Dll プロジェクトにテストプロジェクトを結合する

1. RooterLibTests プロジェクトに RooterLib を追加します。

   1. ソリューションエクスプローラーで、 **RooterLibTests** プロジェクトを選択し、ショートカットメニューの [ **参照** ] をクリックします。

   2. RooterLib の [プロジェクトのプロパティ] ダイアログ ボックスで **[共通プロパティ]** を展開し、**[Framework と参照]** を選択します。

   3. [**新しい参照の追加**] を選択します。

   4. **[参照の追加]** ダイアログ ボックスで **[ソリューション]** を展開し、**[プロジェクト]** を選択します。 次に **[RouterLib]** 項目を選択します。

2. **unittest1.cpp** に RooterLib のヘッダー ファイルをインクルードします。

   1. **unittest1.cpp** を開きます。

   2. `#include "CppUnitTest.h"` 行の下に次のコードを追加します。

       ```cpp
       #include "..\RooterLib\RooterLib.h"
       ```

3. インポートした関数を使用するテストを追加します。 **unittest1.cpp** に次のコードを追加します。

   ```
   TEST_METHOD(BasicTest)
   {
       CRooterLib rooter;
       Assert::AreEqual(
           // Expected value:
           0.0,
           // Actual value:
           rooter.SquareRoot(0.0),
           // Tolerance:
           0.01,
           // Message:
           L"Basic test failed",
           // Line number - used if there is no PDB file:
           LINE_INFO());
   }

   ```

4. ソリューションをビルドします。

    新しいテストがテスト エクスプローラーの **[テストを実行しない]** ノードに表示されます。

5. テストエクスプローラーで [ **すべて実行**] を選択します。

    ![基本テスト成功](../test/media/ute-cpp-testexplorer-basictest.png "UTE_Cpp_TestExplorer_BasicTest")

   テストとコード プロジェクトをセット アップして、コード プロジェクトで関数を実行するテストを実行できることを確認しました。 ここで、実際のテストおよびコードの記述を開始できます。

## <a name="iteratively-augment-the-tests-and-make-them-pass"></a><a name="BKMK_Iteratively_augment_the_tests_and_make_them_pass"></a> テストを繰り返し増やして成功させる

1. 新しいテストを追加します。

    ```
    TEST_METHOD(RangeTest)
    {
        CRooterLib rooter;
        for (double v = 1e-6; v < 1e6; v = v * 3.2)
        {
            double expected = v;
            double actual = rooter.SquareRoot(v*v);
            double tolerance = expected/1000;
            Assert::AreEqual(expected, actual, tolerance);
        }
    };

    ```

    > [!TIP]
    > 合格したテスト内容を変更しないことをお勧めします。 代わりに、新しいテストを追加し、テストが合格するようにコードを更新してから別のテストを追加する、という過程を繰り返します。
    >
    >  ユーザーが要件を変更したら、正しくなくなったテストを無効にします。 新しいテストを作成し、一度に 1 つずつ、同じ増分方式で処理するようにします。

2. テストエクスプローラーで [ **すべて実行**] を選択します。

3. テストが失敗します。

     ![RangeTest 失敗](../test/media/ute-cpp-testexplorer-rangetest-fail.png "UTE_Cpp_TestExplorer_RangeTest_Fail")

    > [!TIP]
    > 各テストが記述した後すぐに失敗することを確認します。 これは、絶対に失敗しないテストを記述するという簡単なミスを避けることに役立ちます。

4. 新しいテストが成功するように、テスト対象のコードを増やします。 **RooterLib.cpp** に次のコードを追加します。

    ```cpp
    #include <math.h>
    ...
    // Find the square root of a number.
    double CRooterLib::SquareRoot(double v)
    {
        double result = v;
        double diff = v;
        while (diff > result/1000)
        {
            double oldResult = result;
            result = result - (result*result - v)/(2*result);
            diff = abs (oldResult - result);
        }
        return result;
    }

    ```

5. ソリューションをビルドし、テストエクスプローラーで [ **すべて実行**] を選択します。

     両方のテストが合格します。

> [!TIP]
> 一度に 1 つのテストを追加してコードを開発します。 各反復処理の後にすべてのテストが合格することを確認します。

## <a name="debug-a-failing-test"></a><a name="BKMK_Debug_a_failing_test"></a> 失敗したテストをデバッグする

1. **unittest1.cpp** に別のテストを追加します。

   ```
   // Verify that negative inputs throw an exception.
    TEST_METHOD(NegativeRangeTest)
    {
      wchar_t message[200];
      CRooterLib rooter;
      for (double v = -0.1; v > -3.0; v = v - 0.5)
      {
        try
        {
          // Should raise an exception:
          double result = rooter.SquareRoot(v);

          swprintf_s(message, L"No exception for input %g", v);
          Assert::Fail(message, LINE_INFO());
        }
        catch (std::out_of_range ex)
        {
          continue; // Correct exception.
        }
        catch (...)
        {
          swprintf_s(message, L"Incorrect exception for %g", v);
          Assert::Fail(message, LINE_INFO());
        }
      }
   };

   ```

2. テストエクスプローラーで [ **すべて実行**] を選択します。

    テストが失敗します。 テスト エクスプローラーでテスト名を選択します。 失敗したアサーションが強調表示されます。 エラー メッセージは、テスト エクスプ ローラーの [詳細] ウィンドウに表示されます。

    ![NegativeRangeTest 失敗](../test/media/ute-cpp-testexplorer-negativerangetest-fail.png "UTE_Cpp_TestExplorer_NegativeRangeTest_Fail")

3. テストが失敗した理由を表示するには、関数をステップ実行します。

   1. `SquareRoot` 関数の先頭にブレークポイントを設定します。

   2. 失敗したテストのショートカット メニューで **[選択したテストのデバッグ]** をクリックします。

        実行がブレークポイントで停止したら、コードをステップ実行します。

   3. 例外をキャッチするには、**RooterLib.cpp** にコードを追加します。

       ```
       #include <stdexcept>
       ...
       double CRooterLib::SquareRoot(double v)
       {
           //Validate the input parameter:
           if (v < 0.0)
           {
             throw std::out_of_range("Can't do square roots of negatives");
           }
       ...

       ```

   1. テストエクスプローラーで [ **すべて実行** ] をクリックして、修正されたメソッドをテストし、回帰が導入されていないことを確認します。

   今回は、すべてのテストに合格します。

   ![すべてのテストの成功](../test/media/ute-ult-alltestspass.png "UTE_ULT_AllTestsPass")

## <a name="refactor-the-code-without-changing-tests"></a><a name="BKMK_Refactor_the_code_without_changing_tests"></a> テストを変更せずにコードをリファクタリングする

1. `SquareRoot` 関数の計算全体を簡略化します。

    ```
    // old code
    //result = result - (result*result - v)/(2*result);
    // new code
    result = (result + v/result) / 2.0;

    ```

2. **[すべて実行]** をクリックして、リファクタリングされたメソッドをテストし、回帰が生じていないことを確認します。

    > [!TIP]
    > 安定した一連の適切な単体テストを実行することで、コードを変更したときにバグが生じていないことを確信できます。
    >
    >  常に他の変更とは別にリファクタリングしてください。
