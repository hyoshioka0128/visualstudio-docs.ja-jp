---
title: Microsoft.VisualStudio.TestTools.CppUnitTestFramework API
ms.date: 09/27/2019
ms.topic: reference
ms.author: corob
manager: jillfra
ms.workload:
- multiple
author: corob-msft
ms.openlocfilehash: 16ea629312237dd859e9eb1aad21b9b219de7229
ms.sourcegitcommit: 5ab22b8601db9c420691f8e57abe140e837aa720
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82109430"
---
# <a name="microsoftvisualstudiotesttoolscppunittestframework-api-reference"></a>Microsoft.VisualStudio.TestTools.CppUnitTestFramework API リファレンス

このトピックでは `Microsoft::VisualStudio::CppUnitTestFramework` の名前空間のパブリック メンバーの一覧を示します。 Microsoft ネイティブ単体テスト フレームワークに基づいて C++ の単体テストを作成するには、これらの API を使います。 トピックの最後には「[使用例](#example)」があります。

ヘッダー ファイルと lib ファイルは *\<Visual Studio インストール フォルダー>\VC\Auxiliary\VS\UnitTest* にあります。

ヘッダーと lib のパスは、ネイティブ テスト プロジェクトで自動的に構成されます。

## <a name="in-this-topic"></a><a name="In_this_topic"></a> このトピックの内容

[CppUnitTest.h](#cppUnitTest_h)

- [テスト クラスとメソッドを作成する](#create_test_classes_and_methods)

- [初期化とクリーンアップ](#Initialize_and_cleanup)

  - [テスト メソッド](#test_methods)

  - [テスト クラス](#test_classes)

  - [テスト モジュール](#test_modules)

- [テスト属性を作成する](#create_test_attributes)

  - [テスト メソッド属性](#test_method_attributes)

  - [テスト クラス属性](#test_class_attributes)

  - [テスト モジュール属性](#test_module_attributes)

  - [定義済みの属性](#pre_defined_attributes)

    [CppUnitTestAssert.h](#cppUnitTestAssert_h)

  - [一般的なアサート](#general_asserts)

    - [等しい](#general_are_equal)

    - [等しくない](#general_are_not_equal)

    - [同じである](#general_are_same)

    - [同じではない](#general_are_not_same)

    - [Null である](#general_is_null)

    - [Null ではない](#general_is_not_null)

    - [True である](#general_is_True)

    - [False である](#general_is_false)

    - [失敗](#general_Fail)

  - [Windows ランタイム アサート](#winrt_asserts)

    - [等しい](#winrt_are_equal)

    - [同じである](#winrt_are_same)

    - [等しくない](#winrt_are_not_equal)

    - [同じではない](#winrt_are_not_same)

    - [Null である](#winrt_is_null)

    - [Null ではない](#winrt_is_not_null)

  - [例外アサート](#exception_asserts)

    - [例外を想定する](#expect_exception)

      [CppUnitTestLogger.h](#cppunittestlogger_h)

    - [Logger](#logger)

    - [メッセージの書き込み](#write_message)

  - [使用例](#example)

## <a name="cppunittesth"></a><a name="cppUnitTest_h"></a> CppUnitTest.h

### <a name="create-test-classes-and-methods"></a><a name="create_test_classes_and_methods"></a> テスト クラスとメソッドを作成する

```cpp
TEST_CLASS(className)
```

テスト メソッドを含む各クラスに必要です。 *className* をテスト クラスとして識別します。 `TEST_CLASS` は名前空間範囲で宣言する必要があります。

```cpp
TEST_METHOD(methodName)
{
    // test method body
}
```

*methodName* をテスト メソッドとして定義します。 `TEST_METHOD` はメソッドのクラスのスコープ内で宣言する必要があります。

### <a name="initialize-and-cleanup"></a><a name="Initialize_and_cleanup"></a> 初期化とクリーンアップ

#### <a name="test-methods"></a><a name="test_methods"></a> テスト メソッド

```cpp
TEST_METHOD_INITIALIZE(methodName)
{
    // method initialization code
}
```

*methodName* を各テスト メソッドが実行される前に実行するメソッドとして定義します。 `TEST_METHOD_INITIALIZE` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

```cpp
TEST_METHOD_CLEANUP(methodName)
{
    // test method cleanup  code
}
```

*methodName* を各テスト メソッドの実行後に実行するメソッドとして定義します。 `TEST_METHOD_CLEANUP` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

#### <a name="test-classes"></a><a name="test_classes"></a> テスト クラス

```cpp
TEST_CLASS_INITIALIZE(methodName)
{
    // test class initialization  code
}
```

*methodName* を各テスト クラスの作成前に実行するメソッドとして定義します。 `TEST_CLASS_INITIALIZE` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

```cpp
TEST_CLASS_CLEANUP(methodName)
{
    // test class cleanup  code
}
```

*methodName* を各テスト クラスの作成後に実行するメソッドとして定義します。 `TEST_CLASS_CLEANUP` はテスト クラスで一度だけ定義でき、テスト クラスのスコープ内で定義する必要があります。

#### <a name="test-modules"></a><a name="test_modules"></a> テスト モジュール

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

### <a name="create-test-attributes"></a><a name="create_test_attributes"></a> テスト属性を作成する

#### <a name="test-method-attributes"></a><a name="test_method_attributes"></a> テスト メソッドの属性

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(testMethodName)
    TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_METHOD_ATTRIBUTE()
```

テスト メソッド *testMethodName* に、1 つ以上の `TEST_METHOD_ATTRIBUTE` マクロで定義された属性を追加します。

`TEST_METHOD_ATTRIBUTE` マクロは名前 *attributeName* と値 *attributeValue* を持つ属性を定義します。

#### <a name="test-class-attributes"></a><a name="test_class_attributes"></a> テスト クラス属性

```cpp
BEGIN_TEST_CLASS_ATTRIBUTE(testClassName)
    TEST_CLASS_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_CLASS_ATTRIBUTE()
```

テスト クラス *testClassName* に、`TEST_CLASS_ATTRIBUTE` の 1 つ以上のマクロで定義された属性を追加します。

`TEST_CLASS_ATTRIBUTE` マクロは名前 *attributeName* と値 *attributeValue* を持つ属性を定義します。

#### <a name="test-module-attributes"></a><a name="test_module_attributes"></a> テスト モジュール属性

```cpp
BEGIN_TEST_MODULE_ATTRIBUTE(testModuleName)
    TEST_MODULE_ATTRIBUTE(attributeName, attributeValue)
    ...
END_TEST_MODULE_ATTRIBUTE()
```

テスト モジュール *testModuleName* に、`TEST_MODULE_ATTRIBUTE` の 1 つ以上のマクロで定義された属性を追加します。

`TEST_MODULE_ATTRIBUTE` マクロは名前 *attributeName* と値 *attributeValue* を持つ属性を定義します。

#### <a name="pre-defined-attributes"></a><a name="pre_defined_attributes"></a> 定義済みの属性

一般的なケースに便利なように、以下の定義済み属性マクロが提供されています。 これらは、上で説明したマクロ `TEST_METHOD_ATTRIBUTE` の代わりに使用できます。

```cpp
TEST_OWNER(ownerAlias)
```

名前 `Owner` と属性値 *ownerAlias* で `TEST_METHOD_ATTRIBUTE` を定義します。

```cpp
TEST_DESCRIPTION(description)
```

名前 `Description` と属性値 *description* で `TEST_METHOD_ATTRIBUTE` を定義します。

```cpp
TEST_PRIORITY(priority)
```

名前 `Priority` と属性値 *priority* で `TEST_METHOD_ATTRIBUTE` を定義します。

```cpp
TEST_WORKITEM(workitem)
```

名前 `WorkItem` と属性値 *workItem* で `TEST_METHOD_ATTRIBUTE` を定義します。

```cpp
TEST_IGNORE()
```

名前 `Ignore` と属性値 `true` で `TEST_METHOD_ATTRIBUTE` を定義します。

## <a name="cppunittestasserth"></a><a name="cppUnitTestAssert_h"></a> CppUnitTestAssert.h

### <a name="general-asserts"></a><a name="general_asserts"></a> 一般的なアサート

#### <a name="are-equal"></a><a name="general_are_equal"></a> 等しい
2 つのオブジェクトが等しいことを確認します

```cpp
template<typename T>
static void Assert::AreEqual(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの倍精度小数点数が等しいことを確認します

```cpp
static void Assert::AreEqual(
    double expected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの浮動小数点数が等しいことを確認します

```cpp
static void Assert::AreEqual(
    float expected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの char* 文字列が等しいことを確認します

```cpp
static void Assert::AreEqual(
    const char* expected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの w_char* 文字列が等しいことを確認します

```cpp
static void Assert::AreEqual(
    const wchar_t* expected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-not-equal"></a><a name="general_are_not_equal"></a> 等しくない
2 つの倍精度小数点数が等しくないことを確認します

```cpp
static void Assert::AreNotEqual(
    double notExpected,
    double actual,
    double tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの浮動小数点数が等しくないことを確認します

```cpp
static void Assert::AreNotEqual(
    float notExpected,
    float actual,
    float tolerance,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの char* 文字列が等しくないことを確認します

```cpp
static void Assert::AreNotEqual(
    const char* notExpected,
    const char* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

2 つの w_char* 文字列が等しくないことを確認します

```cpp
static void Assert::AreNotEqual(
    const wchar_t* notExpected,
    const wchar_t* actual,
    bool ignoreCase = false,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

演算子 == に基づいて、2 つの参照が等しくないことを確認します

```cpp
template<typename T>
static void Assert::AreNotEqual(
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-same"></a><a name="general_are_same"></a> 同じである
2 つの参照が同じオブジェクト インスタンス (ID) を参照していることを確認します。

```cpp
template<typename T>
static void Assert::AreSame(
    const T& expected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="are-not-same"></a><a name="general_are_not_same"></a> 同じではない
2 つの参照が同じオブジェクト インスタンス (ID) を参照していないことを確認します。

```cpp
template<typename T>
static void Assert::AreNotSame (
    const T& notExpected,
    const T& actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-null"></a><a name="general_is_null"></a> Null である
ポインターが NULL であることを確認します。

```cpp
template<typename T>
static void Assert::IsNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-not-null"></a><a name="general_is_not_null"></a> Null ではない
ポインターが NULL ではないことを確認します

```cpp
template<typename T>
static void Assert::IsNotNull(
    const T* actual,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-true"></a><a name="general_is_True"></a> True である
条件が true であることを確認します

```cpp
static void Assert::IsTrue(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="is-false"></a><a name="general_is_false"></a> False である
条件が false であることを確認します

```cpp
static void Assert::IsFalse(
    bool condition,
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

#### <a name="fail"></a><a name="general_Fail"></a> 失敗
テスト ケースの結果が失敗するよう強制します

```cpp
static void Assert::Fail(
    const wchar_t* message = NULL,
    const __LineInfo* pLineInfo = NULL)
```

### <a name="windows-runtime-asserts"></a><a name="winrt_asserts"></a> Windows ランタイム アサート

#### <a name="are-equal"></a><a name="winrt_are_equal"></a> 等しい
2 つの Windows ランタイム ポインターが等しいことを確認します。

```cpp
template<typename T>
static void Assert::AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

2 つの Platform::String^ 文字列が等しいことを確認します。

```cpp
template<typename T>
static void Assert::AreEqual(
    T^ expected,
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-same"></a><a name="winrt_are_same"></a> 同じである
2 つの Windows ランタイム参照が同じオブジェクトを参照していることを確認します。

```cpp
template<typename T>
static void Assert::AreSame(
    T% expected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-not-equal"></a><a name="winrt_are_not_equal"></a> 等しくない
2 つの Windows ランタイム ポインターが等しくないことを確認します。

```cpp
template<typename T>
static void Assert::AreNotEqual(
    T^ notExpected,
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

2 つの Platform::String^ 文字列が等しくないことを確認します。

```cpp
static void Assert::AreNotEqual(
    Platform::String^ notExpected,
    Platform::String^ actual,
    bool ignoreCase = false,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="are-not-same"></a><a name="winrt_are_not_same"></a> 同じではない
2 つの Windows ランタイム参照が同じオブジェクトを参照していないことを確認します。

```cpp
template<typename T>
static void Assert::AreNotSame(
    T% notExpected,
    T% actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="is-null"></a><a name="winrt_is_null"></a> Null である
Windows ランタイム ポインターが nullptr であることを確認します。

```cpp
template<typename T>
static void Assert::IsNull(
    T^ actual,
    Platform::String^ message = nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

#### <a name="is-not-null"></a><a name="winrt_is_not_null"></a> Null ではない
Windows ランタイム ポインターが nullptr ではないことを確認します。

```cpp
template<typename T>
static void Assert::IsNotNull(
    T^ actual,
    Platform::String^ message= nullptr,
    const __LineInfo* pLineInfo= nullptr)
```

### <a name="exception-asserts"></a><a name="exception_asserts"></a> 例外アサート

#### <a name="expect-exception"></a><a name="expect_exception"></a> 例外を想定する
関数が例外を発生させることを確認します。

```cpp
template<typename _EXPECTEDEXCEPTION, typename _FUNCTOR>
static void Assert::ExpectException(
    _FUNCTOR functor,
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo= NULL)
```

関数が例外を発生させることを確認します。

```cpp
template<typename _EXPECTEDEXCEPTION, typename _RETURNTYPE>
    static void Assert::ExpectException(
    _RETURNTYPE (*func)(),
    const wchar_t* message= NULL,
    const __LineInfo* pLineInfo = NULL)
```

## <a name="cppunittestloggerh"></a><a name="cppunittestlogger_h"></a> CppUnitTestLogger.h

### <a name="logger"></a><a name="logger"></a> Logger
ロガー クラスには、**出力ウィンドウ**に書き込むための静的メソッドが含まれます。

### <a name="write-message"></a><a name="write_message"></a> メッセージの書き込み
**出力ウィンドウ**に文字列を書き込む

```cpp
static void Logger::WriteMessage(const wchar_t* message)
```

```cpp
static void Logger::WriteMessage(const char* message)
```

## <a name="example"></a><a name="example"></a> 「例」
以下のコードは VSCppUnit の使用例です。 属性メタデータ、フィクスチャ、アサーションのある単体テスト、およびカスタム ログの例が含まれます。

```cpp
// USAGE EXAMPLE

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

## <a name="see-also"></a>関連項目

- [コードの単体テスト](../test/unit-test-your-code.md)
- [C/C++ 用の単体テストの記述](writing-unit-tests-for-c-cpp.md)
