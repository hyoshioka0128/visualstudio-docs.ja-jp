---
title: プログラムエンジン2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2
helpviewer_keywords:
- IDebugProgramEngines2 interface
ms.assetid: 53d648f0-6c11-4337-badd-c43f3872b62c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 94df9acc6a0478ba2cb36022bc8618c69be97b8c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722402"
---
# <a name="idebugprogramengines2"></a>IDebugProgramEngines2
このインターフェイスは、プログラム ノードでこのプログラムをデバッグできるすべての可能なデバッグ エンジン (DE) を指定するために使用されます。

## <a name="syntax"></a>構文

```
IDebugProgramEngines2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE またはカスタム ポート サプライヤーは、特定のプログラムに使用する特定の DE の確立をサポートするために[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[QueryInterface](/cpp/atl/queryinterface)インターフェイスを取得するには`IDebugProgramNode2`、インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProgramEngines2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[EnumPossibleEngines](../../../extensibility/debugger/reference/idebugprogramengines2-enumpossibleengines.md)|このプログラムをデバッグできるすべての D を示します。|
|[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)|このプログラムのデバッグに使用する DE を選択します。|

## <a name="remarks"></a>Remarks
 ユーザーが DE を選択すると、その選択は[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)を呼び出すことによってプログラム ノードに登録されます。 選択したエンジンは[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)によって返されるエンジンになります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)
