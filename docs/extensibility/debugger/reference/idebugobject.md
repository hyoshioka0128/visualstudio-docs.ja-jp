---
title: IDebugObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dc6fc188537799a8a3eeab66dd4af1d92ffb67db
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953579"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、シンボルと式の値をカプセル化するためにバインダーによって作成されるオブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、このインターフェイスを実装してオブジェクトを表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、解析された式で式エバリュエーターが使用するすべてのオブジェクトの基本クラスです。 これは、 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md) メソッドの呼び出しによって返されます。 [QueryInterface](/cpp/atl/queryinterface) は、このインターフェイスからより特殊化されたインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugObject` ます。

|Method|説明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|オブジェクトのサイズを取得します。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|オブジェクトの値を連続する一連のバイトとして取得します。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|オブジェクトの値を連続する一連のバイトから設定します。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|このオブジェクトの参照値を設定します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|オブジェクトの値のアドレスを表すメモリコンテキストを取得します。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|デバッグエンジンのアドレス空間にマネージオブジェクトのコピーを作成します。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|このオブジェクトが null 参照であるかどうかをテストします。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|オブジェクトとこのオブジェクトを比較します。|
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|このオブジェクトが読み取り専用かどうかを判断します。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|オブジェクトが透過プロキシかどうかを判断します。|

## <a name="remarks"></a>解説
 式エバリュエーターは、このインターフェイスを基底クラスとして使用して、解析ツリー内のオブジェクトを表します。

## <a name="requirements"></a>要件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [束縛](../../../extensibility/debugger/reference/idebugbinder-bind.md)
