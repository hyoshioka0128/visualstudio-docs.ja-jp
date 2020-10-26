---
title: IDebugCodeContext3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e3f81168d9af7fbbb93b5c59f3ab19a17107b56b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734187"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)インターフェイスを拡張して、モジュールインターフェイスとプロセスインターフェイスを取得できるようにします。

## <a name="syntax"></a>構文

```
IDebugCodeContext3 : IDebugCodeContext2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンによって実装され、デバッグパッケージによって使用さ [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] れます。

## <a name="methods"></a>メソッド
 このインターフェイスには、インターフェイスのメソッドに加えて、 `IDebugCodeContext2` 次のメソッドが実装されています。

|Method|説明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|デバッグモジュールのインターフェイスへの参照を取得します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|デバッグプロセスのインターフェイスへの参照を取得します。|

## <a name="remarks"></a>解説
 これは省略可能なインターフェイスであり、通常は実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
