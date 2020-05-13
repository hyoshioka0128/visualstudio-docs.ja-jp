---
title: オブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject
helpviewer_keywords:
- IDebugObject interface
ms.assetid: 05cd8bf4-c9ee-4b49-b782-2263c33067d6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6801176964a47646f03091131e1be89cf63c97f8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726314"
---
# <a name="idebugobject"></a>IDebugObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、バインダーがシンボルと式の値をカプセル化するために作成するオブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugObject : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、オブジェクトを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、式エバリュエーターが解析された式で使用するすべてのオブジェクトの基本クラスです。 [これは、Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)メソッドの呼び出しによって返されます。 [クエリ インターフェイスは](/cpp/atl/queryinterface)、このインターフェイスからより特化されたインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugObject`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)|オブジェクトのサイズを取得します。|
|[GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)|連続する一連のバイトとしてオブジェクトの値を取得します。|
|[SetValue](../../../extensibility/debugger/reference/idebugobject-setvalue.md)|連続するバイトからオブジェクトの値を設定します。|
|[SetReferenceValue](../../../extensibility/debugger/reference/idebugobject-setreferencevalue.md)|このオブジェクトの参照値を設定します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugobject-getmemorycontext.md)|オブジェクトの値のアドレスを表すメモリ コンテキストを取得します。|
|[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)|デバッグ エンジンのアドレス空間にマネージ オブジェクトのコピーを作成します。|
|[IsNullReference](../../../extensibility/debugger/reference/idebugobject-isnullreference.md)|このオブジェクトが null 参照であるかどうかをテストします。|
|[IsEqual](../../../extensibility/debugger/reference/idebugobject-isequal.md)|オブジェクトをこのオブジェクトと比較します。|
|[IsReadOnly](../../../extensibility/debugger/reference/idebugobject-isreadonly.md)|このオブジェクトが読み取り専用かどうかを判断します。|
|[IsProxy](../../../extensibility/debugger/reference/idebugobject-isproxy.md)|オブジェクトが透過プロキシかどうかを判断します。|

## <a name="remarks"></a>Remarks
 式エバリュエーターは、このインターフェイスを基本クラスとして使用して、解析ツリー内のオブジェクトを表します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)
- [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
