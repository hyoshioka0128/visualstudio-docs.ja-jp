---
title: EndTrackingContext | Microsoft Docs
description: MSBuild EndTrackingContext を使用して現在の追跡コンテキストを終了するための構文、戻り値、および要件について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- EndTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- EndTrackingContext
ms.assetid: c2c5d794-8dc8-4594-8717-70dc79a0e75d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: da1ef921106732a7787f68a979bc88f3ac012b6d
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436663"
---
# <a name="endtrackingcontext"></a>EndTrackingContext

現在のコンテキストの追跡を終了します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI EndTrackingContext();
```

## <a name="return-value"></a>戻り値

コンテキストの追跡が終了した場合、 **HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

**ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [StartTrackingContext](../msbuild/starttrackingcontext.md)
