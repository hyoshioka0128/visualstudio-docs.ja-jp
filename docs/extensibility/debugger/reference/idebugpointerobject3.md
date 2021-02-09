---
title: IDebugPointerObject3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPointerObject3 interface
ms.assetid: 11d26af4-1079-435e-96fa-d5269cbea8eb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0f4a87f9cf0bf64378e6dd5acba504d2da7b5d92
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844802"
---
# <a name="idebugpointerobject3"></a>IDebugPointerObject3
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 は、解析ツリー内のポインターを表し、 **IDebugPointerObject** インターフェイスを拡張します。

## <a name="syntax"></a>構文

```
IDebugPointerObject3 : IDebugPointerObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) は、このインターフェイスを実装します。

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetPointerAddress](../../../extensibility/debugger/reference/idebugpointerobject3-getpointeraddress.md)|ポインターのアドレスを取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
