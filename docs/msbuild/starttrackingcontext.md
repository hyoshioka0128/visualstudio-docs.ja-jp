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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 13a22e3a20b69f62fe1e7d6c8e97eb80df6de1b6
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048151"
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

 追跡コンテキストが作成された場合、 **HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*
