---
title: Iデバッグエイリアス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f2ceb87277460f65e52c35f02e7fbbd01da1101a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736515"
---
# <a name="idebugalias"></a>IDebugAlias
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 変数の数値エイリアスを表します。 エイリアスは、変数の名前とは異なる名前です。

## <a name="syntax"></a>構文

```
IDebugAlias : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーター (EE) は、変数の数値エイリアスをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
- [CreateAlias は](../../../extensibility/debugger/reference/idebugobject2-createalias.md)、特定のオブジェクトのエイリアスを作成します。 エイリアスを検索するには[、FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)または[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスでは、次のメソッドが`IDebugAlias`定義されています。

|Method|説明|
|------------|-----------------|
|[Getobject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|このエイリアスが参照するオブジェクトを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|エイリアス名を取得します。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|このオブジェクトに`ICorDebugValue`関するマネージ コード情報へのアクセスを提供するインターフェイスを取得します (マネージ コードのみ)。|
|[処分](../../../extensibility/debugger/reference/idebugalias-dispose.md)|このエイリアスを使用しなくなったものとしてマークします。|

## <a name="remarks"></a>Remarks
 エイリアスは、文字列形式の 10 進数の後に# 文字 (例: 1001#) を指定します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)
- [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)
- [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
