---
description: デバッグセッションを終了するときに、Visual Studio UI の既定の動作をデバッグエンジンがオーバーライドできるようにします。
title: IDebugProgramDestroyEventFlags2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6cb54b3a88255f9102f617298ff23c3e117d3cdd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084234"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
デバッグセッションを終了するときに、デバッグエンジンが UI の既定の動作をオーバーライドできるようにし [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="syntax"></a>Syntax

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

## <a name="remarks"></a>注釈
 UI の既定の動作で [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は、すべてのプログラムがプログラム破棄イベントを送信した後にデザインモードに戻ります。 このインターフェイスを使用すると、デバッグエンジンでその動作を変更できます。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
