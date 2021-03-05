---
description: IDebugBinder オブジェクトの動的フィールドを表します。
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
ms.openlocfilehash: 27fc3fb25b738db20d480a7a4542884dcb76123a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154031"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)オブジェクトの動的フィールドを表します。

## <a name="syntax"></a>構文

```
IDebugDynamicFieldCOMPlus : IDebugDynamicField
```

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|プリミティブ型を指定して型を取得します。|
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|トークンを指定して型を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
