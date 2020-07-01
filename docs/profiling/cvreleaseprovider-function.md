---
title: CvReleaseProvider 関数 | Microsoft Docs
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
ms.openlocfilehash: 0347d3e2345defb13a67e0e0d730e010be618a21
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332182"
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