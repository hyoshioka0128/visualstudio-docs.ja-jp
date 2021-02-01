---
title: CvReleaseProvider 関数 | Microsoft Docs
description: コンカレンシー ビジュアライザー SDK 関数 CvReleaseProvider (C ライブラリ) のリファレンス情報を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseProvider
helpviewer_keywords:
- CvReleaseProvider method
ms.assetid: 8d74379e-295d-452b-bd5f-0769df387d4f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5175f7f649dad3feed9f93a6e34ae5986ecda11b
ms.sourcegitcommit: d13f7050c873b6284911d1f4acf07cfd29360183
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "98686416"
---
# <a name="cvreleaseprovider-function"></a>CvReleaseProvider 関数
マーカー プロバイダーをリリースします。 マーカー プロバイダーをリリースしても、このプロバイダーの以前に作成したマーカー系列には影響がありません。 マーカー系列は、CvReleaseMarkerSeries を呼び出すことで個別にリリースする必要があります。 プロバイダーのリリースに失敗すると、メモリ漏れが発生します。

## <a name="syntax"></a>構文

```C
HRESULT CvReleaseProvider(
   _In_ PCV_PROVIDER pProvider
);
```

#### <a name="parameters"></a>パラメーター
 `pProvider` プロバイダー コンテキスト。 Nll は指定できません。

## <a name="return-value"></a>戻り値
 プロバイダーがリリースされると S_OK を、エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkers.h*

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)