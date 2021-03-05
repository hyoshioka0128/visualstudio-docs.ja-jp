---
description: このインターフェイスは、実行されているポートでデバッグできるプログラムを登録または登録解除します。
title: IDebugPortNotify2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortNotify2
helpviewer_keywords:
- IDebugPortNotify2 interface
ms.assetid: 43278b79-bf16-4c08-bcf1-6f7f7a17feab
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 759be0ff57da7c6bb65ed6ca8191720f835b894a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169341"
---
# <a name="idebugportnotify2"></a>IDebugPortNotify2
このインターフェイスは、実行されているポートでデバッグできるプログラムを登録または登録解除します。

## <a name="syntax"></a>構文

```
IDebugPortNotify2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポート供給業者は、このインターフェイスを実装して、ポートからのプログラムの追加と削除をサポートします。 通常は、 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出すと、 `IDebugPort2` このインターフェイスが返されます。 また、 [Getportnotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md) を呼び出すと、このインターフェイスが返されます。 デバッグエンジンは、 [WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)のパラメーターとしてこのインターフェイスを参照できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugPortNotify2` ます。

|メソッド|説明|
|------------|-----------------|
|[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)|デバッグ可能なプログラムを、それが実行されているポートで登録します。|
|[RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)|デバッグ可能なプログラムを、実行中のポートから登録解除します。|

## <a name="remarks"></a>解説
 デバッグポートでプログラムが読み込まれるかアンロードされるかを知る方法がない限り、カスタムポート供給業者はこのインターフェイスを実装する必要があります。 特定のポートでデバッグするために読み込まれるすべてのプログラムは、このインターフェイスを使用して追跡されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
