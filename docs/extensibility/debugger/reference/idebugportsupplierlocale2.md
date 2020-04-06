---
title: IDebug ポートサプライヤーロケール2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierLocale2 interface
ms.assetid: 910e7220-da2a-4339-9fff-9fb1bad3c28c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 98444ca60937d40262c92d89b8a6c48ed1a0b7ef
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724289"
---
# <a name="idebugportsupplierlocale2"></a>IDebugPortSupplierLocale2
ポート サプライヤーのロケールサポートを提供します。

## <a name="syntax"></a>構文

```
IDebugPortSupplierLocale2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 カスタム ポート サプライヤーは、ロケールを設定するためにこのインターフェイスを実装します。

## <a name="methods"></a>メソッド
 次の表に、**メソッド**を示します。

|Method|説明|
|------------|-----------------|
|[SetLocale](../../../extensibility/debugger/reference/idebugportsupplierlocale2-setlocale.md)|ポート サプライヤーのロケールを設定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: ポートプリフ.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
