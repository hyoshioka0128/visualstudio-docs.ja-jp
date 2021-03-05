---
description: デバッグオプションの修飾子を表します。
title: IDebugModOpt |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 047c01f78931e1b13110640952c67c11a68bc8a2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149861"
---
# <a name="idebugmodopt"></a>IDebugModOpt
デバッグオプションの修飾子を表します。

## <a name="syntax"></a>構文

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

## <a name="requirements"></a>必要条件
 ヘッダー: Sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
