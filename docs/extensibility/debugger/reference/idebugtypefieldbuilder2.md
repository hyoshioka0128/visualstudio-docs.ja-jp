---
title: フィールドビルダー2 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718305"
---
# <a name="idebugtypefieldbuilder2"></a>IDebugTypeFieldBuilder2
配列型を作成できるように**IDebugTypeFieldBuilder**を拡張します。

## <a name="syntax"></a>構文

```
IDebugTypeFieldBuilder2 : IDebugTypeFieldBuilder
```

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、シンボル プロバイダーから取得できます。

## <a name="methods"></a>メソッド
 [インターフェイスの](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)メソッドに加えて、このインターフェイスは次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[CreateArrayOfType](../../../extensibility/debugger/reference/idebugtypefieldbuilder2-createarrayoftype.md)|指定した型とサイズの配列を作成します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: を使用します。

 アセンブリ:
