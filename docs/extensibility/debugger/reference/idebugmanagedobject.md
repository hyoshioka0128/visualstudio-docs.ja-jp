---
title: オブジェクトを管理する |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727684"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスを使用すると、式エバリュエーター (EE) は、値クラスのインスタンス`System.Decimal`(たとえば) のプロパティまたはメソッドを呼び出し、デバッグ中のプログラムで[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)を呼び出さずに値を設定できます。

## <a name="syntax"></a>構文

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、変数などのマネージ コード オブジェクトを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するには、値クラスのインスタンスを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)で[GetManagedDebugObject](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [から](../../../extensibility/debugger/reference/idebugobject.md)継承されたメソッドに加えて、インターフェイスは`IDebugManagedObject`、次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|マネージ コード オブジェクトを表し、適切なマネージ コード インターフェイスを取得できるインターフェイスを返します。|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|このオブジェクトの値を、指定したマネージ コード オブジェクトの値に設定します。|

## <a name="remarks"></a>Remarks
 式エバリュエーターは、このインターフェイスを使用して、解析ツリーにマネージ コード オブジェクトを格納します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [評価](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
