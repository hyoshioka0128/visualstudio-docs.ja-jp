---
title: StartTrackingContext | Microsoft Docs
description: 追跡コンテキストを開始する MSBuild StartTrackingContext のパラメーター、要件、および戻り値について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StartTrackingContext
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StartTrackingContext
ms.assetid: 720cd295-38e7-4974-86db-b8106b1207ba
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 15121f050fd5af9a5cb36ce15ffc2161076df06d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929122"
---
# <a name="starttrackingcontext"></a>StartTrackingContext

追跡コンテキストを開始します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI StartTrackingContext(LPCTSTR intermediateDirectory, LPCTSTR taskName);
```

#### <a name="parameters"></a>パラメーター

[入力] `intermediateDirectory`

 追跡ログを格納するディレクトリ。

[入力] `taskName`

 追跡コンテキストを識別します。 この名前はログ ファイル名の作成に使用されます。

## <a name="return-value"></a>戻り値

 追跡コンテキストが作成された場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*
