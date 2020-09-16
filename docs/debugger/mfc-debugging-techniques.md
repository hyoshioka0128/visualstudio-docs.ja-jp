---
title: MFC のデバッグ技法 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- AfxEnableMemoryTracking
- CMemoryState
- delayFreeMemDF
- checkAlwaysMemDF
- vs.debug.mfc
- vs.debug.objects.dump
- vs.debug.memory.dump
- allocMemDF
- afxMemDF
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [MFC]
ms.assetid: b154fc31-5e90-4734-8cbd-58dd9fe1f750
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 06b42dbf31a8b5f4cb66de047bc1e08a4f840353
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89600243"
---
# <a name="mfc-debugging-techniques"></a>MFC のデバッグ技術
MFC プログラムをデバッグする場合は、次のデバッグ技術が役立ちます。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
[AfxDebugBreak](#BKMK_AfxDebugBreak)

[TRACE マクロ](#BKMK_The_TRACE_macro)

[MFC でのメモリ リークの検出](#BKMK_Memory_leak_detection_in_MFC)

- [メモリ割り当ての追跡](#BKMK_Tracking_memory_allocations)

- [メモリ診断の有効化](#BKMK_Enabling_memory_diagnostics)

- [メモリのスナップショットの取得](#BKMK_Taking_memory_snapshots)

- [メモリ統計情報の表示](#BKMK_Viewing_memory_statistics)

- [オブジェクト ダンプの取得](#BKMK_Taking_object_dumps)

  - [メモリ ダンプの解釈](#BKMK_Interpreting_memory_dumps)

  - [オブジェクト ダンプのカスタマイズ](#BKMK_Customizing_object_dumps)

  - [MFC デバッグ ビルドのサイズの縮小](#BKMK_Reducing_the_size_of_an_MFC_Debug_build)

  - [選択したモジュールのデバッグ情報を持つ MFC アプリケーションのビルド](#BKMK_Building_an_MFC_app_with_debug_information_for_selected_modules)

## <a name="afxdebugbreak"></a><a name="BKMK_AfxDebugBreak"></a> AfxDebugBreak
MFC には、ソース コードにハードコーディングされたブレークポイント用に [AfxDebugBreak](/cpp/mfc/reference/diagnostic-services#afxdebugbreak) 関数が用意されています。

```cpp
AfxDebugBreak( );
```

Intel プラットフォームでは、 `AfxDebugBreak` は次のコードを生成します。このコードは、カーネル コードではなく、ソース コードでプログラムの実行を停止します。

```cpp
_asm int 3
```

他のプラットフォームでは、 `AfxDebugBreak` は単純に `DebugBreak`を呼び出します。

`AfxDebugBreak` ステートメントは、リリース ビルドの作成時には必ず削除してください。または、 `#ifdef _DEBUG` を使用して囲んでください。

[このトピックの内容](#BKMK_In_this_topic)

## <a name="the-trace-macro"></a><a name="BKMK_The_TRACE_macro"></a> TRACE マクロ
プログラムからのメッセージをデバッガーの [[出力] ウィンドウ](../ide/reference/output-window.md)に表示するには、 [ATLTRACE](/previous-versions/6xkxyz08(v=vs.140)) マクロ、または MFC の [TRACE](/previous-versions/6w95a4ha(v=vs.140)) マクロを使用します。 [アサーション](../debugger/c-cpp-assertions.md)と同様に、トレース マクロはプログラムのデバッグ バージョンでだけ有効です。リリース バージョンでコンパイルされた場合は無効になります。

**TRACE** マクロの使用例を次に示します。 `printf`と同様に、 **TRACE** マクロは多数の引数を処理できます。

```cpp
int x = 1;
int y = 16;
float z = 32.0;
TRACE( "This is a TRACE statement\n" );

TRACE( "The value of x is %d\n", x );

TRACE( "x = %d and y = %d\n", x, y );

TRACE( "x = %d and y = %x and z = %f\n", x, y, z );
```

TRACE マクロでは、char\* パラメーターと wchar_twchar_t\* パラメーターの両方が適切に処理されます。 TRACE マクロと異なる型の文字列パラメーターを組み合わせて使用する例を次に示します。

```cpp
TRACE( "This is a test of the TRACE macro that uses an ANSI string: %s %d\n", "The number is:", 2);

TRACE( L"This is a test of the TRACE macro that uses a UNICODE string: %s %d\n", L"The number is:", 2);

TRACE( _T("This is a test of the TRACE macro that uses a TCHAR string: %s %d\n"), _T("The number is:"), 2);
```

**TRACE** マクロの詳細については、「 [診断サービス](/cpp/mfc/reference/diagnostic-services)」を参照してください。

[このトピックの内容](#BKMK_In_this_topic)

## <a name="detecting-memory-leaks-in-mfc"></a><a name="BKMK_Memory_leak_detection_in_MFC"></a> MFC でのメモリ リークの検出
MFC には、割り当てられた後、解放されていないメモリを検出するためのクラスと関数が用意されています。

### <a name="tracking-memory-allocations"></a><a name="BKMK_Tracking_memory_allocations"></a> メモリ割り当ての追跡
MFC では、通常 [new](/previous-versions/tz7sxz99(v=vs.140)) 演算子が使用される場所で **DEBUG_NEW** マクロを使用して、メモリ リークの位置を特定できます。 プログラムのデバッグ バージョンでは、 `DEBUG_NEW` はメモリを割り当てた各オブジェクトのファイル名と行番号を記録します。 プログラムのリリース バージョンをコンパイルするときは、 `DEBUG_NEW` は単に **new** 演算として機能し、ファイル名や行番号の情報を記録しません。 したがって、プログラムのリリース バージョンの実行速度が低下することはありません。

ソース ファイルで次のように `DEBUG_NEW` マクロを定義すると、プログラム全体を書き直さなくても、 **new**の代わりにこのマクロを使用できます。

```cpp
#define new DEBUG_NEW
```

[オブジェクトのダンプ](#BKMK_Taking_object_dumps)を実行すると、 `DEBUG_NEW` で割り当てられた各オブジェクトについて、メモリが割り当てられた場所のファイル名と行番号が表示されます。この情報を使用して、メモリ リークの原因となったコードを特定できます。

MFC フレームワークのデバッグ バージョンでは自動的に `DEBUG_NEW` が使用されますが、プログラマが記述するコードでは自動的には使用されません。 `DEBUG_NEW`を使用するには、 `DEBUG_NEW` を明示的に使用するか、上記のように **#define new** を使用する必要があります。

[このトピックの内容](#BKMK_In_this_topic)

### <a name="enabling-memory-diagnostics"></a><a name="BKMK_Enabling_memory_diagnostics"></a> メモリ診断の有効化
メモリ診断機能を使用するには、あらかじめ診断トレースを有効にしておく必要があります。

**メモリ診断を有効または無効にするには**

- グローバル関数 [AfxEnableMemoryTracking](/previous-versions/hzsxb6e8(v=vs.140)) を呼び出して、診断メモリ アロケーターを有効または無効にします。 デバッグ ライブラリでは既定でメモリの診断が行われるため、通常はメモリの診断を一時的にオフにするためにこの関数を使用します。診断をオフにすると、プログラムの実行速度が上がり、診断出力の量が少なくなります。

  **afxMemDF を使用して特定のメモリ診断機能を選択するには**

- メモリ診断機能をより細かく制御するには、MFC のグローバル変数 [afxMemDF](/previous-versions/ahe4a83t(v=vs.140))に値を設定することにより、個々のメモリ診断機能を個別にオン、オフします。 この変数には、 **afxMemDF**列挙型で指定される次の値を設定できます。

  |[値]|説明|
  |-----------|-----------------|
  |**allocMemDF**|診断メモリ アロケーターをオンにします (既定)。|
  |**delayFreeMemDF**|`delete` や `free` が呼び出された場合に、プログラムが終了するまでメモリの解放を遅らせます。 これにより、プログラムで必要とする最大量のメモリが割り当てられます。|
  |**checkAlwaysMemDF**|メモリが割り当てられるたび、または解放されるたびに、 [AfxCheckMemory](/cpp/mfc/reference/diagnostic-services#afxcheckmemory) を呼び出します。|

  これらの値は、次のように論理 OR 演算を行うことにより、組み合わせて指定できます。

  ```C++
  afxMemDF = allocMemDF | delayFreeMemDF | checkAlwaysMemDF;
  ```

  [このトピックの内容](#BKMK_In_this_topic)

### <a name="taking-memory-snapshots"></a><a name="BKMK_Taking_memory_snapshots"></a> メモリのスナップショットの取得

1. [CMemoryState](/previous-versions/visualstudio/visual-studio-2010/2ads32e2(v=vs.100)) オブジェクトを作成し、 [CMemoryState::Checkpoint](/cpp/mfc/reference/cmemorystate-structure#checkpoint) メンバー関数を呼び出します。 これにより、メモリの最初のスナップショットが作成されます。

2. プログラムでメモリの割り当てと解放が行われた後、別の `CMemoryState` オブジェクトを作成し、このオブジェクトの `Checkpoint` を呼び出します。 これにより、メモリ状態の 2 番目のスナップショットが取得されます。

3. 3 番目の `CMemoryState` オブジェクトを作成し、そのメンバー関数 [CMemoryState::Difference](/cpp/mfc/reference/cmemorystate-structure#difference) を呼び出します。このとき、前に作成した 2 つの `CMemoryState` オブジェクトを引数として渡します。 2 つのメモリ状態に違いがある場合、 `Difference` 関数は 0 以外の値を返します。 この値は、解放されていないメモリ ブロックがあることを示します。

    コードの例を次に示します。

    ```cpp
    // Declare the variables needed
    #ifdef _DEBUG
        CMemoryState oldMemState, newMemState, diffMemState;
        oldMemState.Checkpoint();
    #endif

        // Do your memory allocations and deallocations.
        CString s("This is a frame variable");
        // The next object is a heap object.
        CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );

    #ifdef _DEBUG
        newMemState.Checkpoint();
        if( diffMemState.Difference( oldMemState, newMemState ) )
        {
            TRACE( "Memory leaked!\n" );
        }
    #endif
    ```

    メモリ チェック用のステートメントが **#ifdef _DEBUG / #endif** ブロックで囲まれていることに注意してください。これによって、このコードはプログラムのデバッグ バージョンでのみコンパイルされます。

    メモリ リークが発生していることを確認できたので、別のメンバー関数 [CMemoryState::DumpStatistics](/cpp/mfc/reference/cmemorystate-structure#dumpstatistics) を使用してメモリ リークの位置を特定できます。

    [このトピックの内容](#BKMK_In_this_topic)

### <a name="viewing-memory-statistics"></a><a name="BKMK_Viewing_memory_statistics"></a> メモリ統計情報の表示
[CMemoryState::Difference](/cpp/mfc/reference/cmemorystate-structure#difference) 関数は、2 つのメモリ状態オブジェクトを参照し、1 つ目の状態から 2 つ目の状態までの間にヒープから解放されなかったオブジェクトを検出します。 メモリのスナップショットを取得して、それらのメモリを `CMemoryState::Difference`を使用して比較した後、 [CMemoryState::DumpStatistics](/cpp/mfc/reference/cmemorystate-structure#dumpstatistics) を呼び出すと、解放されなかったオブジェクトに関する情報を取得できます。

次に例を示します。

```cpp
if( diffMemState.Difference( oldMemState, newMemState ) )
{
    TRACE( "Memory leaked!\n" );
    diffMemState.DumpStatistics();
}
```

このコード例では、次の情報がダンプされます。

```cpp
0 bytes in 0 Free Blocks
22 bytes in 1 Object Blocks
45 bytes in 4 Non-Object Blocks
Largest number used: 67 bytes
Total allocations: 67 bytes
```

Free Blocks というのは、 `afxMemDF` が `delayFreeMemDF`に設定されている場合、解放が遅れているブロックのことです。

2 行目に示されている Object Blocks は、ヒープ上に割り当てられたままになっているブロックです。

Non-Object Blocks には、 `new`によって割り当てられた配列と構造体が含まれます。 この例では、ヒープ上に割り当てられた後で解放されていない Non-Object Blocks が 4 つあります。

`Largest number used` は、プログラムが占有したメモリの最大値を示します。

`Total allocations` は、プログラムで使用されたメモリの総量を示します。

[このトピックの内容](#BKMK_In_this_topic)

### <a name="taking-object-dumps"></a><a name="BKMK_Taking_object_dumps"></a> オブジェクト ダンプの取得
MFC プログラムでは、[CMemoryState::DumpAllObjectsSince](/cpp/mfc/reference/cmemorystate-structure#dumpallobjectssince) を使用して、割り当て解除されていないヒープ上のすべてのオブジェクトの記述をダンプできます。 `DumpAllObjectsSince` は、前回の [CMemoryState::Checkpoint](/cpp/mfc/reference/cmemorystate-structure#checkpoint)を呼び出します。 `Checkpoint` が一度も呼び出されていない場合、 `DumpAllObjectsSince` はメモリ上に存在するオブジェクトと非オブジェクトをすべてダンプします。

> [!NOTE]
> MFC のオブジェクト ダンプ機能を使用する場合は、あらかじめ [診断トレースを有効にしておく](#BKMK_Enabling_memory_diagnostics)必要があります。

> [!NOTE]
> MFC では、メモリ リークが発生したオブジェクトはすべてプログラムの終了時に自動的にダンプされるため、オブジェクトをダンプするためにコードを作成する必要はありません。

次のコードは、2 つのメモリ状態を比較することによってメモリ リークを調べ、リークが検出された場合はすべてのオブジェクトをダンプします。

```cpp
if( diffMemState.Difference( oldMemState, newMemState ) )
{
    TRACE( "Memory leaked!\n" );
    diffMemState.DumpAllObjectsSince();
}
```

次のような情報がダンプされます。

```cmd
Dumping objects ->

{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long
{2} a CPerson at $51A4

Last Name: Smith
First Name: Alan
Phone #: 581-0215

{1} strcore.cpp(80) : non-object block at $00A7516E, 25 bytes long
```

行の先頭に記述されている中かっこ内の数字は、そのオブジェクトが割り当てられた順番を示します。 後に割り当てられたオブジェクトほど数字は大きくなり、ダンプ情報の上部に表示されます。

オブジェクト ダンプによって最大限の情報を得るには、任意の `Dump` 派生オブジェクトの `CObject`メンバー関数をオーバーライドして、オブジェクト ダンプをカスタマイズします。

特定のメモリ割り当てにブレークポイントを設定するには、グローバル変数 `_afxBreakAlloc` に中かっこ内の数字を設定します。 再びプログラムを実行すると、そのメモリ割り当てが行われる時点で停止します。 この時点で呼び出し履歴を調べると、問題の割り当てが行われた経緯がわかります。

C ランタイム ライブラリにも同様の関数 [_CrtSetBreakAlloc](/cpp/c-runtime-library/reference/crtsetbreakalloc)があり、C ランタイムでのメモリ割り当てに対して使用できます。

[このトピックの内容](#BKMK_In_this_topic)

#### <a name="interpreting-memory-dumps"></a><a name="BKMK_Interpreting_memory_dumps"></a> メモリ ダンプの解釈
次のオブジェクト ダンプを詳しく検討してください。

```cmd
{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long
{2} a CPerson at $51A4

Last Name: Smith
First Name: Alan
Phone #: 581-0215

{1} strcore.cpp(80) : non-object block at $00A7516E, 25 bytes long
```

このダンプを生成したプログラムでは、メモリが明示的に割り当てられているのは 2 か所だけ (1 つはスタック上、もう 1 つはヒープ上) です。

```cpp
// Do your memory allocations and deallocations.
CString s("This is a frame variable");
// The next object is a heap object.
CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );
```

`CPerson` コンストラクターは、引数として `char`への 3 つのポインターをとり、これらの引数を使用して `CString` メンバー変数を初期化します。 メモリ ダンプ情報を調べてみると、 `CPerson` オブジェクトと一緒に 3 つの非オブジェクト ブロック (non-object block) (3、4、5) が表示されています。 これらのブロックは `CString` メンバー変数の文字を格納しており、 `CPerson` オブジェクトのデストラクターが呼び出されても削除されないことがわかります。

2 番目にメモリが割り当てられたブロックは `CPerson` オブジェクト自体です。 `$51A4` はブロックのアドレスを表し、その後にオブジェクトの内容が表示されています。この情報は、 `CPerson`DumpAllObjectsSince`Dump` によって呼び出された [::](/cpp/mfc/reference/cmemorystate-structure#dumpallobjectssince)が出力したものです。

1 番目にメモリが割り当てられたブロックは、その割り当て番号とサイズから、 `CString` のフレーム変数に割り当てられていることがわかります。ブロック サイズは、 `CString` のフレーム変数の文字数と一致しています。 フレーム上に割り当てられた変数は、フレームがスコープ外に出ると自動的に解放されます。

**フレーム変数**

通常、フレーム変数に割り当てられているヒープ オブジェクトについては、フレーム変数がスコープ外に出ると自動的に解放されるため、メモリ リークについて心配する必要はありません。 メモリ ダンプの診断出力にフレーム変数の記述が含まれないようにするには、フレーム変数のスコープ外で `Checkpoint` を呼び出す必要があります。 たとえば、次のように、前のプログラム例のメモリ割り当てコードを中かっこで囲んでスコープを限定します。

```cpp
oldMemState.Checkpoint();
{
    // Do your memory allocations and deallocations ...
    CString s("This is a frame variable");
    // The next object is a heap object.
    CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );
}
newMemState.Checkpoint();
```

中かっこでスコープを限定したため、この例から出力されるメモリ ダンプ情報は次のようになります。

```cmd
Dumping objects ->

{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long
{2} a CPerson at $51A4

Last Name: Smith
First Name: Alan
Phone #: 581-0215
```

**非オブジェクトへの割り当て**

割り当てには、 `CPerson`などのオブジェクトへの割り当てと、非オブジェクトへの割り当てがあります。 "非オブジェクトへの割り当て" とは、`CObject` から派生していないオブジェクトに対する割り当て、または C のプリミティブ型 (`char`、`int`、`long` など) に対する割り当てのことです。 <strong>CObject</strong> の派生クラスによって内部バッファーなどの領域が追加で割り当てられる場合、これらのオブジェクトについては、オブジェクトへの割り当てと非オブジェクトへの割り当ての両方が表示されます 。

**メモリ リークの防止**

上のコードでは、 `CString` のフレーム変数に割り当てられたメモリ ブロックは自動的に解放されたため、メモリ リークとして表示されていません。 スコープ規則によってメモリを自動的に解放すると、フレーム変数に関連するメモリ リークのほとんどを解消できます。

一方、ヒープ上に割り当てられたオブジェクトについては、メモリ リークを防ぐために明示的に削除する必要があります。 前のプログラム例で、最後のメモリ リークを解消するには、ヒープ上に割り当てられた `CPerson` オブジェクトを次のように削除します。

```cpp
{
    // Do your memory allocations and deallocations.
    CString s("This is a frame variable");
    // The next object is a heap object.
    CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );
    delete p;
}
```

[このトピックの内容](#BKMK_In_this_topic)

#### <a name="customizing-object-dumps"></a><a name="BKMK_Customizing_object_dumps"></a> オブジェクト ダンプのカスタマイズ
[CObject](/cpp/mfc/reference/cobject-class)から派生クラスを作成するときに `Dump` メンバー関数をオーバーライドすると、 [DumpAllObjectsSince](/cpp/mfc/reference/cmemorystate-structure#dumpallobjectssince) を使用して [出力ウィンドウ](../ide/reference/output-window.md)にオブジェクトをダンプするときに、追加情報を提供できます。

`Dump` 関数は、オブジェクトのメンバー変数の内容をテキスト形式でダンプ コンテキスト ([CDumpContext](/cpp/mfc/reference/cdumpcontext-class)) に書き込みます。 ダンプ コンテキストは、入出力ストリームに類似しています。 追加演算子 ( **<<** ) を使用して、 `CDumpContext`を呼び出します。

`Dump` 関数をオーバーライドするときは、まず基底クラスの `Dump` を呼び出して、基底クラスのオブジェクトの内容をダンプします。 その後、派生クラスの各メンバー変数について、テキスト形式の説明と値を出力します。

`Dump` 関数の宣言例を次に示します。

```cpp
class CPerson : public CObject
{
public:
#ifdef _DEBUG
    virtual void Dump( CDumpContext& dc ) const;
#endif

    CString m_firstName;
    CString m_lastName;
    // And so on...
};
```

オブジェクトのダンプは、プログラムをデバッグする場合にだけ必要です。したがって、 `Dump` 関数の宣言は **#ifdef _DEBUG と #endif** で囲みます。

次の例の `Dump` 関数は、まず基底クラスの `Dump` 関数を呼び出します。 その後、各メンバー変数の簡単な説明を各メンバーの値と一緒に診断ストリームに書き込みます。

```cpp
#ifdef _DEBUG
void CPerson::Dump( CDumpContext& dc ) const
{
    // Call the base class function first.
    CObject::Dump( dc );

    // Now do the stuff for our specific class.
    dc << "last name: " << m_lastName << "\n"
        << "first name: " << m_firstName << "\n";
}
#endif
```

ダンプの出力先を指定するために、 `CDumpContext` に引数を渡す必要があります。 MFC のデバッグ バージョンでは、 `CDumpContext` という定義済みの `afxDump` オブジェクトを渡して、出力をデバッガーに送ります。

```cpp
CPerson* pMyPerson = new CPerson;
// Set some fields of the CPerson object.
//...
// Now dump the contents.
#ifdef _DEBUG
pMyPerson->Dump( afxDump );
#endif
```

[このトピックの内容](#BKMK_In_this_topic)

## <a name="reducing-the-size-of-an-mfc-debug-build"></a><a name="BKMK_Reducing_the_size_of_an_MFC_Debug_build"></a> MFC デバッグ ビルドのサイズの縮小
大型の MFC アプリケーションでは、デバッグ情報でかなりのディスク容量が占有される場合があります。 次のいずれかの手順を使用して、サイズを縮小できます。

1. **/Z7** ではなく、[/Z7、/Zi、/ZI (デバッグ情報の形式)](/cpp/build/reference/z7-zi-zi-debug-information-format) オプションを使用して、MFC ライブラリをリビルドします。 これらのオプションを指定すると、ライブラリ全体のデバッグ情報を格納する単一のプログラム データベース (PDB) ファイルがビルドされます。これによって、無駄をなくしてディスク容量を節約できます。

2. MFC ライブラリをデバッグ情報なしでリビルドします ([/Z7、/Zi、/ZI (デバッグ情報の形式)](/cpp/build/reference/z7-zi-zi-debug-information-format) オプションがありません)。 この場合、デバッグ情報がないため、MFC ライブラリのコード内で大半のデバッガー機能を使用できなくなります。しかし、MFC ライブラリは完全にデバッグ済みであるため、このことは問題にはなりません。

3. 次に示すように、選択したモジュールのデバッグ情報だけを追加してアプリケーションをビルドする。

    [このトピックの内容](#BKMK_In_this_topic)

### <a name="building-an-mfc-app-with-debug-information-for-selected-modules"></a><a name="BKMK_Building_an_MFC_app_with_debug_information_for_selected_modules"></a> 選択したモジュールのデバッグ情報を持つ MFC アプリケーションのビルド
選択したモジュールを MFC デバッグ ライブラリと一緒にビルドすると、これらのモジュール内で、ステップ実行やその他のデバッグ機能を使用できます。 この手順ではプロジェクトのデバッグ構成とリリース構成の両方を使用するため、以下の手順に示した変更が必要になります (また、完全なリリース ビルドが必要な場合は、"すべてをリビルドする" 必要があります)。

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[表示]** メニューの **[プロパティ ページ]** をクリックします。

3. まず、新しいプロジェクト構成を作成します。

   1. **[\<Project> プロパティ ページ]** ダイアログ ボックスで、 **[構成マネージャー]** ボタンをクリックします。

   2. [[構成マネージャー] ダイアログ ボックス](/previous-versions/visualstudio/visual-studio-2010/t1hy4dhz(v=vs.100))のグリッド内でプロジェクトを見つけます。 **[構成]** 列の [ **\<New...>** ] を選択します。

   3. [[新規プロジェクト構成] ダイアログ ボックス](/previous-versions/visualstudio/visual-studio-2010/0eh8w4cf(v=vs.100))の **[Project Configuration Name]** ボックスに、新しいプロジェクト構成に付ける名前を "Partial Debug" のように入力します。

   4. **[設定のコピー元]** ボックスの **[Release]** をクリックします。

   5. **[OK]** をクリックして、 **[新しいプロジェクト構成]** ダイアログ ボックスを閉じます。

   6. **[構成マネージャー]** ダイアログ ボックスを閉じます。

4. 次に、プロジェクト全体に関するオプションを設定します。

   1. **[プロパティ ページ]** ダイアログ ボックスで、 **[構成プロパティ]** フォルダーの下の **[全般]** カテゴリを選択します。

   2. プロジェクト設定グリッドで、 **[プロジェクトの既定値]** が展開されていない場合は展開します。

   3. **[プロジェクトの既定値]** の下の **[MFC の使用]** を見つけます。 現在の設定値がグリッドの右列に表示されます。 現在の設定値をクリックし、 **[スタティック ライブラリで MFC を使用する]** に変更します。

   4. **[プロパティ ページ]** ダイアログ ボックスの左ペインで、 **[C/C++]** フォルダーを開き、 **[プリプロセッサ]** を選択します。 プロパティ グリッドで、 **[プロセッサの定義]** を見つけ、"NDEBUG" を "_DEBUG" に置き換えます。

   5. **[プロパティ ページ]** ダイアログ ボックスの左ペインで、 **[リンカー]** フォルダーを開き、 **[入力]** カテゴリを選択します。 プロパティ グリッドで、 **[追加の依存ファイル]** を見つけます。 **[追加の依存ファイル]** の設定値として「NAFXCWD.LIB」および「LIBCMT」と入力します。

   6. **[OK]** をクリックして、新しいビルド オプションを保存し、 **[プロパティ ページ]** ダイアログ ボックスを閉じます。

5. **[ビルド]** メニューの **[リビルド]** をクリックします。 これにより、モジュールからデバッグ情報がすべて削除されますが、MFC ライブラリに影響はありません。

6. 次に、選択したアプリケーション モジュールに、デバッグ情報を改めて追加します。 ブレークポイントの設定やその他のデバッガー機能を使用できるのは、デバッグ情報を追加してコンパイルしたモジュールだけです。 デバッグ情報を追加するプロジェクト ファイルごとに、次の手順を実行します。

   1. ソリューション エクスプローラーで、該当するプロジェクトの下にある **[ソース ファイル]** フォルダーを開きます。

   2. デバッグ情報を設定するファイルを選択します。

   3. **[表示]** メニューの **[プロパティ ページ]** をクリックします。

   4. **[プロパティ ページ]** ダイアログ ボックスで、 **[構成プロパティ]** フォルダーの下の **[C/C++]** フォルダーを開き、 **[全般]** カテゴリを選択します。

   5. プロパティ グリッドで、 **[デバッグ情報の形式]** を見つけます。

   6. **[デバッグ情報の形式]** の設定値をクリックし、デバッグ情報のオプション (通常は **/ZI**) を選択します。

   7. アプリケーション ウィザードで生成されたアプリケーションを使用している場合や、プリコンパイル済みヘッダーがある場合は、他のモジュールをコンパイルする前に、プリコンパイル済みヘッダーを無効にするか再コンパイルする必要があります。 この処理を行わないと、警告メッセージ C4650 とエラー メッセージ C2855 が表示されます。 プリコンパイル ヘッダーを無効にするには、 **[\<Project> プロパティ ページ]** ダイアログ ボックス ( **[構成プロパティ]** フォルダーの **[C/C++]** サブフォルダーにある **[プリコンパイル済みヘッダー]** カテゴリ) の **[プリコンパイル済みヘッダーを作成/使用する]** 設定を変更します。

7. **[ビルド]** メニューの **[ビルド]** をクリックし、最新ではないプロジェクト ファイルをリビルドします。

   このトピックで解説した方法の代わりに、外部メイクファイルを使用して、各ファイルに個別のオプションを定義することもできます。 その場合、MFC デバッグ ライブラリとリンクするには、モジュールごとに [_DEBUG](/cpp/c-runtime-library/debug) フラグを定義する必要があります。 MFC リリース ライブラリを使用する場合は、NDEBUG を定義する必要があります。 外部メイクファイルの記述方法については、「 [NMAKE の実行](/cpp/build/running-nmake)」を参照してください。

   [このトピックの内容](#BKMK_In_this_topic)

## <a name="see-also"></a>関連項目
[ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)