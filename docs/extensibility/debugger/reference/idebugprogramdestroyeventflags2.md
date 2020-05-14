---
title: イベントフラグ2 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722504"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
デバッグ セッションを終了するときに、デバッグ エンジンが[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]UI の既定の動作をオーバーライドできるようにします。

## <a name="syntax"></a>構文

```
IDebugProgramDestroyEventFlags2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、デバッグ エンジンによって実装されます。 これは、プロセスの存続期間にわたって複数のプログラムを作成および破棄するホストに役立ちます。

## <a name="methods"></a>メソッド
 次の表に`IDebugProgramDestroyEventFlags2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|プログラム破棄フラグを取得します。|

## <a name="remarks"></a>Remarks
 UI の既定の[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]動作では、すべてのプログラムがプログラム破棄イベントを送信した後にデザイン モードに戻ります。 このインターフェイスを使用すると、デバッグ エンジンがその動作を変更できます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: を使用します。

 アセンブリ:
