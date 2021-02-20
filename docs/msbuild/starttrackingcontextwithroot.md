---
title: StartTrackingContextWithRoot | Microsoft Docs
description: MSBuild StartTrackingContextWithRoot で、ルート マーカーを指定する応答ファイルを使用して追跡コンテキストを開始する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- StartTrackingContextWithRoot
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- StartTrackingContextWithRoot
ms.assetid: f6ef2b76-8035-4a14-8195-aa221c46ef48
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b52541c99fa81f31eddde8e6c12ad2eee04f3c20
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967047"
---
# <a name="starttrackingcontextwithroot"></a>StartTrackingContextWithRoot

応答ファイルにルート マーカーを指定し、追跡コンテキストを開始します。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI StartTrackingContextWithRoot(LPCTSTR intermediateDirectory, LPCTSTR taskName, LPCTSTR rootMarkerResponseFile);
```

#### <a name="parameters"></a>パラメーター

[入力] `intermediateDirectory`

 追跡ログを格納するディレクトリ。

[入力] `taskName`

 追跡コンテキストを識別します。 この名前はログ ファイル名の作成に使用されます。

[入力] `rootMarkerResponseFile`

 ルート マーカーを含む応答ファイルのパス名。 あるコンテキストのすべての追跡をグループ化するためにルート名が使用されます。

## <a name="return-value"></a>戻り値

 追跡コンテキストが作成された場合、**HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [StartTrackingContext](../msbuild/starttrackingcontext.md)