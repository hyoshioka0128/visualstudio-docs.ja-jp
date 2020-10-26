---
title: IDebugArrayObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugArrayObject2 interface
ms.assetid: be6e504d-4ab3-4141-a61b-0953ee0e038e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a8a6580d0cbdead7866bbc6dd106a2aa0ea56f76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736232"
---
# <a name="idebugarrayobject2"></a>IDebugArrayObject2
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 マネージ配列オブジェクトを表し、式エバリュエーター (EE) が配列のベースインデックス (下限) を決定できるようにします。

## <a name="syntax"></a>構文

```
IDebugArrayObject2 : IDebugArrayObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 これは、マネージデバッグエンジン (DE) によって実装されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-getbaseindices.md)|配列内の次元数を指定して、各インデックスのベースインデックス (下限) を取得します。|
|[HasBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-hasbaseindices.md)|配列にベースインデックス (下限) が定義されているかどうかを判断します。|

## <a name="remarks"></a>解説
 式エバリュエーターは、このインターフェイスを使用して、解析ツリー内のマネージ配列を表します。

## <a name="requirements"></a>必要条件
 ヘッダー: Ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
