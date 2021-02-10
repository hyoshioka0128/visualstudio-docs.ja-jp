---
title: CvLeaveSpan 関数 | Microsoft Docs
description: コンカレンシー ビジュアライザー SDK 関数 CvLeaveSpan (C ライブラリ) のリファレンス情報を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvLeaveSpan
helpviewer_keywords:
- CvLeaveSpan method
ms.assetid: 3bf65fdf-a471-4efd-ac7a-03e701bbae5d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: da049fc5cc96e9eaa6830159db8c60f9469e2ac4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948258"
---
# <a name="cvleavespan-function"></a>CvLeaveSpan 関数
スパンの終了を示します。

## <a name="syntax"></a>構文

```C
HRESULT CvLeaveSpan(
   _In_ PCV_SPAN pSpan
);
```

#### <a name="parameters"></a>パラメーター
 `pSpan` CvEnterSpan* を以前に呼び出したときに返されたスパン オブジェクト。 Nll は指定できません。

## <a name="return-value"></a>戻り値
 メッセージが書き込まれると S_OK を返します。 エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkers.h*

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)