---
title: IDebugField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField
helpviewer_keywords:
- IDebugField interface
ms.assetid: adecdd1c-b1b9-4027-92da-74cbe910636f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8c7a25246f42d288020481330fe60e312849862d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728756"
---
# <a name="idebugfield"></a>IDebugField
このインターフェイスは、フィールド、つまりシンボルまたは型の説明を表します。

## <a name="syntax"></a>構文

```
IDebugField : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、このインターフェイスをすべてのフィールドの基本クラスとして実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、すべてのフィールドの基本クラスです。 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)の戻り値に基づいて、このインターフェイスは[QueryInterface](/cpp/atl/queryinterface)を使用してより特殊化されたインターフェイスを返す場合があります。 また、多くのインターフェイスは、 `IDebugField` さまざまなメソッドからオブジェクトを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugField` ます。

|Method|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|記号または型に関する参照可能情報を取得します。|
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|フィールドの種類を取得します。|
|[GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)|フィールドの型を取得します。|
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|フィールドのコンテナーを取得します。|
|[GetAddress](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|フィールドのアドレスを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|フィールドのサイズ (バイト単位) を取得します。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|フィールドに関する拡張情報を取得します。|
|[Equal](../../../extensibility/debugger/reference/idebugfield-equal.md)|2つのフィールドを比較します。|
|[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|記号または型に関する型に依存しない情報を取得します。|

## <a name="remarks"></a>解説
 型は C 言語に相当 `typedef` します。

 次の C++ 言語の例で `weather` は、はクラス型であり、 `sunny` と `stormy` は記号です。

```cpp
class weather;
weather sunny;
weather stormy;
```

 フィールドがシンボルまたは型を表すかどうかを判断するには、 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) を呼び出し、 [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) の結果を調べます。 ビットが設定されている場合、 `FIELD_KIND_TYPE` フィールドは型であり、ビットが設定されている場合 `FIELD_KIND_SYMBOL` は記号になります。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
