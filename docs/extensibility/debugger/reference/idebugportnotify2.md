---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2
helpviewer_keywords:
- IDebugPortNotify2 interface
ms.assetid: 43278b79-bf16-4c08-bcf1-6f7f7a17feab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 49d3d1161d488ed4a9e12b7af6b70bf336c9f286
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724924"
---
# <a name="idebugportnotify2"></a>IDebugPortNotify2
このインターフェイスは、実行中のポートでデバッグできるプログラムを登録または登録解除します。

## <a name="syntax"></a>構文

```
IDebugPortNotify2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、ポートからのプログラムの追加と削除をサポートするために、このインターフェイスを実装します。 通常[、IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスを実装する同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 インターフェイスで[のクエリ インターフェイス](/cpp/atl/queryinterface)の`IDebugPort2`呼び出しは、このインターフェイスを返します。 また[、GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)の呼び出しは、このインターフェイスを返します。 デバッグ エンジンは、このインターフェイスを[パラメーターとして見ることができます。](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugPortNotify2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)|実行しているポートでデバッグできるプログラムを登録します。|
|[RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)|実行しているポートからデバッグできるプログラムの登録を解除します。|

## <a name="remarks"></a>Remarks
 デバッグ ポートがプログラムの読み込みまたはアンロードを知る方法を持っていない限り、カスタム ポートサプライヤーはこのインターフェイスを実装する必要があります。 特定のポートを通じてデバッグするために読み込まれるすべてのプログラムは、このインターフェイスを使用して追跡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
