---
title: クエリ 2 を実行するマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
- IDebugCustomAttributeQuery2 interface
ms.assetid: 7cfa23e4-a05a-47a3-af6c-bd40c655014b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6fe3969002c64ab361de76012c432e2bb5c61b5c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732491"
---
# <a name="idebugcustomattributequery2"></a>IDebugCustomAttributeQuery2
このフィールドのカスタム属性が存在するかどうかを確認し、存在する場合は属性情報を返します。

## <a name="syntax"></a>構文

```
IDebugCustomAttributeQuery2 : IDebugCustomAttributeQuery
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは、カスタム属性をサポートするために[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)を実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [インターフェイス](../../../extensibility/debugger/reference/idebugfield.md)からこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、インターフェイスのメソッド**を**示します。

|Method|説明|
|------------|-----------------|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)|カスタム属性が名前によって存在するかどうかを判断します。|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)|指定されたカスタム属性の属性情報を取得します。|

 **メソッドに**加えて、`IDebugCustomAttributeQuery2`次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)|このフィールドにアタッチされているすべてのカスタム属性の列挙子を取得します。|

## <a name="remarks"></a>Remarks
 メソッド[は](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)、このフィールドに定義されているすべてのカスタム属性の列挙子を返すことができます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
