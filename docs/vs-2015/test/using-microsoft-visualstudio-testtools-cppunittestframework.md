---
title: Microsoft.VisualStudio.TestTools.CppUnitTestFramework の使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: d1ac9188-d79f-407e-9f3a-80dbefa66317
caps.latest.revision: 10
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c561555df40bc02c3c9f3090ee1de4c0f329bcdc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657170"
---
# <a name="using-microsoftvisualstudiotesttoolscppunittestframework"></a>Microsoft.VisualStudio.TestTools.CppUnitTestFramework の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは `Microsoft::VisualStudio::CppUnitTestFramework` の名前空間のパブリック メンバーの一覧を示します。

 ヘッダーファイルは  _VisualStudio2012 [x86] InstallFolder_**\ Vc\ Unittest/include** フォルダーにあります。

 Lib ファイルは  _VisualStudio2012 [x86] InstallFolder_**\ Vc\ unittest\ lib** フォルダーにあります。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
 [CppUnitTest.h](#BKMK_CppUnitTest_h)

- [テスト クラスとメソッドを作成する](#BKMK_Create_test_classes_and_methods)

- [初期化とクリーンアップ](#BKMK_Initialize_and_cleanup)

  - [テスト メソッド](#BKMK_Test_methods)

  - [テスト クラス](#BKMK_Test_classes)

  - [テスト モジュール](#BKMK_Test_modules)

- [テスト属性を作成する](#BKMK_Create_test_attributes)

  - [テスト メソッド属性](#BKMK_Test_method_attributes)

  - [テスト クラス属性](#BKMK_Test_class_attributes)

  - [テスト モジュール属性](#BKMK_Test_module_attributes)

  - [定義済みの属性](#BKMK_Pre_defined_attributes)

    [CppUnitTestAssert.h](#BKMK_CppUnitTestAssert_h)

  - [一般的なアサート](#BKMK_General_Asserts)

    - [等しい](#BKMK_General_Are_Equal)

    - [等しくない](#BKMK_General_Are_Not_Equal)

    - [同じである](#BKMK_General_Are_Same)

    - [同じではない](#BKMK_General_Are_Not_Same)

    - [Null である](#BKMK_General_Is_Null)

    - [Null ではない](#BKMK_General_Is_Not_Null)

    - [True である](#BKMK_General_Is_True)

    - [False である](#BKMK_General_Is_False)

    - [失敗](#BKMK_General_Fail)

  - [Windows ランタイム アサート](#BKMK_WinRT_Asserts)

    - [等しい](#BKMK_WinRT_Are_Equal)

    - [同じである](#BKMK_WinRT_Are_Same)

    - [等しくない](#BKMK_WinRT_Are_Not_Equal)

    - [同じではない](#BKMK_WinRT_Are_Not_Same)

    - [Null である](#BKMK_WinRT_Is_Null)

    - [Null ではない](#BKMK_WinRT_Is_Not_Null)

  - [例外アサート](#BKMK_Exception_Asserts)

    - [例外を想定する](#BKMK_Expect_Exception)

      [CppUnitTestLogger.h](#BKMK_CppUnitTestLogger_h)

    - [Logger](#BKMK_Logger)

    - [メッセージの書き込み](#BKMK_Write_Message)

## <a name="cppunittesth"></a><a name="BKMK_CppUnitTest_h"></a> CppUnitTest.h

### <a name="create-test-classes-and-methods"></a><a name="BKMK_Create_test_classes_and_methods"></a> テスト クラスとメソッドを作成する

```cpp
TEST_CLASS(className)
```

 テスト メソッドを含む各クラスに必要です。 *className* をテスト クラスとして識別します。 `TEST_CLASS` は namescape のスコープで宣言する必要があります。

```cpp
TEST_METHOD(methodName)
{
    // test method body
}

```

 *methodName* をテスト メソッドとして定義します。 `TEST_METHOD` はメソッドのクラスのスコープ内で宣言する必要があります。

### <a name="initialize-and-cleanup"></a><a name="BKMK_Initialize_and_cleanup"></a> 初期化とクリーンアップ

#### <a name="test-methods"></a><a name="BKMK_Test_methods"></a> テスト メソッド

```cpp
TEST_METHOD_INITIALIZE(methodName)
{
    // method initialization code
}

```

 *methodName* を各テスト メソッドが実行される前に実行するメソッドとして定義します。 `TEST_METHOD_INITIALIZE` はテスト クラスで一度だけ定義でき、そのテスト クラスで定義する必要があります。

```cpp
TEST_METHOD_CLEANUP(methodName)
{
    // test method cleanup  code
}

```

 *methodName* を各テスト メソッドの実行後に実行するメソッドとして定義します。 `TEST_METHOD_CLEANUP` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

#### <a name="test-classes"></a><a name="BKMK_Test_classes"></a> テスト クラス

```cpp
TEST_CLASS_INITIALIZE(methodName)
{
    // test class initialization  code
}

```

 *methodName* を各テスト クラスの作成後に実行するメソッドとして定義します。 `TEST_CLASS_INITIALIZE` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

```cpp
TEST_CLASS_CLEANUP(methodName)
{
    // test class cleanup  code
}

```

 *methodName* を各テスト クラスの作成後に実行するメソッドとして定義します。 `TEST_CLASS_CLEANUP` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

#### <a name="test-modules"></a><a name="BKMK_Test_modules"></a> テスト モジュール

```cpp
TEST_MODULE_INITIALIZE(methodName)
{
    // module initialization code
}
```

 モジュールが読み込まれるときに実行するメソッド *methodName* を定義します。 `TEST_MODULE_INITIALIZE` はテスト モジュールで一度だけ定義でき、名前空間スコープで宣言する必要があります。

```cpp
TEST_MODULE_CLEANUP(methodName)
```

 モジュールがアンロードされるときに実行するメソッド *methodName* を定義します。 `TEST_MODULE_CLEANUP` はテスト モジュールで一度だけ定義でき、名前空間スコープで宣言する必要があります。

### <a name="create-test-attributes"></a><a name="BKMK_Create_test_attributes"></a> テスト属性を作成する

#### <a name="test-method-attributes"></a><a name="BKMK_Test_method_attributes"></a> テスト メソッドの属性

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(testMethodName)
    TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_METHOD_ATTRIBUTE()
```

 テスト メソッド *testClassName* に、`TEST_METHOD_ATTRIBUTE` の 1 つ以上のマクロで定義された属性を追加します。

 `TEST_METHOD_ATTRIBUTE` マクロは名前 *attributeName* と値 *attributeValue* を持つ属性を定義します。

#### <a name="test-class-attributes"></a><a name="BKMK_Test_class_attributes"></a> テスト クラス属性

```cpp
BEGIN_TEST_CLASS_ATTRIBUTE(testClassName)
    TEST_CLASS_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_CLASS_ATTRIBUTE()
```

 テスト クラス *testClassName* に、`TEST_CLASS_ATTRIBUTE` の 1 つ以上のマクロで定義された属性を追加します。

 `TEST_CLASS_ATTRIBUTE` マクロは名前 *attributeName* と値 *attributeValue* を持つ属性を定義します。

#### <a name="test-module-attributes"></a><a name="BKMK_Test_module_attributes"></a> テスト モジュール属性

```cpp
BEGIN_TEST_MODULE_ATTRIBUTE(testModuleName)
    TEST_MODULE_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_MODULE_ATTRIBUTE()
```

 テスト モジュール *testModuleName* に、`TEST_MODULE_ATTRIBUTE` の 1 つ以上のマクロで定義された属性を追加します。

 `TEST_MODULE_ATTRIBUTE` マクロは名前 *attributeName* と値 *attributeValue* を持つ属性を定義します。

#### <a name="pre-defined-attributes"></a><a name="BKMK_Pre_defined_attributes"></a> 定義済みの属性
 これらの定義済み属性マクロは、前に説明したマクロ `TEST_METHOD_ATTRIBUTE`、`TEST_CLASS_ATTRIBUTE`、または `TEST_MODULE_ATTRIBUTE` と置き換えることができます。

```cpp
TEST_OWNER(ownerAlias)
```

 名前 `Owner` と属性値 *ownerAlias* を持つ属性を定義します。

```cpp
TEST_DESCRIPTION(description)
```

 名前 `Description` と属性値 *description* を持つ属性を定義します。

```cpp
TEST_PRIORITY(priority)
```

 名前 `Priority` と属性値 *priority* を持つ属性を定義します。

```cpp
TEST_WORKITEM(workitem)
```

 名前 `WorkItem` と属性値 *workItem* を持つ属性を定義します。

```cpp
TEST_IGNORE()
```

 名前 `Ignore` と属性値 `true` を持つ属性を定義します。

## <a name="cppunittestasserth"></a><a name="BKMK_CppUnitTestAssert_h"></a> CppUnitTestAssert.h

### <a name="general-asserts"></a><a name="BKMK_General_Asserts"></a> 一般的なアサート

#### <a name="are-equal"></a><a name="BKMK_General_Are_Equal"></a> 等しい
 2 つのオブジェクトが等しいことを確認します

```cpp
template<typename T>
static void AreEqual(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの倍精度小数点数が等しいことを確認します

```cpp
static void AreEqual(
    double expected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの浮動小数点数が等しいことを確認します

```cpp
static void AreEqual(
    float expected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの char* 文字列が等しいことを確認します

```cpp
static void AreEqual(
    const char* expected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの w_char* 文字列が等しいことを確認します

```cpp
static void AreEqual(
    const wchar_t* expected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-not-equal"></a><a name="BKMK_General_Are_Not_Equal"></a> 等しくない
 2 つの倍精度小数点数が等しくないことを確認します

```cpp
static void AreNotEqual(
    double notExpected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの浮動小数点数が等しくないことを確認します

```cpp
static void AreNotEqual(
    float notExpected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの char* 文字列が等しくないことを確認します

```cpp
static void AreNotEqual(
    const char* notExpected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 2 つの w_char* 文字列が等しくないことを確認します

```cpp
static void AreNotEqual(
    const wchar_t* notExpected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

 演算子 == に基づいて、2 つの参照が等しくないことを確認します

```cpp
template<typename T>
static void AreNotEqual(
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-same"></a><a name="BKMK_General_Are_Same"></a> 同じである
 2 つの参照が同じオブジェクト インスタンス (ID) を参照していることを確認します。

```cpp
template<typename T>
static void AreSame(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-not-same"></a><a name="BKMK_General_Are_Not_Same"></a> 同じではない
 2 つの参照が同じオブジェクト インスタンス (ID) を参照していないことを確認します。

```cpp
template<typename T>
static void AreNotSame (
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-null"></a><a name="BKMK_General_Is_Null"></a> Null である
 ポインターが NULL であることを確認します。

```cpp
template<typename T>
static void IsNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-not-null"></a><a name="BKMK_General_Is_Not_Null"></a> Null ではない
 ポインターが NULL ではないことを確認します

```cpp
template<typename T>
static void IsNotNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-true"></a><a name="BKMK_General_Is_True"></a> True である
 条件が true であることを確認します

```cpp
static void IsTrue(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-false"></a><a name="BKMK_General_Is_False"></a> False である
 条件が false であることを確認します

```cpp
static void IsFalse(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="fail"></a><a name="BKMK_General_Fail"></a> 失敗
 テスト ケースの結果が失敗するよう強制します

```cpp
static void Fail(
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

### <a name="windows-runtime-asserts"></a><a name="BKMK_WinRT_Asserts"></a> Windows ランタイム アサート

#### <a name="are-equal"></a><a name="BKMK_WinRT_Are_Equal"></a> 等しい
 2 つの Windows ランタイム ポインターが等しいことを確認します。

```
template<typename T>
static void AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

 2 つの Platform::String^ 文字列が等しいことを確認します。

```
template<typename T>
static void AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-same"></a><a name="BKMK_WinRT_Are_Same"></a> 同じである
 2 つの Windows ランタイム参照が同じオブジェクトを参照していることを確認します。

```
template<typename T>
static void AreSame(
    T% expected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-not-equal"></a><a name="BKMK_WinRT_Are_Not_Equal"></a> 等しくない
 2 つの Windows ランタイム ポインターが等しくないことを確認します。

```
template<typename T>
static void AreNotEqual(
    T^ notExpected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

 2 つの Platform::String^ 文字列が等しくないことを確認します。

```
static void AreNotEqual(
    Platform::String^ notExpected,
    Platform::String^ actual,
    bool ignoreCase = false,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-not-same"></a><a name="BKMK_WinRT_Are_Not_Same"></a> 同じではない
 2 つの Windows ランタイム参照が同じオブジェクトを参照していないことを確認します。

```
template<typename T>
static void AreNotSame(
    T% notExpected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="is-null"></a><a name="BKMK_WinRT_Is_Null"></a> Null である
 Windows ランタイム ポインターが nullptr であることを確認します。

```
template<typename T>
static void IsNull(
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="is-not-null"></a><a name="BKMK_WinRT_Is_Not_Null"></a> Null ではない
 Windows ランタイム ポインターが nullptr ではないことを確認します。

```
template<typename T>
static void IsNotNull(
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

### <a name="exception-asserts"></a><a name="BKMK_Exception_Asserts"></a> 例外アサート

#### <a name="expect-exception"></a><a name="BKMK_Expect_Exception"></a> 例外を想定する
 関数が例外を発生させることを確認します。

```
template<typename _EXPECTEDEXCEPTION, typename _FUNCTOR>
static void ExpectException(
    _FUNCTOR functor,
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo= NULL)
```

 関数が例外を発生させることを確認します。

```
template<typename _EXPECTEDEXCEPTION, typename _RETURNTYPE>
    static void ExpectException(
    _RETURNTYPE (*func)(),
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo = NULL)
```

## <a name="cppunittestloggerh"></a><a name="BKMK_CppUnitTestLogger_h"></a> CppUnitTestLogger.h

### <a name="logger"></a><a name="BKMK_Logger"></a> Logger
 ロガー クラスには書き込みを行うための静的メソッドが含まれます

```
class Logger
```

### <a name="write-message"></a><a name="BKMK_Write_Message"></a> メッセージの書き込み

```
static void
Logger::WriteMessage(const wchar_t* message)
```

```
static void
Logger::WriteMessage(const char* message)
```

## <a name="example"></a>例
 以下のコードは一例です

```
////////////////////////////////////////////////////////////
/* USAGE EXAMPLE
// The following is an example of VSCppUnit usage.
// It includes examples of attribute metadata, fixtures,
// unit tests with assertions, and custom logging.

#include <CppUnitTest.h>

using namespace Microsoft::VisualStudio::CppUnitTestFramework;

BEGIN_TEST_MODULE_ATTRIBUTE()
    TEST_MODULE_ATTRIBUTE(L"Date", L"2010/6/12")
END_TEST_MODULE_ATTRIBUTE()

TEST_MODULE_INITIALIZE(ModuleInitialize)
{
    Logger::WriteMessage("In Module Initialize");
}

TEST_MODULE_CLEANUP(ModuleCleanup)
{
    Logger::WriteMessage("In Module Cleanup");
}

TEST_CLASS(Class1)
{

public:

    Class1()
    {
        Logger::WriteMessage("In Class1");
    }

    ~Class1()
    {
        Logger::WriteMessage("In ~Class1");
    }

    TEST_CLASS_INITIALIZE(ClassInitialize)
    {
        Logger::WriteMessage("In Class Initialize");
    }

    TEST_CLASS_CLEANUP(ClassCleanup)
    {
        Logger::WriteMessage("In Class Cleanup");
    }

    BEGIN_TEST_METHOD_ATTRIBUTE(Method1)
        TEST_OWNER(L"OwnerName")
        TEST_PRIORITY(1)
    END_TEST_METHOD_ATTRIBUTE()

    TEST_METHOD(Method1)
    {
        Logger::WriteMessage("In Method1");
        Assert::AreEqual(0, 0);
    }

    TEST_METHOD(Method2)
    {
        Assert::Fail(L"Fail");
    }
};
```

## <a name="see-also"></a>参照
 [テストエクスプローラーを使用したコード単体](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c)テストの[単体テスト](../test/unit-test-your-code.md)[既存の C++ アプリケーションへの単体テストの追加](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)
