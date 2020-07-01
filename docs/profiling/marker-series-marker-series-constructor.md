---
title: marker_series::marker_series コンストラクター | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkersobj/Concurrency, diagnostic::marker_series::marker_series
helpviewer_keywords:
- Concurrency, diagnostic::marker_series constructor
ms.assetid: 042c7d23-f1d8-4e09-9e76-a21c30243790
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 78b2e80611983e69f11465269dcf15dad7d6351e
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329695"
---
# <a name="marker_seriesmarker_series-constructor"></a>marker_series::marker_series コンストラクター
`marker_series` クラスの新しいインスタンスを初期化します。

## <a name="syntax"></a>構文

```cpp
marker_series();
marker_series(
   _In_ LPCTSTR _SeriesName
);
marker_series(
   _In_ const GUID* _ProviderGuid
);
marker_series(
   _In_ const GUID* _ProviderGuid,
   _In_ LPCTSTR _SeriesName
);
```

#### <a name="parameters"></a>パラメーター
 `_SeriesName` 作成するシリーズの名前。

 `_ProviderGuid` シリーズのプロバイダーの GUID。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkersobj.h*

 **名前空間:** Concurrency::diagnostic

## <a name="see-also"></a>関連項目
- [marker_series クラス](../profiling/marker-series-class.md)