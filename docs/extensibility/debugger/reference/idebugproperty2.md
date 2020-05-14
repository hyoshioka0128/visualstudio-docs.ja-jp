---
title: Iデバッグプロパティ2 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721226"
---
# <a name="idebugproperty2"></a>IDebugProperty2
このインターフェイスは、スタック フレーム プロパティ、プログラム ドキュメント プロパティ、またはその他のプロパティを表します。 通常、このプロパティは式の評価の結果です。

> [!NOTE]
> この "property" の使用は、`IDebugProperty2`クラスのメンバー変数を意味するのと混同しないでください。

## <a name="syntax"></a>構文

```
IDebugProperty2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、特定の種類の値を表すためにこのインターフェイスを実装します。 たとえば、式の評価の結果として数値を数値、メモリの表示に使用されるメモリ コンテキスト、レジスタとその値の一覧などが値になります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [評価の](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)結果を表すこのインターフェイスを取得する評価[同期または評価非同期](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)を呼び出します。 `IDebugExpression2::EvaluateAsync`このインターフェイスを返す場合[は、プロパティ](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)を取得するために[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)を呼び出す SDM にインターフェイスを送信します。

- [この](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)インターフェイスを返して、関連付けられたスクリプト ドキュメントを提供します。

- [関数の](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)戻り値を表すインターフェイスを返します。

- [GetDebugProperty は](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)、名前やメモリ コンテキストなど、プログラムのさまざまなプロパティを表すこのインターフェイスを返します。

- [GetDebugProperty は](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)、ローカル変数などのスタック フレームのさまざまなプロパティを表すこのインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProperty2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[プロパティ情報を取得します。](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|プロパティを記述する[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造を埋めます。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|文字列からプロパティの値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|指定した参照の値からプロパティの値を設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|プロパティの子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|プロパティの親を返します。|
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|プロパティの最も派生したプロパティを記述するプロパティを返します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|プロパティの値を構成するメモリ バイトを返します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|プロパティ値のメモリ コンテキストを返します。|
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|プロパティ値のサイズ (バイト単位) を返します。|
|[参照を取得します。](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|このプロパティの値への参照を返します。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|プロパティの拡張情報を返します。|

## <a name="remarks"></a>Remarks
 `IDebugProperty2`インターフェイスによって表されるプロパティは、名前、型、およびアドレスを持つ値と考えることができます。 より一般的な用語では`IDebugProperty2`、 親ノードと子ノードを含む階層構造を持つものすべてを表すことができます。

 プロパティは通常一時的な状態で、たとえば現在のスタック フレームと同じ長さしか持続されません。 一方[、IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)インターフェイスで表される参照は、値がメモリ内に残っている間は続きます。

 IDE は、この`IDebugProperty2`インターフェイスを使用して、実行時にユーザーがプロパティを参照および変更できるようにします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
