---
description: このインターフェイスは DEBUG_PROPERTY_INFO 構造体を列挙します。
title: IEnumDebugPropertyInfo2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2
helpviewer_keywords:
- IEnumDebugPropertyInfo2
ms.assetid: fdea8262-40b8-473e-88ba-639e4c4648e6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fea2dc5cf958f87463af9dfca9f29bec5d01a82b
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224188"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
このインターフェイスは [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、特定のプロパティに関する情報を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Enumchildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を呼び出して、特定のプロパティの子を表すこのインターフェイスを取得します。 [Enumproperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)を呼び出して、特定のスタックフレームのプロパティを表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugPropertyInfo2` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|列挙シーケンス内の指定された数の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|列挙シーケンス内の指定された数の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|列挙子内の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体の数を取得します。|

## <a name="remarks"></a>解説
 一般に、プロパティは、名前、値、アドレス、型、および関連付けられているプロパティオブジェクトまたはスタックフレームに適したその他の情報を含めることができる情報の階層です。 詳細については、「 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
