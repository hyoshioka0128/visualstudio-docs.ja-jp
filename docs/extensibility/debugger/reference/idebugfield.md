---
title: Iデバッグフィールド |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728756"
---
# <a name="idebugfield"></a>IDebugField
このインターフェイスは、フィールド、つまりシンボルまたは型の説明を表します。

## <a name="syntax"></a>構文

```
IDebugField : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは、すべてのフィールドの基本クラスとしてこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、すべてのフィールドの基本クラスです。 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)の戻り値に基づいて、このインターフェイスは[、QueryInterface](/cpp/atl/queryinterface)を使用して、より特化したインターフェイスを返す場合があります。 さらに、多くのインターフェイスは`IDebugField`さまざまなメソッドからオブジェクトを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugField`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|シンボルまたは型に関する表示可能な情報を取得します。|
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|フィールドの種類を取得します。|
|[Gettype](../../../extensibility/debugger/reference/idebugfield-gettype.md)|フィールドの種類を取得します。|
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|フィールドのコンテナーを取得します。|
|[GetAddress](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|フィールドのアドレスを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|フィールドのサイズをバイト単位で取得します。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|フィールドに関する拡張情報を取得します。|
|[Equal](../../../extensibility/debugger/reference/idebugfield-equal.md)|2 つのフィールドを比較します。|
|[ゲットタイプ情報](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|シンボルまたは型に関する型に依存しない情報を取得します。|

## <a name="remarks"></a>Remarks
 型は C 言語`typedef`と同等です。

 次の C++ 言語の`weather`例では、クラス型であり`sunny`、`stormy`シンボルです。

```cpp
class weather;
weather sunny;
weather stormy;
```

 フィールドがシンボルまたは型を表すかどうかは[、GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)を呼び出して[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)結果を調べることによって判断できます。 ビットが`FIELD_KIND_TYPE`設定されている場合、フィールドは型であり、ビットが`FIELD_KIND_SYMBOL`設定されている場合は、シンボルです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
