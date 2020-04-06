---
title: Iデバッグ関数の位置2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2
helpviewer_keywords:
- IDebugFunctionPosition2 interface
ms.assetid: a835f65b-91b0-48ad-8485-04534c814b1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c260b6316207b0079a2ca8893b851db8b1288ba6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728312"
---
# <a name="idebugfunctionposition2"></a>IDebugFunctionPosition2
このインターフェイスは、ソース ドキュメント内の関数の抽象位置を表します。

## <a name="syntax"></a>構文

```
IDebugFunctionPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、ソース ドキュメント内の関数の位置を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、BP_LOCATION[共用体](../../../extensibility/debugger/reference/bp-location.md)(具体的には[、BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)構造体) の一部として提供され、保留中のブレークポイントの作成に使用される[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)構造体の一部です。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugFunctionPosition2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetFunctionName](../../../extensibility/debugger/reference/idebugfunctionposition2-getfunctionname.md)|この位置が相対的な関数の名前を取得します。|
|[GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)|関数の先頭からのオフセットを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスで表される位置は、テキスト ベース、具体的には[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造です。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
