---
description: このインターフェイスは、オブジェクトに関する追加情報を提供します。
title: IDebugObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c5e3b3f05ae205e30cff7085b71c1690d02c73e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084689"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、オブジェクトに関する追加情報を提供します。

## <a name="syntax"></a>Syntax

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、このインターフェイスを実装して、エイリアスと、オブジェクトに関する情報へのアクセスをサポートします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスは、 [QueryInterface](/cpp/atl/queryinterface)を使用してこのインターフェイスを取得できます。 また、このインターフェイスは [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) によって返されます。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 インターフェイスには、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスのメソッドに加えて、 `IDebugObject2` 次のものが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|このオブジェクトによって表されるプロパティをバッキングしている可能性のあるフィールドまたは変数 (存在する場合) を取得します。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|このオブジェクトの値を表すマネージコードオブジェクトを取得します。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|このオブジェクトの一意の ID を作成するか、既存のエイリアスを返します。|
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|このオブジェクトに関連付けられているエイリアス (存在する場合) を取得します。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|このオブジェクトの型を取得します。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|このオブジェクトがユーザーデータを表すかどうかを判断します。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|エディットコンティニュの状態が無効になっているかどうかを判断します。<br /><br /> カスタム式エバリュエーターは、このメソッドを実装していません (常にを返す必要があり `E_NOTIMPL` ます)。|

## <a name="remarks"></a>注釈
 エイリアスの詳細については、「 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 」を参照してください。

## <a name="requirements"></a>要件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
