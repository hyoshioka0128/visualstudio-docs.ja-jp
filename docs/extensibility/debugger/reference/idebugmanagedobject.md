---
title: IDebugManagedObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6fbd270aa1b65f05f308d41d22f154fb53b8833d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727684"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスを使用すると、式エバリュエーター (EE) は、値クラスのインスタンス (など) でプロパティやメソッドを呼び出し `System.Decimal` たり、デバッグ中のプログラムで [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) を呼び出さずに値を設定したりできます。

## <a name="syntax"></a>構文

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、変数などのマネージコードオブジェクトを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、値クラスのインスタンスを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)で[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスは、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)から継承されたメソッドに加えて、 `IDebugManagedObject` 次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|マネージコードオブジェクトを表し、適切なマネージコードインターフェイスを取得できるインターフェイスを返します。|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|このオブジェクトの値を、指定したマネージコードオブジェクトの値に設定します。|

## <a name="remarks"></a>解説
 式エバリュエーターは、このインターフェイスを使用して、マネージコードオブジェクトを解析ツリーに格納します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
