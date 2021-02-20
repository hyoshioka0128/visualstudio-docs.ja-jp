---
title: IDebugTypeFieldBuilder |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder interface
ms.assetid: 2dfed0be-6972-4bec-baec-f0b78df9ef97
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67a94f3f88d85d1e74ce7b1d67e1ef3d44546132
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965695"
---
# <a name="idebugtypefieldbuilder"></a>IDebugTypeFieldBuilder
型を表すフィールドを作成する機能を表します。

## <a name="syntax"></a>構文

```
IDebugTypeFieldBuilder : IUnknown
```

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、シンボルプロバイダーから取得されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[CreatePrimitive](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createprimitive.md)|プリミティブ型を表すオブジェクトを作成します。|
|[CreatePointerToType](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createpointertotype.md)|指定した型へのポインターを作成します。|

## <a name="requirements"></a>要件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
