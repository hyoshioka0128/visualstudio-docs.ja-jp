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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ff6b0449c877b5ae925ba2088917d7bacab4c34
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330667"
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