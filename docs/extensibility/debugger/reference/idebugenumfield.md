---
title: フィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7885f36a113809e81279498a769e257af4f1cde2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730174"
---
# <a name="idebugenumfield"></a>IDebugEnumField
このインターフェイスは、列挙型を表します。

## <a name="syntax"></a>構文

```
IDebugEnumField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは、列挙体を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)が返された`FIELD_TYPE_ENUM`[場合は、](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 インターフェイス`IDebugField`と`IDebugContainerField`インターフェイスのメソッドに加えて、このインターフェイスは次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|この列挙型の名前を説明する[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)を返します。|
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|指定された値に関連付けられた列挙定数の名前を返します。|
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|指定された列挙定数名に関連付けられた値を返します。|
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|指定された列挙定数名に関連付けられた値を返しますが、大文字と小文字は無視します。|

## <a name="remarks"></a>Remarks
 これは、実際に[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)を使用して位置にバインドされている基になるシンボルです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)
