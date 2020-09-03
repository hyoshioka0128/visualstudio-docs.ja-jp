---
title: IDebugProgramDestroyEventFlags2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d869304dd8b6dc82db78cc09ed9d51a54acdc3c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722504"
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

## <a name="remarks"></a>注釈
 UI の既定の動作で [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] は、すべてのプログラムがプログラム破棄イベントを送信した後にデザインモードに戻ります。 このインターフェイスを使用すると、デバッグエンジンでその動作を変更できます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
