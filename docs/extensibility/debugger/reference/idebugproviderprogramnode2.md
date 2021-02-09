---
title: IDebugProviderProgramNode2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e11472c2c883705c36ab71a37b1af10eb1cb5b10
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99909813"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
このインターフェイスは、プロセスの境界を越えてプログラムに関連するインターフェイスをマーシャリングします。

## <a name="syntax"></a>構文

```
IDebugProviderProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、プロセスの境界を越えたマーシャリングインターフェイスをサポートするために、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugProgramNode2` このインターフェイスを取得します。 このインターフェイスを取得できない場合、DE はインターフェイスのマーシャリングをサポートしません。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|プロセスの境界を越えて、指定されたインターフェイスを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、デバッグ中のプログラムとは別のプロセス空間で DE が実行されるときに実装されます。たとえば、デバッグ中のプログラムのプロセス空間ではなく、Visual Studio のプロセス領域で DE が実行されている場合などです。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
