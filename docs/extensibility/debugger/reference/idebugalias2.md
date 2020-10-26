---
title: IDebugAlias2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugAlias2 interface
ms.assetid: 5252dcbb-8bfe-4d8a-a8e5-b022b194df19
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 00e13da257c5477b3834ebb85bf6d481fe699362
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736354"
---
# <a name="idebugalias2"></a>IDebugAlias2
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 変数の数値の別名を表し、式エバリュエーター (EE) がエイリアスのアプリケーションドメインを取得できるようにします。

## <a name="syntax"></a>構文

```
IDebugAlias2 : IDebugAlias
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、マネージデバッグエンジン (DE) によって実装されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetAppDomainId](../../../extensibility/debugger/reference/idebugalias2-getappdomainid.md)|アプリケーションドメインの識別子を取得します。|

## <a name="remarks"></a>解説
 エイリアスは、文字列形式の10進数の後に # 文字が続きます (たとえば、1001 #)。

## <a name="requirements"></a>必要条件
 ヘッダー: Ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
