---
description: このインターフェイスは、ポインター型を表します。
title: IDebugPointerField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField
helpviewer_keywords:
- IDebugPointerField interface
ms.assetid: d51bd5b2-f18e-4e27-b4fb-e6f652fbf635
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 568e442f5294b3aaa4cd8c99d7bbd1f769581ca6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087744"
---
# <a name="idebugpointerfield"></a>IDebugPointerField
このインターフェイスは、ポインター型を表します。

## <a name="syntax"></a>Syntax

```
IDebugPointerField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、ポインターを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)がを返す場合は、 [QueryInterface](/cpp/atl/queryinterface)を使用して、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスからこのインターフェイスを取得し `FIELD_TYPE_POINTER` ます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 インターフェイスとインターフェイスのメソッドに加え `IDebugField` て `IDebugContainerField` 、このインターフェイスは次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetDereferencedField](../../../extensibility/debugger/reference/idebugpointerfield-getdereferencedfield.md)|ポインターのターゲットを記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。|

## <a name="remarks"></a>注釈
 C/c + + では、配列が配列表記で使用されている場合、ポインターをコンテナーにすることができます。 たとえば、指定されたは `char *pString` 、 `pString` へのポインターの型を持ってい `char` ます。 `pString[3]` は、 `char` そのコンテナーの4番目の要素を参照するへのポインターであるコンテナーの型を持ちます。

## <a name="requirements"></a>要件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
