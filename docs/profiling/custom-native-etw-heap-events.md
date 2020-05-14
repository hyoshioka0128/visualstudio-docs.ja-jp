---
title: カスタム ネイティブ ETW ヒープ イベント | Microsoft Docs
ms.date: 02/24/2017
ms.topic: conceptual
ms.assetid: 668a6603-5082-4c78-98e6-f3dc871aa55b
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- C++
ms.workload:
- cplusplus
ms.openlocfilehash: 1bb6f906cbfb715d67f6e10ddcecf094bc25821f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62552966"
---
# <a name="custom-native-etw-heap-events"></a>カスタム ネイティブ ETW ヒープ イベント

Visual Studio には、[プロファイリングと診断](../profiling/profiling-feature-tour.md)のためのさまざまなツールがあります。その 1 つがネイティブ メモリ プロファイラーです。  このプロファイラーはヒープ プロバイダーから [ETW イベント](/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)をフックし、メモリの割り当て状況と使用状況を分析します。  既定では、このツールは、標準の Windows ヒープから行われた割り当てのみを分析できます。このネイティブ ヒープ外の割り当ては表示されません。

カスタム ヒープを使用し、標準ヒープの割り当てオーバーヘッドを回避する方法を使用したい場合があります。  たとえば、[VirtualAlloc](/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc) を使用し、アプリまたはゲームの開始時に大量のメモリを割り当て、そのリスト内で独自のブロックを管理できます。  このシナリオでは、メモリ プロファイラー ツールは最初の割り当てのみを認識し、メモリ チャンク内で行われたカスタム管理は認識されません。  ただし、カスタム ネイティブ ヒープの ETW プロバイダーを使用すると、標準ヒープ外で行うあらゆる割り当てをこのツールに認識させることができます。

たとえば、`MemoryPool` がカスタム ヒープである次のようなプロジェクトでは、Windows ヒープに割り当てが 1 つだけ表示されます。

```cpp
class Foo
{
public:
    int x, y;
};

...

// MemoryPool is a custom managed heap, which allocates 8192 bytes
// on the standard Windows Heap named "Windows NT"
MemoryPool<Foo, 8192> mPool;

// the "allocate" method requests memory from the pool created above
// and is cast to an object of type Foo, shown above
Foo* pFoo1 = (Foo*)mPool.allocate();
Foo* pFoo2 = (Foo*)mPool.allocate();
Foo* pFoo3 = (Foo*)mPool.allocate();
```

カスタム ヒープの追跡がない[メモリ使用量](../profiling/memory-usage.md)ツールからのスナップショットには、8192 バイトの割り当てが 1 つだけ表示され、プールにより行われたカスタム割り当ては何も表示されません。

![Windows ヒープ割り当て](media/heap-example-windows-heap.png)

次の手順を実行することで、この同じツールを使用し、カスタム ヒープのメモリ使用量を追跡できます。

## <a name="how-to-use"></a>使い方

このライブラリは C と C++ で簡単に使用できます。

1. カスタム ヒープ ETW プロバイダーのヘッダーを追加します。

   ```cpp
   #include <VSCustomNativeHeapEtwProvider.h>
   ```

1. 新しく割り当てられたヒープ メモリにポインターを返すカスタム ヒープ マネージャーの関数に `__declspec(allocator)` デコレータを追加します。  このデコレータにより、返されるメモリの種類をツールが正確に識別できます。  次に例を示します。

   ```cpp
   __declspec(allocator) void *MyMalloc(size_t size);
   ```

   > [!NOTE]
   > このデコレータは、この関数がアロケーターの呼び出しであることをコンパイラに通知します。  関数が呼び出されるたびに、呼び出しサイトのアドレス、呼び出し指示のサイズ、新しいオブジェクトのタイプ ID が新しい `S_HEAPALLOCSITE` 記号に出力されます。  呼び出し履歴が割り当てられると、Windows はこの情報で ETW イベントを発行します。  メモリ プロファイラー ツールは呼び出し履歴で `S_HEAPALLOCSITE` 記号に一致するリターン アドレスを探します。この記号のタイプ ID 情報を利用し、割り当てのランタイム タイプが表示されます。
   >
   > つまり、`(B*)(A*)MyMalloc(sizeof(B))` のように見える呼び出しは、`B` や `void` ではなく、タイプ `A` としてツールに表示されます。

1. C++ の場合、ヒープの名前を指定して `VSHeapTracker::CHeapTracker` オブジェクトを作成します。この名前はプロファイリング ツールに表示されます。

   ```cpp
   auto pHeapTracker = std::make_unique<VSHeapTracker::CHeapTracker>("MyCustomHeap");
   ```

   C を使用している場合、代わりに `OpenHeapTracker` 関数を使用します。  この関数は、他の追跡関数を呼び出すときに使用するハンドルを返します。

   ```C
   VSHeapTrackerHandle hHeapTracker = OpenHeapTracker("MyHeap");
   ```

1. カスタム関数を利用してメモリを割り当てるとき、メモリのポインターと割り当てサイズを渡して `AllocateEvent` (C++) または `VSHeapTrackerAllocateEvent` (C) メソッドを呼び出し、割り当てを追跡記録します。

   ```cpp
   pHeapTracker->AllocateEvent(memPtr, size);
   ```

   or

   ```C
   VSHeapTrackerAllocateEvent(hHeapTracker, memPtr, size);
   ```

   > [!IMPORTANT]
   > 先に説明した `__declspec(allocator)` デコレータを利用し、カスタム アロケーター関数にタグを付けることを忘れないでください。

1. カスタム関数を利用してメモリを解放するとき、メモリのポインターを渡して `DeallocateEvent` (C++) または `VSHeapTracerDeallocateEvent` (C) 関数を呼び出し、割り当て解除を追跡記録します。

   ```cpp
   pHeapTracker->DeallocateEvent(memPtr);
   ```

   または

   ```C
   VSHeapTrackerDeallocateEvent(hHeapTracker, memPtr);
   ```

1. カスタム関数を利用してメモリを再割り当てするとき、新しいメモリのポインター、割り当てのサイズ、古いメモリのポインターを渡して `ReallocateEvent` (C++) または `VSHeapReallocateEvent` (C) メソッドを呼び出します。

   ```cpp
   pHeapTracker->ReallocateEvent(memPtrNew, size, memPtrOld);
   ```

   または

   ```C
   VSHeapTrackerReallocateEvent(hHeapTracker, memPtrNew, size, memPtrOld);
   ```

1. 最後になりますが、C++ でカスタム ヒープ トラッカーを閉じ、クリーンアップするには、`CHeapTracker` デストラクターを使用します。その場合、手動で行うか、標準のスコープ規則または C の `CloseHeapTracker` 関数を利用します。

   ```cpp
   delete pHeapTracker;
   ```

   または

   ```C
   CloseHeapTracker(hHeapTracker);
   ```

## <a name="track-memory-usage"></a>メモリ使用量の追跡
呼び出しが所定の場所にあるので、Visual Studio の標準**メモリ使用量**ツールを利用し、カスタム ヒープ使用量を追跡できます。  このツールの使用方法については、[メモリ使用量](../profiling/memory-usage.md)に関する文書を参照してください。 スナップショットによるヒープ プロファイリングを有効にしてください。有効にしない場合、カスタム ヒープ使用量が表示されません。

![ヒープ プロファイリングを有効にする](media/heap-enable-heap.png)

カスタム ヒープ追跡を表示するには、 **[スナップショット]** ウィンドウの右上隅にある **[ヒープ]** ドロップダウンを利用し、*NT ヒープ*から先に名前を付けた独自のヒープに変更します。

![ヒープ選択](media/heap-example-custom-heap.png)

`MemoryPool` で `VSHeapTracker::CHeapTracker` オブジェクトを作成し、独自の `allocate` メソッドで `AllocateEvent` メソッドを呼び出す上記のコード例を使用して、そのカスタム割り当ての結果を表示できます。ここには、合計 24 バイトのインスタンスが 3 つ表示され、種類はすべて `Foo` です。

既定の *NT ヒープ*は前と同じに見えますが、`CHeapTracker` オブジェクトが追加されています。

![NT ヒープとトラッカー](media/heap-example-windows-heap.png)

標準 Windows ヒープと同様に、このツールを利用してスナップショットを比較し、カスタム ヒープのリークや破損を探すこともできます。詳しくは、[メモリ使用量](../profiling/memory-usage.md)に関する文書を参照してください。

> [!TIP]
> Visual Studio の**パフォーマンス プロファイリング** ツールセットにも**メモリ使用量**ツールがあります。これは、 **[デバッグ]**  >  **[パフォーマンス プロファイラー]** メニュー オプション、または **Alt**+**F2** キーの組み合わせで有効にできます。  この機能にはヒープ追跡がありません。ここの説明のようにカスタム ヒープが表示されることはありません。  この機能があるのは **[診断ツール]** ウィンドウだけです。このウィンドウは、 **[デバッグ]**  >  **[Windows]**  >  **[診断ツールの表示]** メニュー、または **Ctrl**+**Alt**+**F2** キーの組み合わせで有効にできます。

## <a name="see-also"></a>参照
[プロファイリング ツールの概要](../profiling/profiling-feature-tour.md)
[メモリ使用量](../profiling/memory-usage.md)
