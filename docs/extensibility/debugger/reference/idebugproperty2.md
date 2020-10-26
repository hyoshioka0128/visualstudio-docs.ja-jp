---
title: IDebugProperty2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4b04abdac135143ccbbd1b8e5632bf85c974f29d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721226"
---
# <a name="idebugproperty2"></a>IDebugProperty2
このインターフェイスは、スタックフレームプロパティ、プログラムドキュメントプロパティ、またはその他のプロパティを表します。 通常、プロパティは、式の評価の結果です。

> [!NOTE]
> この "property" の使用は、クラスのメンバー変数と混同しないようにしてください。ただし、は、この `IDebugProperty2` ようなエンティティを表すことができます。

## <a name="syntax"></a>構文

```
IDebugProperty2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、特定の種類の値を表すために、このインターフェイスを実装します。 たとえば、値には、式の評価の結果としての数値、メモリの表示に使用されるメモリコンテキスト、レジスタとその値の一覧などがあります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)または[evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を呼び出して、評価の結果を表すこのインターフェイスを取得します。 `IDebugExpression2::EvaluateAsync`[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)インターフェイスを SDM に送信することによって、このインターフェイスを返します。このインターフェイスは、 [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)を呼び出してプロパティを取得します。

- [Getdebugproperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) は、関連付けられているスクリプトドキュメントを提供するために、このインターフェイスを返します。

- [Getreturnvalue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) 値は、関数の戻り値を表すために、このインターフェイスを返します。

- [Getdebugproperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) は、名前やメモリコンテキストなど、プログラムのさまざまなプロパティを表すために、このインターフェイスを返します。

- [Getdebugproperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) は、ローカル変数などのスタックフレームのさまざまなプロパティを表すために、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProperty2` ます。

|Method|説明|
|------------|-----------------|
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|プロパティを記述する [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を設定します。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|文字列のプロパティの値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|指定された参照の値からプロパティの値を設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|プロパティの子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|プロパティの親を返します。|
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|プロパティの最も派生したプロパティを示すプロパティを返します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|プロパティの値を構成するメモリのバイト数を返します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|プロパティ値のメモリコンテキストを返します。|
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|プロパティ値のサイズ (バイト単位) を返します。|
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|このプロパティの値への参照を返します。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|プロパティの拡張された情報を返します。|

## <a name="remarks"></a>解説
 インターフェイスによって表されるプロパティは、 `IDebugProperty2` 名前、型、およびアドレスを持つ値と考えることができます。 一般的に、は、 `IDebugProperty2` 親ノードと子ノードを持つ階層構造を持つ任意のものを表すことができます。

 通常、プロパティは一時的であり、現在のスタックフレームと同じ長さになります。たとえば、のようになります。 一方、 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) インターフェイスによって表される参照は、値がメモリ内に保持されている限り継続します。

 IDE では、インターフェイスを使用して、 `IDebugProperty2` ユーザーが実行時にプロパティを参照および変更できるようにすることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
