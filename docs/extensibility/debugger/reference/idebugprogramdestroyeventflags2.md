---
description: デバッグセッションを終了するときに、Visual Studio UI の既定の動作をデバッグエンジンがオーバーライドできるようにします。
title: IDebugProgramDestroyEventFlags2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 02b2d934c2a556d3556d494368145e52a8c97394
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168193"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
デバッグセッションを終了するときに、デバッグエンジンが UI の既定の動作をオーバーライドできるようにし [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="syntax"></a>構文

```
IDebugProgramDestroyEventFlags2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、デバッグエンジンによって実装されます。 これは、プロセスの有効期間中に複数のプログラムを作成して破棄する可能性のあるホストに便利です。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugProgramDestroyEventFlags2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|プログラムの破棄フラグを取得します。|

## <a name="remarks"></a>解説
 UI の既定の動作で [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は、すべてのプログラムがプログラム破棄イベントを送信した後にデザインモードに戻ります。 このインターフェイスを使用すると、デバッグエンジンでその動作を変更できます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
