---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e468b5a282ffb5466d57a3c9b1a37aa3ae8643ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726074"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、オブジェクトに関する追加情報を提供します。

## <a name="syntax"></a>構文

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、別名のサポートとオブジェクトに関する情報へのアクセスを提供するために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [インターフェイス](../../../extensibility/debugger/reference/idebugobject.md)は、[クエリ インターフェイス](/cpp/atl/queryinterface)を使用してこのインターフェイスを取得できます。 また[、GetObject はこの](../../../extensibility/debugger/reference/idebugalias-getobject.md)インターフェイスを返します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 [インターフェイス](../../../extensibility/debugger/reference/idebugobject.md)のメソッドに加えて、インターフェイスは`IDebugObject2`、次を実装します。

|Method|説明|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|このオブジェクトによって表されるプロパティをバッキングしている可能性があるフィールドまたは変数 (存在する場合) を取得します。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|このオブジェクトの値を表すマネージ コード オブジェクトを取得します。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|このオブジェクトの一意の ID を作成するか、既存のエイリアスを返します。|
|[エイリアスを取得します。](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|このオブジェクトに関連付けられているエイリアス (存在する場合) を取得します。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|このオブジェクトの型を取得します。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|このオブジェクトがユーザー データを表すかどうかを判断します。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|エディット コンティニュの状態が有効でなくなったかどうかを判断します。<br /><br /> カスタム式エバリュエーターは、このメソッドを実装しません`E_NOTIMPL`(常に返す必要があります)。|

## <a name="remarks"></a>Remarks
 エイリアスに関する説明については[、「IDebugAlias」](../../../extensibility/debugger/reference/idebugalias.md)を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [Getobject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
