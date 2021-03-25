---
description: このインターフェイスは、スタックフレームプロパティまたはその他のプロパティへの参照を表します。
title: IDebugReference2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6b1c30b2da2862e17a1ebf16cc41008341127c5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075758"
---
# <a name="idebugreference2"></a>IDebugReference2
このインターフェイスは、スタックフレームプロパティまたはその他のプロパティへの参照を表します。

> [!NOTE]
> `IDebugReference2` 将来使用するために予約されており、すべてのメソッドがを返す必要があり `E_NOTIMPL` ます。

## <a name="syntax"></a>Syntax

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、特定の種類の値への参照を表すために、このインターフェイスを実装します。 たとえば、値には、式の評価の結果としての数値、メモリの表示に使用されるメモリコンテキスト、レジスタとその値の一覧などがあります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、 [Getreference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md) を呼び出します。 [GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md) と [GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md) も、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugReference2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|この参照を記述する [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体を取得します。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|文字列からこの参照の値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|この参照の値を別の参照から設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|この参照の子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|この参照の親を取得します。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|この参照の最も派生した参照を取得します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|この参照が参照するメモリのバイト数を取得します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|この参照のメモリコンテキストを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|この参照のサイズ (バイト単位) を取得します。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|この参照型を設定します。|
|[比較](../../../extensibility/debugger/reference/idebugreference2-compare.md)|この参照と別の参照を比較します。|

## <a name="remarks"></a>注釈

> [!NOTE]
> この "property" の使用は、クラスのメンバー変数と混同しないようにしてください。ただし、は、この `IDebugReference2` ようなエンティティを表すことができます。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) はプロパティを表し、 `IDebugReference2` はプロパティへの参照を表します。通常は、デバッグ中のプログラム内のオブジェクトへの参照です。

 プロパティと参照の主な違いは、プロパティがオブジェクトの名前付きインスタンスを参照し、参照が名前のないインスタンスを参照していることです。 たとえば、プロパティは、によってプログラムのヒープ内のオブジェクトを参照でき `"a.b"` ます。 別のプロパティはと同じオブジェクトを参照する場合があり `"c.d"` ます。 このプロパティを参照する方法では、 `"a.b"` またはがスコープ内にある必要があり `"c.d"` ます。 この同じオブジェクトへの参照は無名です。オブジェクトのメモリが有効である限り、オブジェクトを参照できます。

 インターフェイスは、 `IDebugProperty2` 名前、型、およびアドレスを持つ値と考えることができます。 一方、は、 `IDebugReference2` 型とアドレスとして考えることができます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)
