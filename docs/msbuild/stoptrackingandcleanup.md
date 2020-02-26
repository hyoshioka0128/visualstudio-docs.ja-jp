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
ms.openlocfilehash: 4a80fcde7aeab601791c033bd21effce175b2cb9
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579567"
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