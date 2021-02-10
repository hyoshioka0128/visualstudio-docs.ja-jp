---
title: SetThreadCount | Microsoft Docs
description: MSBuild で SetThreadCount を使用して、グローバルなスレッド カウントを設定し、そのカウントを現在のスレッドに割り当てます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
apiname:
- SetThreadCount
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- SetThreadCount
ms.assetid: 335335a5-8ca0-4e18-95f5-62aa6a691386
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f7282b8c4589007492e48994628910b3a4ef0691
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99966163"
---
# <a name="setthreadcount"></a>SetThreadCount

グローバルなスレッド カウントを設定し、そのカウントを現在のスレッドに割り当てます。

## <a name="syntax"></a>構文

```cmd
HRESULT WINAPI SetThreadCount(int threadCount);
```

#### <a name="parameters"></a>パラメーター

[入力] `threadCount`

 使用するスレッドの数。

## <a name="return-value"></a>戻り値

 スレッド カウントが更新された場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*