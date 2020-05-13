---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d20a1180e1162e7de3aee1c5d69facf8c193910
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727426"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
このインターフェイスは、デバッグ中のプログラムを実行しているコンピュータのアドレス空間内の位置を表します。

## <a name="syntax"></a>構文

```
IDebugMemoryContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、メモリ内のアドレスを表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 呼び出しを[呼](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)び[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)出します。 また[、Add](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)と[Subtract](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)の呼び出しは、適切な算術演算が適用された後に、このインターフェイスの新しいコピーを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugMemoryContext2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|このコンテキストのユーザー表示可能な名前を取得します。|
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|このコンテキストを説明する情報を取得します。|
|[追加](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|指定した値を現在のコンテキストのアドレスに追加して、新しいコンテキストを作成します。|
|[減算](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|現在のコンテキストのアドレスから指定した値を減算して、新しいコンテキストを作成します。|
|[比較](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|比較フラグで示される方法で 2 つのコンテキストを比較します。|

## <a name="remarks"></a>Remarks
 メモリ アドレスに使用される評価された式を含むインターフェイス`IDebugMemoryContext2`を取得する[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)を取得する Visual Studio の**メモリ**ウィンドウを呼び出します。 このコンテキストは[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)と[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)に渡され、読み取りまたは書き込み先のアドレスを指定します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)
- [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)
- [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)
