---
title: フィールドビルダー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder interface
ms.assetid: 2dfed0be-6972-4bec-baec-f0b78df9ef97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 81532e2616eefb9cb584eae1a70371fd2f963be1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718389"
---
# <a name="idebugtypefieldbuilder"></a>IDebugTypeFieldBuilder
型を表すフィールドを作成する機能を表します。

## <a name="syntax"></a>構文

```
IDebugTypeFieldBuilder : IUnknown
```

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、シンボル プロバイダーから取得されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[CreatePrimitive](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createprimitive.md)|プリミティブ型を表すオブジェクトを作成します。|
|[CreatePointerToType](../../../extensibility/debugger/reference/idebugtypefieldbuilder-createpointertotype.md)|指定した型へのポインターを作成します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: を使用します。

 アセンブリ:
