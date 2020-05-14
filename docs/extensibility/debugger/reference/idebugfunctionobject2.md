---
title: オブジェクト 2 を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c4150480d2e6686992d78727b6fed817da270145
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728429"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 関数を表し、インターフェイスを強化[します](../../../extensibility/debugger/reference/idebugfunctionobject.md)。

## <a name="syntax"></a>構文

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーター (EE) 関数を表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスのメソッドは、次の方法で**IDebugFunctionObject の**メソッドを延期します。

- メソッド**は**フラグを受け取ります。

- **メソッド**は、フラグとタイムアウトを受け取ります。

- メソッドは**長**さを取ります。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|評価フラグの設定とタイムアウト値を指定したコンストラクターを使用するオブジェクトを作成します。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|指定した長さを持つ文字列オブジェクトを作成します。|
|[評価](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|関数を呼び出し、結果の値をオブジェクトとして返します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: を使用します。

 アセンブリ:
