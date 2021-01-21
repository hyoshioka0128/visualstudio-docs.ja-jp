---
title: SuspendTracking | Microsoft Docs
description: 現在のコンテキストでの追跡を一時停止する MSBuild SuspendTracking の構文、要件、および戻り値について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 164e1a11c7d107bf1d98419d77fdc50ed353f93b
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048089"
---
# <a name="suspendtracking"></a>SuspendTracking

現在のコンテキストで追跡を一時停止します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI SuspendTracking(void);
```

## <a name="return-value"></a>戻り値

 追跡が一時停止された場合、 **HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [ResumeTracking](../msbuild/resumetracking.md)