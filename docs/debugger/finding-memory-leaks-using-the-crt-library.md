---
title: CRT ライブラリを使用したメモリ リークの検出 | Microsoft Docs
ms.date: 10/04/2018
ms.topic: conceptual
dev_langs:
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
ms.openlocfilehash: 13a346aa0212f4830c2c88ed866b674fc19d30bd
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404977"
---
# <a name="find-memory-leaks-with-the-crt-library"></a>CRT ライブラリを使用したメモリ リークの検出

メモリ リークは、C/C++ アプリのバグの中でわかりづらく検出しにくいものの 1 つです。 メモリ リークが発生するのは、以前に割り当てられていたメモリの割り当てを適切に解除できなかった場合です。 わずかなメモリ リークは最初は認識されないことがありますが、長期にわたると、アプリケーションがメモリ不足になり、パフォーマンスの低下からクラッシュまで、さまざまな兆候が現れる可能性があります。 メモリ リークしているアプリケーションによってすべての使用可能なメモリが消費されると、別のアプリケーションがクラッシュし、原因となったアプリケーションの特定が困難になることもあります。 害のないメモリ リークであっても、修正が必要な別の問題を示している可能性があります。

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーと C ランタイム ライブラリ (CRT) は、メモリ リークを検出して特定するのに役立ちます。

## <a name="enable-memory-leak-detection"></a>メモリ リーク検出の有効化

メモリ リークを検出するための主要ツールは、C/C++ デバッガーと C ランタイム ライブラリ (CRT) デバッグ ヒープ関数です。

すべてのデバッグ ヒープ関数を有効にするには、次のステートメントを C++ プログラムに次の順序で追加します。

```cpp
#define _CRTDBG_MAP_ALLOC
#include <stdlib.h>
#include <crtdbg.h>
```

`#define` ステートメントにより、CRT ヒープ関数の基本バージョンがデバッグ バージョンに対応付けられます。 `#define` ステートメントを省略した場合、メモリ リーク ダンプに含まれる[情報が少なく](#interpret-the-memory-leak-report)なります。

*crtdbg.h* をインクルードすると、`malloc` 関数と `free` 関数は、それぞれのデバッグ バージョンである [_malloc_dbg](/cpp/c-runtime-library/reference/malloc-dbg) と [_free_dbg](/cpp/c-runtime-library/reference/free-dbg) に対応付けられます。これらの関数では、メモリの割り当てと解放が追跡されます。 この対応付けは、 `_DEBUG`が定義されているデバッグ ビルドでだけ行われます。 リリース ビルドでは、通常の `malloc` 関数と `free` 関数が使用されます。

前のステートメントを使用してデバッグ ヒープ関数を有効にした後、アプリケーションの終了ポイントの前に [_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) の呼び出しを配置すると、アプリケーションの終了時にメモリ リーク レポートを表示できます。

```cpp
_CrtDumpMemoryLeaks();
```

アプリに複数の終了があっても、すべての終了ポイントに手動で `_CrtDumpMemoryLeaks` を配置する必要はありません。 各終了ポイントで自動的に `_CrtDumpMemoryLeaks` が呼び出されるようにするには、ここに示すビット フィールドを使用してアプリケーションの先頭に `_CrtSetDbgFlag` の呼び出しを配置します。

```cpp
_CrtSetDbgFlag ( _CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF );
```

既定では、 `_CrtDumpMemoryLeaks` は、メモリ リーク レポートを **[出力]** ウィンドウの **デバッグ** ウィンドウに出力します。 ライブラリを使用すると、情報の出力場所が別の場所に変更されることがあります。

次に示すように `_CrtSetReportMode` を使用して、レポートを別の場所にリダイレクトしたり、 **[出力]** ウィンドウに戻したりすることができます。

```cpp
_CrtSetReportMode( _CRT_ERROR, _CRTDBG_MODE_DEBUG );
```

## <a name="interpret-the-memory-leak-report"></a>メモリ リーク レポートの解釈

アプリケーションで `_CRTDBG_MAP_ALLOC`を定義していない場合は、[_CrtDumpMemoryLeaks](/cpp/c-runtime-library/reference/crtdumpmemoryleaks) により次のようなメモリ リーク レポートが出力されます。

```cmd
Detected memory leaks!
Dumping objects ->
{18} normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

アプリケーションで `_CRTDBG_MAP_ALLOC` を定義している場合は、次のようなメモリ リーク レポートが出力されます。

```cmd
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\leaktest\leaktest.cpp(20) : {18}
normal block at 0x00780E80, 64 bytes long.
 Data: <                > CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD CD
Object dump complete.
```

2 つ目のレポートには、リークしているメモリが最初に割り当てられたファイル名と行番号が表示されます。

`_CRTDBG_MAP_ALLOC` を定義するかどうかにかかわらず、メモリ リーク レポートには次のように表示されます。

- メモリの割り当て番号 (この例では `18`)
- ブロックの種類 (この例では `normal`)
- 16 進形式で表したメモリ位置 (この例では `0x00780E80`)
- ブロックのサイズ (この例では `64 bytes`)
- ブロックのデータの最初の 16 バイト (16 進形式)

メモリ ブロックの種類は、*normal*、*client*、または *CRT* です。 *normal ブロック* は、プログラムによって割り当てられる通常のメモリです。 *client ブロック* は、デストラクターを必要とするオブジェクト用に、MFC プログラムが使用する特殊なメモリ ブロックです。 MFC の `new` 演算子は、作成されるオブジェクトに応じて、normal ブロックまたは client ブロックを作成します。

*CRT ブロック* は、CRT ライブラリが独自に使用するために割り当てるメモリ ブロックです。 CRT ライブラリはこれらのブロックの割り当てを解除するため、CRT ライブラリに重大な問題がある場合を除き、CRT ブロックはメモリ リーク レポートには表示されません。

これ以外に、メモリ リーク レポートに表示されないメモリ ブロックが 2 種類あります。 "*free ブロック*" は、解放済みのメモリ ブロックです。名前からわかるように、リークされることはありません。 "*ignore ブロック*" は、メモリ リーク レポートに出力しないように明示的にマークされているブロックです。

これらの手法では、標準 CRT の `malloc` 関数を使用して割り当てられたメモリのメモリ リークを特定できます。 ただし、プログラムで C++ の `new` 演算子を使用してメモリを割り当てている場合は、`operator new` が `_malloc_dbg` を呼び出すファイル名と行番号のみをメモリ リーク レポートに表示できます。 メモリ リーク レポートをさらに便利にするには、次のようなマクロを記述して、割り当てを行った行を報告します。

```cpp
#ifdef _DEBUG
    #define DBG_NEW new ( _NORMAL_BLOCK , __FILE__ , __LINE__ )
    // Replace _NORMAL_BLOCK with _CLIENT_BLOCK if you want the
    // allocations to be of _CLIENT_BLOCK type
#else
    #define DBG_NEW new
#endif
```

これで、コードで `DBG_NEW` マクロを使用して、`new` 演算子を置き換えることができます。 デバッグ ビルドでは、`DBG_NEW` は、ブロックの種類、ファイル、および行番号の追加パラメーターを受け取るグローバル `operator new` のオーバーロードを使用します。 `new` のオーバーロードは、追加情報を記録するために `_malloc_dbg` を呼び出します。 メモリ リーク レポートには、リークしたオブジェクトを割り当てたファイル名と行番号が表示されます。 リリース ビルドでは依然として既定の `new` が使用されます。 この手法の例を次に示します。

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

Visual Studio デバッガーでこのコードを実行するとき、`_CrtDumpMemoryLeaks` を呼び出すと、 **[出力]** ウィンドウに次のようなレポートが生成されます。

```Output
Detected memory leaks!
Dumping objects ->
c:\users\username\documents\projects\debug_new\debug_new.cpp(20) : {75}
 normal block at 0x0098B8C8, 4 bytes long.
 Data: <    > CD CD CD CD
Object dump complete.
```

この出力では、リークした割り当てが *debug_new.cpp* の 20 行目にあることが報告されています。

>[!NOTE]
>`new` という名前のプリプロセッサ マクロやその他の言語キーワードは作成しないことをお勧めします。

## <a name="set-breakpoints-on-a-memory-allocation-number"></a>メモリ割り当て番号へのブレークポイントの設定

メモリ割り当て番号は、リークしているメモリ ブロックがいつ割り当てられたかを示します。 たとえば、メモリ割り当て番号が 18 のブロックは、アプリケーションの実行中に割り当てられたメモリの 18 番目のブロックです。 CRT レポートでは、実行中のすべてのメモリブロック割り当てが合計されます。これには、CRT ライブラリおよびその他のライブラリ (MFC など) による割り当ても含まれます。 したがって、メモリ割り当てブロック番号 18 は、おそらくコードによって 18 番目に割り当てられたブロックではありません。

この割り当て番号を使用して、メモリの割り当てにブレークポイントを設定できます。

**ウォッチ ウィンドウを使用してメモリ割り当てブレークポイントを設定するには**

1. アプリの先頭付近にブレークポイントを設定し、デバッグを開始します。

1. アプリがブレークポイントで一時停止したら、 **[デバッグ]**  >  **[ウィンドウ]**  >  **[ウォッチ 1]** (または **[ウォッチ 2]** 、 **[ウォッチ 3]** 、または **[ウォッチ 4]** ) を選択して**ウォッチ** ウィンドウを開きます。

1. **ウォッチ** ウィンドウの **[名前]** 列に、「`_crtBreakAlloc`」と入力します。

   マルチスレッド DLL バージョン (/MD オプション) の CRT ライブラリを使用している場合は、コンテキスト演算子を追加して「`{,,ucrtbased.dll}_crtBreakAlloc`」とします。
   
   デバッグ シンボルが読み込まれていることを確認します。 そうしないと、`_crtBreakAlloc` が *unidentified* として報告されます。

1. **Enter** キーを押します。

   デバッガーによって呼び出しが評価され、その結果が **[値]** 列に表示されます。 メモリ割り当てにまだブレークポイントが設定されていない場合、この値は **-1** になります。

1. **[値]** 列の値を、デバッガーで中断するメモリ割り当ての割り当て番号に置き換えます。

メモリ割り当て番号にブレークポイントを設定したら、デバッグを続行できます。 メモリ割り当て番号が変更されないように、必ず同じ状態で実行してください。 指定したメモリ割り当てでプログラムが停止したら、 **[呼び出し履歴]** ウィンドウやその他のデバッガー ウィンドウを参照して、メモリが割り当てられた状況を確認できます。 その後、実行を続行して、オブジェクトで何が起こっているかを確認し、オブジェクトが正常に解放されない原因を調べることができます。

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

メモリ リークの位置を特定するためのもう 1 つの方法では、ある時点におけるアプリケーションのメモリ状態のスナップショットを取得します。 アプリケーションの任意の時点でのメモリ状態のスナップショットを取得するには、`_CrtMemState` 構造体を作成し、`_CrtMemCheckpoint` 関数に渡します。

```cpp
_CrtMemState s1;
_CrtMemCheckpoint( &s1 );
```

`_CrtMemCheckpoint`関数は、現在のメモリ状態のスナップショットを構造体に格納します。

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

`_CrtMemDifference` は、`s1` と `s2` のメモリ状態を比較し、`s1` と `s2` の相違を示す結果 (`s3`) を返します。

メモリ リークを見つけるための 1 つの方法では、最初にアプリケーションの先頭と末尾で `_CrtMemCheckpoint` を呼び出し、`_CrtMemDifference` を使用して結果を比較します。 `_CrtMemDifference` によってメモリ リークが示された場合は、さらに多くの `_CrtMemCheckpoint` の呼び出しを追加して、リークの原因が特定されるまでバイナリ検索を使用してプログラムを分割できます。

## <a name="false-positives"></a>誤検知

 ライブラリが内部割り当てを CRT ブロックまたは client ブロックではなく normal ブロックとしてマークした場合、`_CrtDumpMemoryLeaks` によって、メモリ リークが誤って検知されることがあります。 その場合、 `_CrtDumpMemoryLeaks` では、ユーザー割り当てとライブラリの内部的な割り当てを区別することができません。 ライブラリ割り当てのグローバル デストラクターが、 `_CrtDumpMemoryLeaks`の呼び出しポイント後に実行される場合、すべての内部ライブラリ割り当てがメモリ リークとして報告されます。 Visual Studio .NET より前のバージョンの標準テンプレート ライブラリによって、`_CrtDumpMemoryLeaks` が誤検出を報告する可能性があります。

## <a name="see-also"></a>関連項目

- [CRT デバッグ ヒープの詳細](../debugger/crt-debug-heap-details.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
