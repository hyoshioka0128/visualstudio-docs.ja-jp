---
title: IDebugポートサプライヤーEx2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierEx2 interface
ms.assetid: dae0050a-a50a-4f35-bfbd-e538f537b20f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 26387618b320ed56ce754e64698fbb1c4223f2f6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724326"
---
# <a name="idebugportsupplierex2"></a>IDebugPortSupplierEx2
ポートサプライヤーがコアサーバーを選択して対話するサポートを提供します。

## <a name="syntax"></a>構文

```
IDebugPortSupplierEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、使用するコア サーバーを選択できるように、このインターフェイスを実装します。

## <a name="methods"></a>メソッド
 次の表に **、IDebugPortSupplierEx2**のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[SetServer](../../../extensibility/debugger/reference/idebugportsupplierex2-setserver.md)|ポート サプライヤーのコア サーバーを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: ポートプリフ.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
