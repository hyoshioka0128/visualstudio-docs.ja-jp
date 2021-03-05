---
description: では、コアサーバーを選択して操作するためのポートサプライヤーがサポートされています。
title: IDebugPortSupplierEx2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierEx2 interface
ms.assetid: dae0050a-a50a-4f35-bfbd-e538f537b20f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bd166280ab75b6cb560d6936342d8c3905b87ade
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167114"
---
# <a name="idebugportsupplierex2"></a>IDebugPortSupplierEx2
では、コアサーバーを選択して操作するためのポートサプライヤーがサポートされています。

## <a name="syntax"></a>構文

```
IDebugPortSupplierEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポート供給業者は、このインターフェイスを実装して、使用するコアサーバーを選択できるようにします。

## <a name="methods"></a>メソッド
 次の表は、 **IDebugPortSupplierEx2** のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[SetServer](../../../extensibility/debugger/reference/idebugportsupplierex2-setserver.md)|ポートサプライヤーのコアサーバーを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Portpriv. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
