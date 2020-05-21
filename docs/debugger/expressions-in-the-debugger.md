---
title: デバッガーでの式 | Microsoft Docs
ms.date: 03/02/2020
ms.topic: conceptual
f1_keywords:
- vs.debug.expressions
helpviewer_keywords:
- expressions [debugger]
- debugging [Visual Studio], expressions
- expression evaluation, debugger evaluator
- native expression evaluation
- expression evaluators
- debugger, evaluating expressions
- debugging [Visual Studio], expression evaluation
- debugging [Visual Studio], variable evaluation
ms.assetid: 70f9b531-44c7-4d77-980d-5eddbf2bff41
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4ab66f288ad8442b6f2b5aab3499e2c1f3857632
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301135"
---
# <a name="expressions-in-the-visual-studio-debugger"></a>Visual Studio デバッガーでの式
Visual Studio デバッガーには式エバリュエーターという機能があり、 **[クイック ウォッチ]** ダイアログ ボックス、 **[ウォッチ]** ウィンドウ、または **[イミディエイト]** ウィンドウで式を入力するときに役立ちます。 式エバリュエーターは **[ブレークポイント]** ウィンドウなど、他のデバッガー機能でも使用できます。

以下のセクションでは、Visual Studio でサポートされている言語に対する式の評価での制限事項について説明します。

## <a name="f-expressions-are-not-supported"></a>F# の式はサポートされていません。
F# の式は認識されません。 F# のコードをデバッグする場合は、デバッガー ウィンドウまたはダイアログ ボックスに式を入力する前に、式を C# の構文に変換する必要があります。 式を F# から C# に変換するときは、C# では等価をテストするのに `==` 演算子を使用しますが、F# では単一の `=`を使用することにご注意ください。

## <a name="c-expressions"></a>C++ 式
C++ の式でのコンテキスト演算子の使用については、「 [Context Operator (C++)](../debugger/context-operator-cpp.md)」をご覧ください。

### <a name="unsupported-expressions-in-c"></a>C++ でサポートされていない式

#### <a name="constructors-destructors-and-conversions"></a>コンストラクター、デストラクター、および変換
オブジェクトに対し明示的または暗黙にコンストラクターまたはデストラクターを呼び出すことはできません。 たとえば、次の式は明示的にコンストラクターを呼び出すと、エラー メッセージが表示されます。

```C++
my_date( 2, 3, 1985 )
```

変換先がクラスである場合は、変換関数を呼び出せません。 クラスへの変換には、オブジェクトの構築が必要です。 たとえば、 `myFraction` が `CFraction`のインスタンスであり、変換関数演算子 `FixedPoint`を定義する場合、次の式はエラーになります。

```C++
(FixedPoint)myFraction
```

new 演算子または delete 演算子を呼び出すことはできません。 たとえば、次の式はサポートされません。

```C++
new Date(2,3,1985)
```

#### <a name="preprocessor-macros"></a>プリプロセッサ マクロ
デバッガーではプリプロセッサ マクロはサポートされていません。 たとえば定数 `VALUE` が `#define VALUE 3`として宣言されている場合、 `VALUE` ウォッチ **ウィンドウで** を使用することはできません。 この制約を回避するには、可能な場合は常に `#define`を列挙体と関数に置き換えてください。

### <a name="using-namespace-declarations"></a>名前空間の宣言の使用
`using namespace` 宣言は使用できません。  現在の名前空間外部の型名または変数にアクセスするには、完全修飾名を使用する必要があります。

### <a name="anonymous-namespaces"></a>匿名の名前空間
匿名の名前空間はサポートされていません。 次のコードを使用する場合、ウォッチ ウィンドウに `test` を追加できません。

```C++
namespace mars
{
    namespace
    {
        int test = 0;
    }
}
int main()
{
    // Adding a watch on test does not work.
    mars::test++;
    return 0;
}

```

### <a name="using-debugger-intrinsic-functions-to-maintain-state"></a><a name="BKMK_Using_debugger_intrinisic_functions_to_maintain_state"></a> デバッガーの組み込み関数による状態の保持
デバッガーの組み込み関数を使用すると、アプリケーションの状態を変更せずに、式の中で特定の C/C++ 関数を呼び出すことができます。

デバッガーの組み込み関数には次の特徴があります。

- 安全なことが保証されています。デバッガーの組み込み関数を実行しても、デバッグ対象のプロセスは破損しません。

- すべての式で使用できます。副作用と関数評価が許可されていないシナリオでも使用できます。

