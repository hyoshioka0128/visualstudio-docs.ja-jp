---
description: このインターフェイスは、IDebugProcess2 実装者によって実装される拡張インターフェイスです。
title: IDebugProcessQueryProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8205b96723a1b48da46e6e19162c50139c9fe71d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166217"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
このインターフェイスは、 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 実装者によって実装される拡張インターフェイスです。 これにより、実装者はデバッグプロセス環境に関する情報を取得できます。

## <a name="syntax"></a>構文

```
IDebugProcessQueryProperties: IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグプロセスの実行環境に関する情報を取得するには、このインターフェイスを実装します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProcessQueryProperties` ます。

|メソッド|説明|
|------------|-----------------|
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|プロパティ値に対するクエリを行います。|
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|プロパティ値に対するクエリを行います。|

## <a name="remarks"></a>解説
 このインターフェイスはほとんど実装されていません。

## <a name="requirements"></a>必要条件
 ヘッダー: Portpriv. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
