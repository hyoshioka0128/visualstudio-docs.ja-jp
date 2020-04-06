---
title: オブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c04409fb695613fea5d54b285946c04719fbe5b0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716256"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは[、IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>構文

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは[、IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスを実装するオブジェクトのセットを提供するために、このインターフェイスを実装します。 [GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)メソッドが存在するため、これは標準の COM 列挙体ではありません。

## <a name="notes-for-callers"></a>発信者向けのメモ
- [このインターフェイスを](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)返します。

## <a name="methods-in-vtable-order"></a>V テーブル順のメソッド
 このインターフェイスは、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|列挙体から[IDebugObject オブジェクト](../../../extensibility/debugger/reference/idebugobject.md)の次のセットを取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|指定した数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|列挙を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|現在の列挙体のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|列挙体のエントリ数を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスを使用すると、デバッグ エンジンは配列内のオブジェクトのセットを列挙できます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)