- ミニダンプのデバッグ中など、通常の関数呼び出しができないシナリオでも機能します。

  デバッガーの組み込み関数は、式の評価をより便利にすることもできます。 たとえば、ブレークポイント条件に記述する際、 `strncmp(str, "asd")` は `str[0] == 'a' && str[1] == 's' && str[2] == 'd'`よりもはるかに簡単です。 )

|区分|組み込み関数|
|----------|-------------------------|
|**文字列長**|[strlen、wcslen](https://docs.microsoft.com/cpp/c-runtime-library/reference/strlen-wcslen-mbslen-mbslen-l-mbstrlen-mbstrlen-l)、[strnlen、wcsnlen](https://docs.microsoft.com/cpp/c-runtime-library/reference/strnlen-strnlen-s)|
|**文字列比較**|[strcmp、wcscmp](https://docs.microsoft.com/cpp/c-runtime-library/reference/strcmp-wcscmp-mbscmp)、[stricmp、wcsicmp](https://docs.microsoft.com/cpp/c-runtime-library/reference/stricmp-wcsicmp)、[_stricmp、_strcmpi、_wcsicmp、_wcscmpi](https://docs.microsoft.com/cpp/c-runtime-library/reference/stricmp-wcsicmp-mbsicmp-stricmp-l-wcsicmp-l-mbsicmp-l)、[strncmp、wcsncmp](https://docs.microsoft.com/cpp/c-runtime-library/reference/strncmp-wcsncmp-mbsncmp-mbsncmp-l)、[strnicmp、wcsnicmp](https://docs.microsoft.com/cpp/c-runtime-library/reference/strnicmp-wcsnicmp)、[_strnicmp、_wcsnicmp](https://docs.microsoft.com/cpp/c-runtime-library/reference/strnicmp-wcsnicmp-mbsnicmp-strnicmp-l-wcsnicmp-l-mbsnicmp-l)|
|**文字列検索**|[strchr、wcschr](https://docs.microsoft.com/cpp/c-runtime-library/reference/strchr-wcschr-mbschr-mbschr-l)、[memchr、wmemchr](https://docs.microsoft.com/cpp/c-runtime-library/reference/memchr-wmemchr)、[strstr、wcsstr](https://docs.microsoft.com/cpp/c-runtime-library/reference/strstr-wcsstr-mbsstr-mbsstr-l)|
|**Win32**|[CoDecodeProxy](https://docs.microsoft.com/windows/win32/api/combaseapi/nf-combaseapi-codecodeproxy)、[DecodePointer](https://docs.microsoft.com/previous-versions/bb432242%28v%3dvs.85%29)、[GetLastError](https://docs.microsoft.com/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror)、[TlsGetValue](https://docs.microsoft.com/windows/win32/api/processthreadsapi/nf-processthreadsapi-tlsgetvalue)|
|**Windows 8**|[RoInspectCapturedStackBackTrace](https://docs.microsoft.com/windows/win32/api/roerrorapi/nf-roerrorapi-roinspectcapturedstackbacktrace)、[WindowsCompareStringOrdinal](https://docs.microsoft.com/windows/win32/api/winstring/nf-winstring-windowscomparestringordinal)、[WindowsGetStringLen](https://docs.microsoft.com/windows/win32/api/winstring/nf-winstring-windowsgetstringlen)、[WindowsGetStringRawBuffer](https://docs.microsoft.com/windows/win32/api/winstring/nf-winstring-windowsgetstringrawbuffer)<br /><br /> これらの関数では、デバッグ対象のプロセスが Windows 8 上で動作している必要があります。 Windows 8 デバイスから生成されたダンプ ファイルをデバッグする際も、Visual Studio コンピューターが Windows 8 を実行している必要があります。 ただし、Windows 8 デバイスをリモートでデバッグする場合は、Visual Studio コンピューターが Windows 7 を実行していてもかまいません。|
|**その他**|__log2 // 指定した整数の底 2 の対数 (最も近い整数に切り捨てられます) を返します。<br /><br />__findNonNull、DecodeHString、DecodeWinRTRestrictedException、DynamicCast、DynamicMemberLookup、GetEnvBlockLength<br /><br />Stdext_HashMap_Int_OperatorBracket_idx、Std_UnorderedMap_Int_OperatorBracket_idx<br /><br />ConcurrencyArray_OperatorBracket_idx // Concurrency::array<>::operator[index<>] および operator(index<>)<br /><br />ConcurrencyArray_OperatorBracket_int // Concurrency::array<>::operator(int, int, ...)<br /><br />ConcurrencyArray_OperatorBracket_tidx // Concurrency::array<>::operator[tiled_index<>] および operator(tiled_index<>)<br /><br />ConcurrencyArrayView_OperatorBracket_idx // Concurrency::array_view<>::operator[index<>] および operator(index<>)<br /><br />ConcurrencyArrayView_OperatorBracket_int // Concurrency::array_view<>::operator(int, int, ...)<br /><br />ConcurrencyArrayView_OperatorBracket_tidx // Concurrency::array_view<>::operator[tiled_index<>] および operator(tiled_index<>)<br /><br />TreeTraverse_Init // 新しいツリー トラバーサルを初期化します<br /><br />TreeTraverse_Next // ツリー内のノードを返します<br /><br />TreeTraverse_Skip // 保留中のツリー トラバーサル内のノードをスキップします|

## <a name="ccli---unsupported-expressions"></a>C++/CLI - サポートされていない式

- ポインターを使用するキャスト、およびユーザー定義のキャストはサポートされていません。

- オブジェクトの比較と代入はサポートされていません。

- オーバーロードされた演算子とオーバーロードされた関数はサポートされていません。

- ボックス化とボックス化解除はサポートされていません。

- `Sizeof` 演算子はサポートされていません。

## <a name="c---unsupported-expressions"></a>C# - サポートされていない式

### <a name="dynamic-objects"></a>動的オブジェクト
デバッガー式では、静的に型指定された変数を動的として使用できます。 <xref:System.Dynamic.IDynamicMetaObjectProvider> を実装するオブジェクトがウォッチ ウィンドウで評価されると、[動的ビュー] ノードが追加されます。 [動的ビュー] ノードにはオブジェクトのメンバーが表示されますが、そのメンバーの値を編集することはできません。

動的オブジェクトでは、以下の機能はサポートされていません。

- 複合演算子 `+=`、 `-=`、 `%=`、 `/=`、 `*=`

- 多数のキャスト (数値キャスト、型引数キャストなど)

- 3 つ以上の引数を指定したメソッド呼び出し

- 3 つ以上の引数を指定したプロパティの getter

- 引数を指定したプロパティの setter

- インデクサーへの割り当て

- ブール演算子 `&&` および `||`

### <a name="anonymous-methods"></a>匿名メソッド
匿名メソッドの新規作成はサポートされていません。

## <a name="visual-basic---unsupported-expressions"></a>Visual Basic - サポートされていない式

### <a name="dynamic-objects"></a>動的オブジェクト
デバッガー式では、静的に型指定された変数を動的として使用できます。 <xref:System.Dynamic.IDynamicMetaObjectProvider> を実装するオブジェクトがウォッチ ウィンドウで評価されると、[動的ビュー] ノードが追加されます。 [動的ビュー] ノードにはオブジェクトのメンバーが表示されますが、そのメンバーの値を編集することはできません。

動的オブジェクトでは、以下の機能はサポートされていません。

- 複合演算子 `+=`、 `-=`、 `%=`、 `/=`、 `*=`

- 多数のキャスト (数値キャスト、型引数キャストなど)

- 3 つ以上の引数を指定したメソッド呼び出し

- 3 つ以上の引数を指定したプロパティの getter

- 引数を指定したプロパティの setter

- インデクサーへの割り当て

- ブール演算子 `&&` および `||`

### <a name="local-constants"></a>ローカル定数
ローカル定数はサポートされていません。

### <a name="import-aliases"></a>インポート エイリアス
インポート エイリアスはサポートされていません。

### <a name="variable-declarations"></a>変数宣言
デバッガー ウィンドウでは、明示的に新しい変数を宣言できません。 ただし、 **イミディエイト** ウィンドウ内で新しい暗黙的な変数を割り当てることはできます。 このように暗黙的な変数のスコープは、デバッグ セッションに制限されるため、デバッガーの外部ではアクセスできません。 たとえば、ステートメント `o = 5` によって、新しい変数 `o` が暗黙的に作成され、値 5 が割り当てられます。 このように暗黙的な変数は、デバッガーで型を推測できなければ、型 **Object** になります。

### <a name="unsupported-keywords"></a>サポートされないキーワード

- `AddressOf`

- `End`

- `Error`

- `Exit`

- `Goto`

- `On Error`

- `Resume`

- `Return`

- `Select/Case`

- `Stop`

- `SyncLock`

- `Throw`

- `Try/Catch/Finally`

- `With`

- 名前空間またはモジュール レベルのキーワード ( `End Sub` や `Module`など)。

## <a name="see-also"></a>関連項目
- [C++ の書式指定子](../debugger/format-specifiers-in-cpp.md)
- [Context Operator (C++)](../debugger/context-operator-cpp.md)
- [C++ の書式指定子](../debugger/format-specifiers-in-csharp.md)
- [擬似変数](../debugger/pseudovariables.md)
