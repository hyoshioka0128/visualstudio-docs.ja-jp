---
title: IDebugDynamicFieldCOMPlus |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus interface
ms.assetid: c3a25f27-327a-4bdb-b026-27d436ddcd0c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 768031d75537befb73a54166f5792b49574798a2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919915"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクトの動的フィールドを表します。

## <a name="syntax"></a>構文

```
IDebugDynamicFieldCOMPlus : IDebugDynamicField
```

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|プリミティブ型を指定して型を取得します。|
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|トークンを指定して型を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
