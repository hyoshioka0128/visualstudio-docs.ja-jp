---
description: IDebugCodeContext2 インターフェイスを拡張して、モジュールインターフェイスとプロセスインターフェイスを取得できるようにします。
title: IDebugCodeContext3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4dd0ffb94f25ae8ac9566571a645d706fa224cd8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088316"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)インターフェイスを拡張して、モジュールインターフェイスとプロセスインターフェイスを取得できるようにします。

## <a name="syntax"></a>Syntax

```
IDebugCodeContext3 : IDebugCodeContext2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンによって実装され、デバッグパッケージによって使用さ [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] れます。

## <a name="methods"></a>メソッド
 このインターフェイスには、インターフェイスのメソッドに加えて、 `IDebugCodeContext2` 次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|デバッグモジュールのインターフェイスへの参照を取得します。|
|[GetProcess](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|デバッグプロセスのインターフェイスへの参照を取得します。|

## <a name="remarks"></a>注釈
 これは省略可能なインターフェイスであり、通常は実装する必要はありません。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
