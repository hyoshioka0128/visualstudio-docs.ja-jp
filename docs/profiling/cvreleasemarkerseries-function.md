---
title: CvReleaseMarkerSeries 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseMarkerSeries
helpviewer_keywords:
- CvReleaseMarkerSeries method
ms.assetid: 3b4711ee-e534-411d-9128-f69cd7932a48
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 84db5dac77fbbc51c9f1c0e24173dcc8ca1d68c1
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332193"
---
# <a name="cvreleasemarkerseries-function"></a>CvReleaseMarkerSeries 関数
マーカー系列をリリースします。 リリース後はマーカー系列オブジェクトを使用しないでください。使用すると、アプリケーションがクラッシュすることがあります。 マーカー系列のリリースに失敗すると、メモリ漏れが発生します。

## <a name="syntax"></a>構文

```C
HRESULT CvReleaseMarkerSeries(
   _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries
);
```

#### <a name="parameters"></a>パラメーター
 `pMarkerSeries` プロバイダー オブジェクト変数のアドレス。 アドレスには NULL を指定できません。変数には値を含めることができます。

## <a name="return-value"></a>戻り値
 マーカー系列がリリースされると S_OK を、エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkers.h*

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)