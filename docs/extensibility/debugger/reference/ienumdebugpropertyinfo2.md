---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2
helpviewer_keywords:
- IEnumDebugPropertyInfo2
ms.assetid: fdea8262-40b8-473e-88ba-639e4c4648e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bfa0f8feff6a53b84a6337e5bea8bdc622e19a20
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715351"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
このインターフェイスは[、DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、特定のプロパティの情報を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)を呼び出して、特定のプロパティの子を表すこのインターフェイスを取得します。 [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)を呼び出して、特定のスタック フレームのプロパティを表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugPropertyInfo2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|列挙体シーケンス内の指定した数の[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体を取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|列挙体シーケンス内の指定した数の[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|列挙子の[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体の数を取得します。|

## <a name="remarks"></a>Remarks
 一般に、プロパティは、名前、値、アドレス、および型、および関連付けられたプロパティ オブジェクトまたはスタック フレームに適切なその他の情報を含むことができる情報の階層です。 詳細については[、IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)
