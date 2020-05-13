---
title: メソッドフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField
helpviewer_keywords:
- IDebugMethodField interface
ms.assetid: a7dc9030-fc98-4cf1-b943-37a4003300b6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 061035933e57ea4ca8e7857f68ac3d6311bae32c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727064"
---
# <a name="idebugmethodfield"></a>IDebugMethodField
このインターフェイスはメソッドを記述します。

## <a name="syntax"></a>構文

```
IDebugMethodField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは[、IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、メソッドを提示する特殊化です。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)が`FIELD_TYPE_METHOD`[返す場合](../../../extensibility/debugger/reference/idebugcontainerfield.md)は、インターフェイスからこのインターフェイスを取得するのに[は、クエリ インターフェイス](/cpp/atl/queryinterface)を使用します。 さらに、メソッド、 [GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md) [、GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)、および[列挙コンストラクター](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)のすべてがインターフェイスを`IDebugMethodField`返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスのメソッドに加えて、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)[このインターフェイスは](../../../extensibility/debugger/reference/idebugcontainerfield.md)、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)|メソッドのパラメーターの列挙子を作成します。|
|[GetThis](../../../extensibility/debugger/reference/idebugmethodfield-getthis.md)|メソッドを含むオブジェクトの "this" ポインターを取得します。|
|[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)|メソッドのすべてのローカル変数の列挙子を作成します。|
|[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)|メソッドの選択したローカル変数の列挙子を作成します。|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugmethodfield-iscustomattributedefined.md)|特定のカスタム属性が定義されているかどうかを判断します。|
|[EnumStaticLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumstaticlocals.md)|メソッドの静的ローカル変数の列挙子を作成します。|
|[GetGlobalContainer](../../../extensibility/debugger/reference/idebugmethodfield-getglobalcontainer.md)|メソッドのグローバル コンテナーを取得します。|
|[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)|メソッドの呼び出しに必要な各引数の型の列挙子を作成します。|

## <a name="remarks"></a>Remarks
 メソッドには、パラメーターとローカル変数を含めることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
