---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField
helpviewer_keywords:
- IDebugPointerField interface
ms.assetid: d51bd5b2-f18e-4e27-b4fb-e6f652fbf635
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a69797cc513b96c364f0357f22788fc9bcd65657
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725600"
---
# <a name="idebugpointerfield"></a>IDebugPointerField
このインターフェイスは、ポインター型を表します。

## <a name="syntax"></a>構文

```
IDebugPointerField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは、ポインターを表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)が返された`FIELD_TYPE_POINTER`[場合は、](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 インターフェイス`IDebugField`と`IDebugContainerField`インターフェイスのメソッドに加えて、このインターフェイスは次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetDereferencedField](../../../extensibility/debugger/reference/idebugpointerfield-getdereferencedfield.md)|ポインターのターゲットを記述する[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)を返します。|

## <a name="remarks"></a>Remarks
 C/C++ では、ポインターを配列表記と共に使用する場合、ポインターをコンテナーにすることができます。 たとえば、`char *pString`は、`pString`へのポインター型を`char`持っています。 `pString[3]`は、そのコンテナーの 4 番目の要素`char`を参照するポインターであるコンテナーの型を持ちます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
