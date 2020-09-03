---
title: IDebugPrimitiveTypeField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPrimitiveTypeField interface
ms.assetid: 73a428fd-797e-4ceb-8392-ba16f1c5226b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 07cd3d1a1f80d1c5e816877b7e70a9e65d24d650
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80724274"
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
