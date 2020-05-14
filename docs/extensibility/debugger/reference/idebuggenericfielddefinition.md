---
title: フィールド定義を使用するマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldDefinition interface
ms.assetid: b5a853b7-221e-4d62-8948-07423089d75d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 019633b62d46f6a8ac68e6f5f4abc888e6986ab1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728196"
---
# <a name="idebuggenericfielddefinition"></a>IDebugGenericFieldDefinition
マネージ コードジェネリック型のフィールドの定義を表します。

## <a name="syntax"></a>構文

```
IDebugGenericFieldDefinition : IUnknown
```

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[ConstructInstantiation](../../../extensibility/debugger/reference/idebuggenericfielddefinition-constructinstantiation.md)|引数型の配列を指定してフィールド インスタンスを構築します。|
|[GetFormalTypeParams](../../../extensibility/debugger/reference/idebuggenericfielddefinition-getformaltypeparams.md)|パラメーターの数を指定した型パラメーターを取得します。|
|[TypeParamCount](../../../extensibility/debugger/reference/idebuggenericfielddefinition-typeparamcount.md)|ジェネリック フィールドに関連付けられている型パラメーターの数を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: を使用します。

 アセンブリ:
