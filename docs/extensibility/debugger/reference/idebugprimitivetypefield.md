---
description: IDebugField インターフェイスからのプリミティブ型の列挙値を表します。
title: IDebugPrimitiveTypeField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPrimitiveTypeField interface
ms.assetid: 73a428fd-797e-4ceb-8392-ba16f1c5226b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ba0fd92098d8089f6d80573c1db53e0b7e003b8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150303"
---
# <a name="idebugprimitivetypefield"></a>IDebugPrimitiveTypeField
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスからのプリミティブ型の列挙値を表します。

## <a name="syntax"></a>構文

```
IDebugPrimitiveTypeField : IDebugField
```

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetPrimitiveType](../../../extensibility/debugger/reference/idebugprimitivetypefield-getprimitivetype.md)|このフィールドに関連付けられているプリミティブ型を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
