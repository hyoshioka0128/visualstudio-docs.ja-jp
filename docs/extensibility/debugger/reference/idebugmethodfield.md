---
title: IDebugMethodField |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727064"
---
# <a name="idebugmethodfield"></a>IDebugMethodField
このインターフェイスは、メソッドを記述します。

## <a name="syntax"></a>構文

```
IDebugMethodField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、メソッドを提供する特殊化です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)がを返す場合は、 [QueryInterface](/cpp/atl/queryinterface)を使用して、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスからこのインターフェイスを取得し `FIELD_TYPE_METHOD` ます。 さらに、メソッド、 [Getpropertygetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)、 [getpropertygetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)、および [enumconstructors](../../../extensibility/debugger/reference/idebugclassfield-enumconstructors.md)はすべてインターフェイスを返し `IDebugMethodField` ます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスと [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)|メソッドのパラメーターの列挙子を作成します。|
|[GetThis](../../../extensibility/debugger/reference/idebugmethodfield-getthis.md)|メソッドを格納しているオブジェクトの "this" ポインターを取得します。|
|[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)|メソッドのすべてのローカル変数の列挙子を作成します。|
|[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)|メソッドの選択されたローカル変数の列挙子を作成します。|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugmethodfield-iscustomattributedefined.md)|特定のカスタム属性が定義されているかどうかを判断します。|
|[EnumStaticLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumstaticlocals.md)|メソッドの静的ローカル変数の列挙子を作成します。|
|[GetGlobalContainer](../../../extensibility/debugger/reference/idebugmethodfield-getglobalcontainer.md)|メソッドのグローバルコンテナーを取得します。|
|[EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)|メソッドを呼び出すために必要な各引数の型の列挙子を作成します。|

## <a name="remarks"></a>解説
 メソッドには、ローカル変数だけでなく、パラメーターを含めることもできます。

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
