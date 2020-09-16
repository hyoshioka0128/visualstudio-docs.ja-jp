---
title: C および C++ のアサーション | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [MFC], assertions
- results, checking
- result checking
- Call Stack window, assertion failures
- debugging [C++], assertions
- VERIFY macro
- assertions, side effects
- assertions
- ASSERT macro
- errors [C++], catching with assertions
- testing, error conditions with assertion statements
- _DEBUG macro
- Assertion Failed dialog box
- failures, finding locations
ms.assetid: 2d7b0121-71aa-414b-bbb6-ede1093d0bfc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: abea0f45609c74e02cd95d6c21bbe8879d46eea1
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89600216"
---
# <a name="cc-assertions"></a>C および C++ のアサーション
アサート ステートメントでは、プログラム内で true になる必要のある条件を指定します。 この条件が true にならない場合、アサーションは失敗し、プログラムの実行が中断され、[[アサートに失敗しました] ダイアログ ボックス](../debugger/assertion-failed-dialog-box.md)が表示されます。

Visual Studio は、次の構造に基づく C++ のアサート ステートメントをサポートしています。

- MFC アサーション (MFC プログラムの場合)

- [ATLASSERT](/cpp/atl/reference/debugging-and-error-reporting-macros#atlassert) (ATL を使用するプログラムの場合)

- CRT アサーション (C ランタイム ライブラリを使用するプログラムの場合)

- ANSI [assert 関数](/cpp/c-runtime-library/reference/assert-macro-assert-wassert) (その他の C/C++ プログラムの場合)

  アサーションを使用して論理エラーを検出し、操作の結果を確認することで、処理する必要があるエラー条件をテストできます。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
[アサーションのしくみ](#BKMK_How_assertions_work)

[デバッグ ビルドとリリース ビルドでのアサーション](#BKMK_Assertions_in_Debug_and_Release_builds)

[アサーション使用の副作用](#BKMK_Side_effects_of_using_assertions)

[CRT アサーション](#BKMK_CRT_assertions)

[MFC アサーション](#BKMK_MFC_assertions)

- [MFC ASSERT_VALID と CObject::AssertValid](#BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid)

- [AssertValid に関する制限事項](#BKMK_Limitations_of_AssertValid)

  [アサーションの使用](#BKMK_Using_assertions)

- [論理エラーの検出](#BKMK_Catching_logic_errors)

- [結果の確認](#BKMK_Checking_results_)

- [処理されないエラーの検索](#BKMK_Testing_error_conditions_)

## <a name="how-assertions-work"></a><a name="BKMK_How_assertions_work"></a> アサーションのしくみ
MFC ライブラリまたは C ランタイム ライブラリのアサーションによってデバッガーが停止したとき、ソース ファイルが利用可能である場合は、そのソース ファイル内のアサーションが発生した位置にジャンプします。 アサーション メッセージが [[出力] ウィンドウ](../ide/reference/output-window.md)と **[アサートに失敗しました]** ダイアログ ボックスの両方に表示されます。 後で参照するためにアサーション メッセージを保存する場合は、 **[出力]** ウィンドウからテキスト ウィンドウへコピーします。 **[出力]** ウィンドウに、他のエラー メッセージが表示されていることもあります。 アサーションが失敗した原因を突き止める手掛かりとなるため、これらのエラー メッセージをよく調べてください。

開発中にアサーションを使用してエラーを検出します。 一般的に、想定ごとに 1 つのアサーションを使用します。 たとえば、引数が NULL でないと想定した場合、アサーションを使用してその想定が正しいかどうかをテストします。

[このトピックの内容](#BKMK_In_this_topic)

## <a name="assertions-in-debug-and-release-builds"></a><a name="BKMK_Assertions_in_Debug_and_Release_builds"></a> デバッグ ビルドとリリース ビルドでのアサーション
アサート ステートメントは、`_DEBUG` が定義されている場合のみコンパイルされます。 定義されていない場合、コンパイラはアサーションを null ステートメントとして扱います。 したがって、プログラムの最終リリース バージョンではアサート ステートメントのオーバーヘッドやパフォーマンス コストはゼロになります。`#ifdef` ディレクティブを使用する必要もありません。

## <a name="side-effects-of-using-assertions"></a><a name="BKMK_Side_effects_of_using_assertions"></a> アサーション使用の副作用
アサーションをコードに追加するときは、そのアサーションに副作用がないことを確認してください。 たとえば、`nM` 値を変更する次のアサーションを考えます。

```cpp
ASSERT(nM++ > 0); // Don't do this!
```

`ASSERT` 式はプログラムのリリース バージョンでは評価されないため、`nM` の値は、デバッグ バージョンとリリース バージョンとでは異なります。 MFC でこの問題を回避するには、`ASSERT` ではなく [VERIFY](/cpp/mfc/reference/diagnostic-services#verify) マクロを使用します。 `VERIFY` によってすべてのバージョンの式が評価されますが、リリース バージョンの結果はチェックされません。

アサート ステートメントで関数を呼び出す場合は、その関数の評価によって予想外の副作用が生じることがあるため特に注意してください。

```cpp
ASSERT ( myFnctn(0)==1 ) // unsafe if myFnctn has side effects
VERIFY ( myFnctn(0)==1 ) // safe
```

`VERIFY` は、デバッグ バージョンでもリリース バージョンでも `myFnctn` を呼び出すため、安全に使用できます。 ただし、`VERIFY` を使用すると、リリース バージョンで不要な関数呼び出しのオーバーヘッドが発生します。

[このトピックの内容](#BKMK_In_this_topic)

## <a name="crt-assertions"></a><a name="BKMK_CRT_assertions"></a> CRT アサーション
CRTDBG.H ヘッダー ファイルには、アサーションによるチェックを行うための [_ASSERT マクロと _ASSERTE マクロ](/cpp/c-runtime-library/reference/assert-asserte-assert-expr-macros)が定義されています。

| マクロ | 結果 |
|------------| - |
| `_ASSERT` | 指定した式が FALSE と評価された場合、`_ASSERT` 対象のファイル名と行番号を出力します。 |
| `_ASSERTE` | `_ASSERT` と同様の結果と共に、アサートされた式の文字列形式も出力します。 |

FALSE と評価されたアサート対象の式もレポートするため、`_ASSERTE` マクロの方が強力です。 このマクロを使用すると、ソース コードを参照しなくても問題を識別できます。 ただし、アプリケーションのデバッグ バージョンに、`_ASSERTE` を使用してアサートした式ごとに文字列定数が含まれることになります。 `_ASSERTE` マクロを多用すると、これらの文字列式がかなりのメモリを占有します。 これが問題となる場合は、`_ASSERT` マクロを使用してメモリを節約してください。

`_DEBUG` が定義されている場合、`_ASSERTE` マクロは次のように定義されます。

```cpp
#define _ASSERTE(expr) \
    do { \
        if (!(expr) && (1 == _CrtDbgReport( \
            _CRT_ASSERT, __FILE__, __LINE__, #expr))) \
            _CrtDbgBreak(); \
    } while (0)
```

アサート対象の式が FALSE と評価された場合、[_CrtDbgReport](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw) が呼び出され、アサーションが失敗したことをレポートします (既定では、メッセージ ダイアログ ボックスを使用します)。 このメッセージ ダイアログ ボックスで **[再試行]** を選択すると、`_CrtDbgReport` は 1 を返し、`_CrtDbgBreak` は `DebugBreak` を使用してデバッガーを呼び出します。

### <a name="checking-for-heap-corruption"></a>ヒープ破損のチェック
次の例は、[_CrtCheckMemory](/cpp/c-runtime-library/reference/crtcheckmemory) を使用してヒープの破損をチェックします。

```cpp
_ASSERTE(_CrtCheckMemory());
```

### <a name="checking-pointer-validity"></a>ポインターの有効性チェック
次の例は、[_CrtIsValidPointer](/cpp/c-runtime-library/reference/crtisvalidpointer) を使用して、指定したメモリ範囲への読み取りまたは書き込みが有効かどうかを検証します。

```cpp
_ASSERTE(_CrtIsValidPointer( address, size, TRUE );
```

次の例は、[_CrtIsValidHeapPointer](/cpp/c-runtime-library/reference/crtisvalidheappointer) を使用して、ポインターがローカル ヒープ上のメモリを指しているかどうかを検証します (C ランタイム ライブラリのこのインスタンスによって作成および管理されるヒープを指します。DLL はライブラリの独自のインスタンスを持っているため、アプリケーション ヒープの外部に独自のヒープを所有していることになります)。 このアサーションは、null アドレスや範囲外のアドレスだけでなく、静的変数、スタック変数、その他の非ローカル メモリを指すポインターも検出します。

```cpp
_ASSERTE(_CrtIsValidPointer( myData );
```

### <a name="checking-a-memory-block"></a>メモリ ブロックのチェック
次の例は、[_CrtIsMemoryBlock](/cpp/c-runtime-library/reference/crtismemoryblock) を使用して、メモリ ブロックがローカル ヒープ上にあり、有効なブロック型があることを確認します。

```cpp
_ASSERTE(_CrtIsMemoryBlock (myData, size, &requestNumber, &filename, &linenumber));
```

[このトピックの内容](#BKMK_In_this_topic)

## <a name="mfc-assertions"></a><a name="BKMK_MFC_assertions"></a> MFC アサーション
MFC には、アサーションによるチェックを行うための [ASSERT](/previous-versions/ew16s3zc(v=vs.140)) マクロが定義されています。 また、`MFC ASSERT_VALID` 派生オブジェクトの内部状態を検証するための `CObject::AssertValid` および `CObject` も定義されています。

MFC の `ASSERT` マクロの引数がゼロまたは false に評価された場合、マクロはプログラムの実行を停止し、ユーザーに警告を表示します。それ以外の場合、プログラムの実行を続けます。

アサーションが失敗すると、アサーション対象のソース ファイル名と行番号がメッセージ ダイアログ ボックスに表示されます。 このダイアログ ボックスで [再試行] を選択すると、[AfxDebugBreak](/cpp/mfc/reference/diagnostic-services#afxdebugbreak) が呼び出され、デバッガーのためにプログラムの実行が中断されます。 この時点で、呼び出し履歴を調べるかその他のデバッガー機能を使って、アサーションが失敗した原因を確認できます。 [Just-In-Time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)を有効にしておくと、デバッガーがまだ実行されていない場合に、このダイアログ ボックスからデバッガーを起動できます。

`ASSERT` を使用して関数の戻り値をチェックする方法を次に示します。

```cpp
int x = SomeFunc(y);
ASSERT(x >= 0);   //  Assertion fails if x is negative
```

ASSERT を次のように [IsKindOf](/cpp/mfc/reference/cobject-class#iskindof) 関数と組み合わせて使用すると、関数の引数の型チェックを行うことができます。

```cpp
ASSERT( pObject1->IsKindOf( RUNTIME_CLASS( CPerson ) ) );
```

`ASSERT` マクロは、リリース バージョンではコードを生成しません。 リリース バージョンで式を評価する必要がある場合は、ASSERT の代わりに [VERIFY](/cpp/mfc/reference/diagnostic-services#verify) マクロを使用します。

### <a name="mfc-assert_valid-and-cobjectassertvalid"></a><a name="BKMK_MFC_ASSERT_VALID_and_CObject__AssertValid"></a> MFC ASSERT_VALID と CObject::AssertValid
[CObject::AssertValid](/cpp/mfc/reference/cobject-class#assertvalid) メソッドを使用すると、オブジェクトの内部状態を実行時にチェックできます。 `AssertValid` からクラスを派生させる場合、必ずしも `CObject` をオーバーライドする必要はありませんが、そうすることによって、クラスの信頼性を高めることができます。 `AssertValid` によって、オブジェクトのすべてのメンバー変数に対し、有効な値を保持しているかどうかを検証するアサーションが実行されます。 たとえば、ポインターのメンバー変数が NULL でないかどうかをチェックできます。

`AssertValid` 関数の宣言方法を次に示します。

```cpp
class CPerson : public CObject
{
protected:
    CString m_strName;
    float   m_salary;
public:
#ifdef _DEBUG
    // Override
    virtual void AssertValid() const;
#endif
    // ...
};
```

`AssertValid` をオーバーライドするときは、派生クラス独自のチェックを行う前に、基底クラスの `AssertValid` を呼び出します。 その後で、ASSERT マクロを使用して、派生クラス独自のメンバーをチェックします。次に例を示します。

```cpp
#ifdef _DEBUG
void CPerson::AssertValid() const
{
    // Call inherited AssertValid first.
    CObject::AssertValid();

    // Check CPerson members...
    // Must have a name.
    ASSERT( !m_strName.IsEmpty());
    // Must have an income.
    ASSERT( m_salary > 0 );
}
#endif
```

オブジェクトを格納しているメンバー変数がある場合は、`ASSERT_VALID` マクロを使用して、そのオブジェクトの内部状態が有効かどうかを検証します (オブジェクトのクラスが `AssertValid` をオーバーライドしている場合)。

たとえば、`CMyData` クラスのメンバー変数の 1 つに [CObList](/cpp/mfc/reference/coblist-class) が格納されているとします。 `CObList` 型の変数 `m_DataList` は、`CPerson` オブジェクトのコレクションを格納します。 `CMyData` クラスの宣言の概要を次に示します。

```cpp
class CMyData : public CObject
{
    // Constructor and other members ...
    protected:
        CObList* m_pDataList;
    // Other declarations ...
    public:
#ifdef _DEBUG
        // Override:
        virtual void AssertValid( ) const;
#endif
    // And so on ...
};
```

`AssertValid` クラスでオーバーライドした `CMyData` は次のようになります。

```cpp
#ifdef _DEBUG
void CMyData::AssertValid( ) const
{
    // Call inherited AssertValid.
    CObject::AssertValid( );
    // Check validity of CMyData members.
    ASSERT_VALID( m_pDataList );
    // ...
}
#endif
```

`CMyData` クラスでは、`AssertValid` のメカニズムを使用して、データ メンバーに格納されているオブジェクトの有効性が検証されます。 `AssertValid` クラスでオーバーライドした `CMyData` は、独自の m_pDataList メンバー変数に対して `ASSERT_VALID` マクロを呼び出します。

`CObList` クラスも `AssertValid` をオーバーライドしているため、有効性の検証はこの段階では停止しません。 このオーバーライドにより、そのクラスが表すリストの内部状態の有効性も検証されます。 つまり、`CMyData` オブジェクトの有効性を検証すると、そのメンバー変数に格納されている `CObList` リスト オブジェクトの内部状態の有効性も検証されることになります。

さらにコードを追加すると、リストに格納されている `CPerson` オブジェクトの有効性も検証できます。 たとえば、`CPersonList` から派生クラス `CObList` を生成し、`AssertValid` をオーバーライドできます。 このオーバーライドでは、`CObject::AssertValid` を呼び出した後、リストに格納されている `AssertValid` オブジェクトごとに `CPerson` を呼び出すことによってリストを反復処理します。 `CPerson` クラスは、このトピックの冒頭に示したように、既に `AssertValid` をオーバーライドしています。

これらの関数やマクロは、デバッグ バージョンのビルドに強力な機構を提供します。 リリース バージョンのビルド時には、この機構は自動的にオフになります。

### <a name="limitations-of-assertvalid"></a><a name="BKMK_Limitations_of_AssertValid"></a> AssertValid に関する制限事項
この関数は、オブジェクトが不正な場合に、アサートしてプログラムの実行を停止します。 ただし、アサートされない場合でも、問題が検出されなかったことを示すだけで、必ずしもオブジェクトに問題がないと保証されたわけではありません。

[このトピックの内容](#BKMK_In_this_topic)

## <a name="using-assertions"></a><a name="BKMK_Using_assertions"></a> アサーションの使用

### <a name="catching-logic-errors"></a><a name="BKMK_Catching_logic_errors"></a> 論理エラーの検出
プログラムの論理に従えば true になるはずの条件にアサーションを設定しておきます。 論理エラーが発生しない場合、このアサーションは特に機能しません。

たとえば、容器内の気体分子をシミュレートすると想定し、変数 `numMols` で分子の総数を表すことにします。 この数値が 0 より小さくなることはあり得ないため、次のような MFC アサート ステートメントを挿入しておきます。

```cpp
ASSERT(numMols >= 0);
```

または、次のように CRT アサーションを挿入することもできます。

```cpp
_ASSERT(numMols >= 0);
```

プログラムが正しく動作していれば、これらのステートメントは何の処理も行いません。 ただし、論理エラーにより `numMols` がゼロ未満になると、アサーションによってプログラムの実行が停止され、[[アサートに失敗しました] ダイアログ ボックス](../debugger/assertion-failed-dialog-box.md)が表示されます。

[このトピックの内容](#BKMK_In_this_topic)

### <a name="checking-results"></a><a name="BKMK_Checking_results_"></a> 結果の確認
アサーションは、ざっと見ただけでは結果がわかりにくい演算をテストする場合に有用です。

たとえば、次のコードを検討してみます。このコードは、`iMols` の指すリンク リストの内容に基づいて変数 `mols` を更新します。

```cpp
/* This code assumes that type has overloaded the != operator
 with const char *
It also assumes that H2O is somewhere in that linked list.
Otherwise we'll get an access violation... */
while (mols->type != "H2O")
{
    iMols += mols->num;
    mols = mols->next;
}
ASSERT(iMols<=numMols); // MFC version
_ASSERT(iMols<=numMols); // CRT version
```

`iMols` でカウントされる分子の数は、必ず分子の総数 `numMols` 以下であることが必要です。 このループを目で見ただけでは必ずそうなるかどうかを確認できないため、ループの後にアサート ステートメントを挿入し、その条件が満たされているかどうかをチェックします。

[このトピックの内容](#BKMK_In_this_topic)

### <a name="finding-unhandled-errors"></a><a name="BKMK_Testing_error_conditions_"></a> 処理されないエラーの検索
アサーションを使用すると、コード内のエラー処理が完了しているはずの個所で、エラー条件をチェックできます。 次の例のグラフィック ルーチンは、エラー コードを返します。または、正常終了した場合は 0 を返します。

```cpp
myErr = myGraphRoutine(a, b);

/* Code to handle errors and
   reset myErr if successful */

ASSERT(!myErr); -- MFC version
_ASSERT(!myErr); -- CRT version
```

エラー処理コードが正しく機能していれば、アサート ステートメントに達する前に、発生したエラーは処理され、`myErr` は 0 にリセットされるはずです。 `myErr` が別の値である場合、アサーションは失敗し、プログラムは停止し、[[アサートに失敗しました] ダイアログ ボックス](../debugger/assertion-failed-dialog-box.md)が表示されます。

ただし、アサート ステートメントは、エラー処理コードに代わるものではありません。 最終リリース バージョンのコードで問題となる可能性のあるアサート ステートメントの例を次に示します。

```cpp
myErr = myGraphRoutine(a, b);

/* No Code to handle errors */

ASSERT(!myErr); // Don't do this!
_ASSERT(!myErr); // Don't do this, either!
```

このコードは、アサート ステートメントを使用してエラー条件を処理しています。 その結果、`myGraphRoutine` が返すエラー コードは、最終リリース バージョンのコードでは処理されないままになります。

[このトピックの内容](#BKMK_In_this_topic)

## <a name="see-also"></a>関連項目

- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
- [マネージド コードのアサーション](../debugger/assertions-in-managed-code.md)