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
ms.openlocfilehash: 950c6a07a46f7f4b970912e576257a577021367e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632013"
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