---
title: ResumeTracking | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- ResumeTracking
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- ResumeTracking
ms.assetid: d637e019-7c50-4b0a-812e-bc822001e697
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6bb4663013a73d88ed7c2118816007705834162c
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77578451"
---
# <a name="resumetracking"></a>ResumeTracking
現在のコンテキストで追跡を再開します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI ResumeTracking();
```

## <a name="return-value"></a>戻り値
 追跡が再開された場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。 コンテキストが利用できず、追跡を再開できない場合、**E_FAIL** が返されます。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目
- [SuspendTracking](../msbuild/suspendtracking.md)