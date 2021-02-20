---
title: marker_series::is_enabled メソッド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_series::is_enabled
helpviewer_keywords:
- Concurrency, diagnostic::marker_series::is_enabled method
ms.assetid: 8ce4dd50-ca29-4c72-98d6-582693f7d501
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e68ec76737308d9bc9478f4106420626389f5eeb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917727"
---
# <a name="marker_seriesis_enabled-method"></a>marker_series::is_enabled メソッド
任意のセッションでプロバイダーが有効にされているかどうかを調べます。

## <a name="syntax"></a>構文

```cpp
bool is_enabled();
bool is_enabled(
   marker_importance _Importance,
   int _Category
);
```

#### <a name="parameters"></a>パラメーター
 `_Importance` 重要度レベル。

 `_Category` カテゴリ。

## <a name="return-value"></a>戻り値

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkersobj.h*

 **名前空間:** Concurrency::diagnostic

## <a name="see-also"></a>関連項目
- [marker_series クラス](../profiling/marker-series-class.md)