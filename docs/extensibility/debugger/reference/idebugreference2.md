---
title: を参照してください。 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2
helpviewer_keywords:
- IDebugReference2 interface
ms.assetid: 3cfed312-f532-4bce-84a5-1677c14567d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 52f655afd35ed316080a3a85ccfae047aa50d87f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720265"
---
# <a name="idebugreference2"></a>IDebugReference2
このインターフェイスは、スタック フレーム プロパティまたはその他のプロパティへの参照を表します。

> [!NOTE]
> `IDebugReference2`は将来の使用のために予約されており、すべてのメソッドは`E_NOTIMPL`を返す必要があります。

## <a name="syntax"></a>構文

```
IDebugReference2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、特定の種類の値への参照を表すために、このインターフェイスを実装します。 たとえば、式の評価の結果として数値を数値、メモリの表示に使用されるメモリ コンテキスト、レジスタとその値の一覧などが値になります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するには[、GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)を呼び出します。 [親](../../../extensibility/debugger/reference/idebugreference2-getparent.md)と[派生ほとんどの参照](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)もこのインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugReference2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)|この参照を記述する[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体を取得します。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugreference2-setvalueasstring.md)|文字列からこの参照の値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugreference2-setvalueasreference.md)|別の参照からこの参照の値を設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)|この参照の子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugreference2-getparent.md)|この参照の親を取得します。|
|[GetDerivedMostReference](../../../extensibility/debugger/reference/idebugreference2-getderivedmostreference.md)|この参照の最も派生した参照を取得します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)|この参照が参照するメモリバイトを取得します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)|この参照のメモリ コンテキストを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugreference2-getsize.md)|この参照のサイズ (バイト単位) を取得します。|
|[SetReferenceType](../../../extensibility/debugger/reference/idebugreference2-setreferencetype.md)|この参照型を設定します。|
|[比較](../../../extensibility/debugger/reference/idebugreference2-compare.md)|この参照を他の参照と比較します。|

## <a name="remarks"></a>Remarks

> [!NOTE]
> この "property" の使用は、`IDebugReference2`クラスのメンバー変数を意味するのと混同しないでください。

- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)プロパティを表し`IDebugReference2`、プロパティへの参照を表します。

 プロパティと参照の主な違いは、プロパティがオブジェクトの名前付きインスタンスを参照し、参照が名前のないインスタンスを参照していることです。 たとえば、プロパティは プログラムのヒープ内のオブジェクトを参照`"a.b"`する場合があります。 別のプロパティは、同じオブジェクトを`"c.d"`と参照する場合があります。 このプロパティを参照する方法では、それが`"a.b"`必要`"c.d"`であるか、スコープ内にある必要があります。 この同じオブジェクトへの参照は名前なしです。オブジェクトは、そのオブジェクトのメモリが有効である限り参照できます。

 インターフェイス`IDebugProperty2`は、名前、型、およびアドレスを持つ値と考えることができます。 一`IDebugReference2`方、型と住所と考えることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [参照を取得します。](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)
