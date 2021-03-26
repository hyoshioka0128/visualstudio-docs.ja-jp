---
description: ポートサプライヤーのロケールサポートを提供します。
title: IDebugPortSupplierLocale2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierLocale2 interface
ms.assetid: 910e7220-da2a-4339-9fff-9fb1bad3c28c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: da7c08363d07e577d11259b8633aa15ac3cd0eb0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071767"
---
# <a name="idebugportsupplierlocale2"></a>IDebugPortSupplierLocale2
ポートサプライヤーのロケールサポートを提供します。

## <a name="syntax"></a>Syntax

```
IDebugPortSupplierLocale2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタムポート供給業者は、このインターフェイスを実装してロケールを設定します。

## <a name="methods"></a>メソッド
 次の表は、 **IDebugPortSupplierLocale2** のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[SetLocale](../../../extensibility/debugger/reference/idebugportsupplierlocale2-setlocale.md)|ポートサプライヤーのロケールを設定します。|

## <a name="requirements"></a>要件
 ヘッダー: Portpriv. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
