---
title: StopTrackingAndCleanup | Microsoft Docs
description: MSBuild で StopTrackingAndCleanup を使用して、すべての追跡を停止し、追跡セッションによって使用されているメモリを解放する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 05aec8bc85ac392670469da8073da02888b2f063
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048100"
---
# <a name="stoptrackingandcleanup"></a>StopTrackingAndCleanup

すべての追跡を停止し、追跡セッションで使用されているメモリを解放します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI StopTrackingAndCleanup(void);
```

## <a name="return-value"></a>戻り値

 追跡が停止された場合、 **HRESULT** に **SUCCEEDED** ビットが設定され、返されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [StartTrackingContext](../msbuild/starttrackingcontext.md)