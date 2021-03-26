---
description: デバッグオプションの修飾子を表します。
title: IDebugModOpt |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb235d58c254d130636da0f4b97961c11f9a372
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087900"
---
# <a name="idebugmodopt"></a>IDebugModOpt
デバッグオプションの修飾子を表します。

## <a name="syntax"></a>Syntax

```
IDebugModOpt : IUnknown
```

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 クラスまたはメソッドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトから取得されます。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|省略可能な修飾子のリストを取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
