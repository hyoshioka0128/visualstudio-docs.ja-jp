---
title: IDebugProgramEngines2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2
helpviewer_keywords:
- IDebugProgramEngines2 interface
ms.assetid: 53d648f0-6c11-4337-badd-c43f3872b62c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 56c74b265331b67564856baa003632d8d778bfb3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898900"
---
# <a name="idebugprogramengines2"></a>IDebugProgramEngines2
このインターフェイスは、プログラムノードがこのプログラムをデバッグできるすべてのデバッグエンジン (DE) を指定するために使用されます。

## <a name="syntax"></a>構文

```
IDebugProgramEngines2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE またはカスタムポートサプライヤーは、特定のプログラムに使用する特定の DE の確立をサポートするために、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugProgramNode2` このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProgramEngines2` ます。

|Method|説明|
|------------|-----------------|
|[EnumPossibleEngines](../../../extensibility/debugger/reference/idebugprogramengines2-enumpossibleengines.md)|このプログラムをデバッグできるすべての DEs を示します。|
|[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)|このプログラムのデバッグに使用する DE を選択します。|

## <a name="remarks"></a>解説
 ユーザーが DE を選択すると、 [Setengine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)を呼び出すことによってその選択がプログラムノードに登録されます。 選択したエンジンが、 [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)によって返されるエンジンになります。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)
