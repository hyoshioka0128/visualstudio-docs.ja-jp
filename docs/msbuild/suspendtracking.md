---
title: SuspendTracking | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- SuspendTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- SuspendTracking
ms.assetid: f5e06e5a-8083-444c-99c1-07ba834226b5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d48c29b9dcca477c5a5470c443be08d5060b413d
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578111"
---
# <a name="suspendtracking"></a>SuspendTracking
現在のコンテキストで追跡を一時停止します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI SuspendTracking(void);
```

## <a name="return-value"></a>戻り値
 追跡が一時停止された場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目
- [ResumeTracking](../msbuild/resumetracking.md)