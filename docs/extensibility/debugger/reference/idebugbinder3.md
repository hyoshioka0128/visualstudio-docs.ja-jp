---
title: Iデバッグバインダー3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3
helpviewer_keywords:
- IDebugBinder3 interface
ms.assetid: 92353a74-dc74-4f93-8762-61d6b220478c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa85872337fdc1f7519d0de98cffe1436ef41c67
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735669"
---
# <a name="idebugbinder3"></a>IDebugBinder3
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、型、エイリアス、およびカスタム ビジュアライザー サービスへのアクセスを提供します。

## <a name="syntax"></a>構文

```
IDebugBinder3 : IDebugBinder
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジンは、エイリアス、カスタム ビジュアライザー サービス、およびオブジェクト型情報へのアクセスをサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [インターフェイス](../../../extensibility/debugger/reference/idebugbinder.md)は、[クエリ インターフェイス](/cpp/atl/queryinterface)を使用してこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは[、IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイスによって提供されるメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetMemoryObject](../../../extensibility/debugger/reference/idebugbinder3-getmemoryobject.md)|このオブジェクトがバインドされているメモリを表すメモリ オブジェクトを取得します。|
|[GetExceptionObjectAndType](../../../extensibility/debugger/reference/idebugbinder3-getexceptionobjectandtype.md)|このオブジェクトに関連付けられている例外 (存在する場合) を取得します。|
|[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)|名前を指定してエイリアスを取得します。|
|[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)|このオブジェクトのすべてのエイリアスの配列を取得します。|
|[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)|このオブジェクトに関連付けられている引数の型の数を取得します。|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)|このオブジェクトに関連付けられている引数の型のリストを取得します。|
|[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)|ビジュアライザー サービスへのインターフェイスを取得します。|
|[GetMemoryContext64](../../../extensibility/debugger/reference/idebugbinder3-getmemorycontext64.md)|オブジェクトの場所または 64 ビットメモリ アドレスをメモリ コンテキストに変換します。|

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
