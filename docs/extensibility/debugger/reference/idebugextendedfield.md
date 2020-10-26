---
title: IDebugExtendedField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExtendedField interface
ms.assetid: b491499c-af57-47da-87d6-34b7398f6591
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad10050aa157b4481fa2041ec5f322451983149f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729039"
---
# <a name="idebugextendedfield"></a>IDebugExtendedField
マネージコードジェネリックをサポートするために使用できるフィールドの型を拡張します。

## <a name="syntax"></a>構文

```
IDebugExtendedField : IDebugField
```

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)|指定した拡張フィールドの種類を取得します。|
|[IsClosedType](../../../extensibility/debugger/reference/idebugextendedfield-isclosedtype.md)|フィールドが閉じられた型を表すかどうかを判断します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
