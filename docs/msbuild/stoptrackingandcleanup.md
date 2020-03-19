---
title: StopTrackingAndCleanup | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StopTrackingAndCleanup
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StopTrackingAndCleanup
ms.assetid: 9f8c5994-2dfc-43c3-a5fb-89b2f8990429
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ee30bf031761fa7920dadad04d8f17a1bcc0b3a2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631992"
---
# <a name="stoptrackingandcleanup"></a>StopTrackingAndCleanup

すべての追跡を停止し、追跡セッションで使用されているメモリを解放します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI StopTrackingAndCleanup(void);
```

## <a name="return-value"></a>戻り値

 追跡が停止された場合、**HRESULT** に **SUCCEEDED** ビットが設定され、返されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [StartTrackingContext](../msbuild/starttrackingcontext.md)