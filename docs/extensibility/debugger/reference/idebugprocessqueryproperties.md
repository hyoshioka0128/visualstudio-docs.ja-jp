---
title: IDebugProcessQueryProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08abf401b4e8f0e7a33d882e8178d77e6f248318
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80723277"
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

## <a name="remarks"></a>注釈
 このインターフェイスはほとんど実装されていません。

## <a name="requirements"></a>必要条件
 ヘッダー: Portpriv. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
