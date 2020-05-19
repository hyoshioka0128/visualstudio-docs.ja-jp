---
title: VSG_NODEFAULT_INSTANCE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 19c95b0d-9a4d-441f-9ed7-3acb39e67521
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 304576391b2287aee7567b3ccc2e4514ce5cb2e8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848462"
---
# <a name="vsg_nodefault_instance"></a>VSG_NODEFAULT_INSTANCE
その存在によって、プログラムによるキャプチャ インターフェイスを提供する [VsgDbg Class](vsgdbg-class.md) クラスの既定のインスタンスが提供されるかどうかを定義します。

## <a name="syntax"></a>構文

```C++
#define VSG_NODEFAULT_INSTANCE
```

## <a name="value"></a>[値]
 その有無によって `VsgDbg` クラスの既定のインスタンスが提供されるかどうかを判断するプリプロセッサ シンボル。 このシンボルが定義されている場合は、`VsgDbg` クラスの既定のインスタンスは提供されません。それ以外の場合は、プログラムの実行前に既定のインスタンスが提供され、初期化されます。

 プログラムによるキャプチャ インターフェイスは、グローバル スコープを持つポインター `g_pVsgDbg` を通じて提供されます。

```cpp
VsgDbg *g_pVsgDbg;
```

## <a name="remarks"></a>Remarks
 ほとんどの場合は既定のインスタンスで十分ですが、D3D デバイスが DLL の外部で作成されたときのその DLL 内部のプログラムによるキャプチャ インターフェイスを使用するには、`VsgDbg` クラスの独自のインスタンスを作成および管理する必要があります。 プログラムによるキャプチャの API への独自のインターフェイスをこのように管理している場合は、オーバーヘッドを避けるために、`VSG_NODEFAULT_INSTANCE` を定義して既定のインスタンスを無効にします。

 既定のインスタンスが無効になっていない場合は、プログラムの実行前に自動的に初期化され、プログラムの終了時に自動的に破棄されます。 このインスタンスの初期化および初期化解除を明示的に行う必要はありません。

 既定のインスタンスを無効にするには、プログラムで `vsgcapture.h` を含める前に、`VSG_NODEFAULT_INSTANCE` を定義する必要があります。

## <a name="example"></a>例
 次の例は、既定のインスタンスを無効にする方法を示しています。

```cpp
// Define VSG_NODEFAULT_INSTANCE before including vsgcapture.h
#define VSG_NODEFAULT_INSTANCE

#include <vsgcapture.h>
```
