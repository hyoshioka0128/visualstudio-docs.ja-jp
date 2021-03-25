---
description: このインターフェイスは、IDebugObject インターフェイスを実装するオブジェクトのコレクションを表します。
title: IEnumDebugObjects |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects
helpviewer_keywords:
- IEnumDebugObjects interface
ms.assetid: 0950364c-6c8a-4b6c-ba37-c6aa359fa72c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d9cd15c267906730ea94636e94978f5f77374e6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052828"
---
# <a name="ienumdebugobjects"></a>IEnumDebugObjects
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスを実装するオブジェクトのコレクションを表します。

## <a name="syntax"></a>Syntax

```
IEnumDebugObjects : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、このインターフェイスを実装して、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスを実装するオブジェクトのセットを提供します。 これは、 [GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md) メソッドが存在するため、標準の COM 列挙ではないことに注意してください。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [Getelements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md) は、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable の順序でのメソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)|列挙体から次の [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトのセットを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugobjects-skip.md)|指定された数のエントリをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugobjects-reset.md)|列挙体を最初のエントリにリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugobjects-clone.md)|現在の列挙体のコピーを取得します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugobjects-getcount.md)|列挙体のエントリ数を取得します。|

## <a name="remarks"></a>注釈
 このインターフェイスを使用すると、デバッグエンジンは配列内のオブジェクトのセットを列挙できます。

## <a name="requirements"></a>要件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)
