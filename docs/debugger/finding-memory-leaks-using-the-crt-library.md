---
title: CRT ライブラリを使用したメモリリークの検出 |Microsoft Docs
ms.date: 10/04/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- breakpoints, on memory allocation
- _CrtMemState
- _CrtMemCheckpoint
- memory leaks
- _CrtMemDifference
- memory leaks, detecting and isolating
- _CrtDumpMemoryLeaks
- _CrtSetBreakAlloc
- _crtBreakAlloc
- _CrtSetReportMode
- memory, debugging
- _CrtMemDumpStatistics
- debugging memory leaks
- _CRTDBG_MAP_ALLOC
- _CrtSetDbgFlag
ms.assetid: cf6dc7a6-cd12-4283-b1b6-ea53915f7ed1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: eb2729dcaf0da41c0adac24b0e1909a6d2697eb6
ms.sourcegitcommit: 697f2ab875fd789685811687387e9e8e471a38c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74829943"
---
# <a name="find-memory-leaks-with-the-crt-library"></a>CRT ライブラリを使用したメモリ リークの検出

メモリリークは、C/C++アプリで最も微妙で検出しにくいバグの1つです。 メモリリークが発生したため、以前に割り当てられたメモリの割り当てを正しく解除できませんでした。 わずかなメモリリークは最初は認識されない場合がありますが、時間の経過と共に、アプリでメモリ不足が発生した場合にパフォーマンスが低下するという現象が発生する可能性があります。 使用可能なすべてのメモリを使用するリークしているアプリによって、他のアプリがクラッシュする可能性があります。これにより、アプリの責任として混乱が生じます。 無害なメモリリークであっても、修正が必要な他の問題を示している可能性があります。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーと C ランタイムライブラリ (CRT) は、メモリリークを検出して特定するのに役立ちます。

## <a name="enable-memory-leak-detection"></a>メモリリーク検出の有効化

メモリリークを検出するための主要なツールはC++ 、c/デバッガーと c ランタイムライブラリ (CRT) デバッグヒープ関数です。

すべてのデバッグヒープ関数を有効にするには、次のC++ステートメントをプログラムに次の順序で含めます。

```cpp
#define _CRTDBG_MAP_ALLOC
#include <stdlib.h>
#include <crtdbg.h>
```

`#define` ステートメントにより、CRT ヒープ関数の基本バージョンがデバッグ バージョンに対応付けられます。 `#define` ステートメントを省略すると、メモリリークダンプの[詳細が小さく](#interpret-the-memory-leak-report)なります。

*Crtdbg.h*をインクルードすると、`malloc` 関数と `free` 関数がデバッグバージョンの[_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg)および[_free_dbg](/cpp/c-runtime-library/reference/free-dbg)にマップされ、メモリの割り当てと解放が追跡されます。 この対応付けは、 `_DEBUG`が定義されているデバッグ ビルドでだけ行われます。 リリース ビルドでは、通常の `malloc` 関数と `free` 関数が使用されます。

前のステートメントを使用してデバッグヒープ関数を有効にした後、アプリの終了ポイントの前に[_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks)を呼び出して、アプリが終了したときにメモリリークレポートを表示します。

```cpp
_CrtDumpMemoryLeaks();
```

アプリに複数の終了がある場合は、すべての終了ポイントに手動で `_CrtDumpMemoryLeaks` を配置する必要はありません。 各終了ポイントで `_CrtDumpMemoryLeaks` を自動的に呼び出すには、次に示すビットフィールドを使用して、アプリの先頭に `_CrtSetDbgFlag` の呼び出しを配置します。

```cpp
_CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );
```

既定では、 `_CrtDumpMemoryLeaks` は、メモリ リーク レポートを **[出力]** ウィンドウの **デバッグ** ウィンドウに出力します。 ライブラリを使用すると、情報の出力場所が別の場所に変更されることがあります。

次に示すように、`_CrtSetReportMode` を使用してレポートを別の場所にリダイレクトしたり、**出力**ウィンドウに戻したりすることができます。

```cpp
_CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_DEBUG );
```

## <a name="interpret-the-memory-leak-report"></a>メモリリークレポートの解釈

アプリで `_CRTDBG_MAP_ALLOC`が定義されていない場合、 [_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks)は次のようなメモリリークレポートを表示します。

```cmd
Detected memory leaks!
Dumping objects ->
{18} normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

アプリで `_CRTDBG_MAP_ALLOC`が定義されている場合、メモリリークレポートは次のようになります。

```cmd
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\leaktest\leaktest.cpp(20) : {18}
normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

2番目のレポートには、リークしたメモリが最初に割り当てられたファイル名と行番号が表示されます。

`_CRTDBG_MAP_ALLOC`を定義するかどうかにかかわらず、メモリリークレポートには次のように表示されます。

- メモリ割り当て番号 (例では `18`)
- ブロックの種類。例では `normal` ます。
- 16進メモリ位置。例では `0x00780E80`。
- ブロックのサイズ (例では `64 bytes`)。
- ブロックのデータの最初の 16 バイト (16 進形式)

メモリブロックの型は、*通常*、*クライアント*、または*CRT*です。 *normal ブロック* は、プログラムによって割り当てられる通常のメモリです。 *client ブロック* は、デストラクターを必要とするオブジェクト用に、MFC プログラムが使用する特殊なメモリ ブロックです。 MFC の `new` 演算子は、作成されるオブジェクトに応じて、normal ブロックまたは client ブロックを作成します。

*CRT ブロック* は、CRT ライブラリが独自に使用するために割り当てるメモリ ブロックです。 Crt ライブラリでは、これらのブロックの割り当てが解除されるため、crt ライブラリに重大な問題がある場合を除き、CRT ブロックはメモリリークレポートには表示されません。

これ以外に、メモリ リーク レポートに表示されないメモリ ブロックが 2 種類あります。 *Free ブロック*は解放されたメモリであるため、定義によってリークされることはありません。 *Ignore ブロック*は、メモリリークレポートから除外するように明示的にマークされているメモリです。

上記の手法は、標準の CRT `malloc` 関数を使用して割り当てられたメモリのメモリリークを識別します。 ただし、 C++ `new` 演算子を使用してプログラムがメモリを割り当てる場合、`operator new` がメモリリークレポートに `_malloc_dbg` を呼び出したときにのみ、ファイル名と行番号が表示されることがあります。 さらに便利なメモリリークレポートを作成するには、次のようなマクロを記述して、割り当てられた行を報告します。

```cpp
#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif
```

これで、コードで `DBG_NEW` マクロを使用して、`new` 演算子を置き換えることができます。 デバッグビルドでは、`DBG_NEW` は、ブロックの種類、ファイル、および行番号に対して追加のパラメーターを受け取る、グローバル `operator new` のオーバーロードを使用します。 `new` のオーバーロードは、追加情報を記録するために `_malloc_dbg` を呼び出します。 メモリリークレポートには、リークしたオブジェクトが割り当てられたファイル名と行番号が表示されます。 リリースビルドでは依然として既定の `new`が使用されます。 この手法の例を次に示します。

```cpp
// debug_new.cpp
// compile by using: cl /EHsc /W4 /D_DEBUG /MDd debug_new.cpp
#define _CRTDBG_MAP_ALLOC
#include <cstdlib>
#include <crtdbg.h>

#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif

struct Pod {
    int x;
};

void main() {
    Pod* pPod = DBG_NEW Pod;
    pPod = DBG_NEW Pod; // Oops, leaked the original pPod!
    delete pPod;

    _CrtDumpMemoryLeaks();
}
```

Visual Studio デバッガーでこのコードを実行すると、`_CrtDumpMemoryLeaks` を呼び出すと、次のようなレポートが **[出力]** ウィンドウに生成されます。

```Output
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\debug_new\debug_new.cpp(20) : {75}
 normal block at 0x0098B8C8, 4 bytes long.
 Data: <    > CD CD CD CD
Object dump complete.
```

この出力は、リークした割り当てが*debug_new .cpp*の20行目にあったことを報告します。

>[!NOTE]
>`new`という名前のプリプロセッサマクロや、その他の言語キーワードは作成しないことをお勧めします。

## <a name="set-breakpoints-on-a-memory-allocation-number"></a>メモリ割り当て番号にブレークポイントを設定する

メモリ割り当て番号は、リークしているメモリ ブロックがいつ割り当てられたかを示します。 たとえば、メモリ割り当て番号が18のブロックは、アプリの実行中に割り当てられたメモリの18番目のブロックです。 CRT レポートでは、実行中のすべてのメモリブロック割り当てがカウントされます。これには、CRT ライブラリおよびその他のライブラリ (MFC など) による割り当ても含まれます。 したがって、メモリ割り当てブロック番号18は、コードによって割り当てられた18個のメモリブロックではないと想定されます。

この割り当て番号を使用して、メモリの割り当てにブレークポイントを設定できます。

**ウォッチ ウィンドウを使用してメモリ割り当てブレークポイントを設定するには**

1. アプリの先頭付近にブレークポイントを設定し、デバッグを開始します。

1. アプリがブレークポイントで一時停止したら、[**デバッグ** > **Windows** ] >  **[ウォッチ 1]** (または ウォッチ **[2]** 、 **[ウォッチ 3]** 、または ウォッチ **[4]** ) を選択して、**ウォッチ**ウィンドウを開きます。

1. **[ウォッチ]** ウィンドウで、 **[名前]** 列に「`_crtBreakAlloc`」と入力します。

   CRT ライブラリのマルチスレッド DLL バージョン (/MD オプション) を使用している場合は、コンテキスト演算子を追加します。 `{,,ucrtbased.dll}_crtBreakAlloc`
   
   デバッグシンボルが読み込まれていることを確認します。 それ以外の場合 `_crtBreakAlloc` は*不明*として報告されます。

1. **Enter** キーを押します。

   デバッガーによって呼び出しが評価され、その結果が **[値]** 列に表示されます。 メモリ割り当てにまだブレークポイントが設定されていない場合、この値は **-1** になります。

1. **[値]** 列で、値を、デバッガーが中断するメモリ割り当ての割り当て番号に置き換えます。

メモリ割り当て番号にブレークポイントを設定したら、デバッグを続行します。 メモリ割り当て番号が変更されないように、必ず同じ状態で実行してください。 指定したメモリ割り当てでプログラムが中断した場合は、 **[呼び出し履歴]** ウィンドウとその他のデバッガーウィンドウを使用して、メモリが割り当てられた条件を確認します。 次に、実行を続行して、オブジェクトの動作を確認し、オブジェクトが正しく割り当て解除されていない原因を特定できます。

オブジェクトにデータ ブレークポイントを設定する方法も役に立つことがあります。 詳細については、「[ブレークポイントの使用](../debugger/using-breakpoints.md)」を参照してください。

さらに、コード内でメモリ割り当てブレークポイントを設定することもできます。 次のように設定できます。

```cpp
_crtBreakAlloc = 18;
```

 または

```cpp
_CrtSetBreakAlloc(18);
```

## <a name="compare-memory-states"></a>メモリ状態の比較
 メモリ リークの位置を特定するためのもう 1 つの方法では、ある時点におけるアプリケーションのメモリ状態のスナップショットを取得します。 アプリケーションの特定の時点でメモリ状態のスナップショットを取得するには、`_CrtMemState` 構造体を作成し、それを `_CrtMemCheckpoint` 関数に渡します。

```cpp
_CrtMemState s1;
_CrtMemCheckpoint( &s1 );
```

`_CrtMemCheckpoint` 関数は、現在のメモリ状態のスナップショットを構造体に格納します。

`_CrtMemState` 構造体の内容を出力するには、構造体を `_ CrtMemDumpStatistics` 関数に渡します。

```cpp
_CrtMemDumpStatistics( &s1 );
```

`_ CrtMemDumpStatistics` は、次のようなメモリ状態のダンプを出力します。

```cmd
0 bytes in 0 Free Blocks.
0 bytes in 0 Normal Blocks.
3071 bytes in 16 CRT Blocks.
0 bytes in 0 Ignore Blocks.
0 bytes in 0 Client Blocks.
Largest number used: 3071 bytes.
Total allocations: 3764 bytes.
```

コード内のセクションでメモリ リークが発生したかどうかを調べるには、そのセクションの前後のメモリ状態のスナップショットを取得した後、 `_ CrtMemDifference` を使用して 2 つのメモリ状態を比較します。

```cpp
_CrtMemCheckpoint( &s1 );
// memory allocations take place here
_CrtMemCheckpoint( &s2 );

if ( _CrtMemDifference( &s3, &s1, &s2) )
   _CrtMemDumpStatistics( &s3 );
```

`_CrtMemDifference` は `s1` と `s2` のメモリ状態を比較し、`s1` と `s2`の差である (`s3`) に結果を返します。

メモリリークを検出する方法の1つは、アプリの先頭と末尾に `_CrtMemCheckpoint` 呼び出しを配置し、`_CrtMemDifference` を使用して結果を比較することです。 `_CrtMemDifference` がメモリリークを示している場合は、リークの原因が特定されるまで、`_CrtMemCheckpoint` 呼び出しを追加して、バイナリ検索を使用してプログラムを分割できます。

## <a name="false-positives"></a>誤検知
 ライブラリによって、CRT ブロックやクライアントブロックではなく通常のブロックとして内部割り当てがマークされている場合は、`_CrtDumpMemoryLeaks` によってメモリリークが誤って示されることがあります。 その場合、 `_CrtDumpMemoryLeaks` では、ユーザー割り当てとライブラリの内部的な割り当てを区別することができません。 ライブラリ割り当てのグローバル デストラクターが、 `_CrtDumpMemoryLeaks`の呼び出しポイント後に実行される場合、すべての内部ライブラリ割り当てがメモリ リークとして報告されます。 Visual Studio .NET より前のバージョンの標準テンプレートライブラリでは、`_CrtDumpMemoryLeaks` によってこのような誤検知が報告される場合があります。

## <a name="see-also"></a>参照
- [CRT デバッグ ヒープの詳細](../debugger/crt-debug-heap-details.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
