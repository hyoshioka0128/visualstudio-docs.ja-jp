---
title: IDebug 拡張フィールド |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729039"
---
# <a name="idebugextendedfield"></a>IDebugExtendedField
マネージ コード ジェネリックをサポートするために使用できるフィールドの種類を拡張します。

## <a name="syntax"></a>構文

```
IDebugExtendedField : IDebugField
```

## <a name="methods"></a>メソッド
 [インターフェイス](../../../extensibility/debugger/reference/idebugfield.md)のメソッドに加えて、このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)|指定された拡張フィールドの種類を取得します。|
|[IsClosedType](../../../extensibility/debugger/reference/idebugextendedfield-isclosedtype.md)|フィールドがクローズ型を表すかどうかを判断します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: を使用します。

 アセンブリ:
