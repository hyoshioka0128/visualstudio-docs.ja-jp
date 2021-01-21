---
title: WriteAllTLogs |Microsoft Docs
description: すべてのスレッドとコンテキストの追跡ログを書き込む WriteAllTLogs の構文、要件、および戻り値について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
apiname:
- WriteAllTLogs
apilocation:
- filetracker.dll
apitype: COM
helpviewer_keywords:
- WriteAllTLogs
ms.assetid: 1fa3e10b-263c-4960-a9ad-485c02a7a872
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 754b34b872ba0f0f677a194194b2ff893e7107e1
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93047479"
---
# <a name="writealltlogs"></a>WriteAllTLogs

すべてのスレッドとコンテキストの追跡ログを書き込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT WINAPI WriteAllTLogs(LPCTSTR intermediateDirectory, LPCTSTR tlogRootName);
```

#### <a name="parameters"></a>パラメーター

[入力] `intermediateDirectory`

 追跡ログを格納するディレクトリ。

[入力] `tlogRootName`

 ログ ファイル名のルート名。

## <a name="return-value"></a>戻り値

 追跡コンテキストが作成された場合、 **HRESULT** に **SUCCEEDED** ビットが設定されます。

## <a name="requirements"></a>必要条件

 **ヘッダー:** *FileTracker.h*

## <a name="see-also"></a>関連項目

- [WriteContextTLogs](../msbuild/writecontexttlogs.md)