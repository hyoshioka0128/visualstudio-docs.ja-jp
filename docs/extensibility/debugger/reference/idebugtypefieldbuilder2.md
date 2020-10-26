---
title: IDebugTypeFieldBuilder2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder2 interface
ms.assetid: 23911c5b-2bbf-4734-9976-87a0bd6ea36c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ed34284e373a7d96761aabe5a7f179367649bc0f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718305"
---
# <a name="idebugtypefieldbuilder2"></a>IDebugTypeFieldBuilder2
**IDebugTypeFieldBuilder**を拡張して、配列型を作成できるようにします。

## <a name="syntax"></a>構文

```
IDebugTypeFieldBuilder2 : IDebugTypeFieldBuilder
```

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、シンボルプロバイダーから取得できます。

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[CreateArrayOfType](../../../extensibility/debugger/reference/idebugtypefieldbuilder2-createarrayoftype.md)|指定した型とサイズの配列を作成します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
