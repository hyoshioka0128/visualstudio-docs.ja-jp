---
title: CvCreateMarkerSeries 関数 | Microsoft Docs
description: コンカレンシー ビジュアライザー SDK 関数 CvCreateMarkerSeries (C ライブラリ) のリファレンス情報を参照してください。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- cvmarkers/CvCreateMarkerSeriesA
- cvmarkers/CvCreateMarkerSeriesW
helpviewer_keywords:
- CvCreateMarkerSeriesA method
- CvCreateMarkerSeriesW method
ms.assetid: e280530b-137a-43a7-8643-aa514ab86ed7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8915724c39a656917d6565c60ddc7dfbb0737564
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941035"
---
# <a name="cvcreatemarkerseries-function"></a>CvCreateMarkerSeries 関数
指定されたプロバイダーに対してマーカー系列を作成します。

## <a name="syntax"></a>構文

```C
_Check_return_ HRESULT CvCreateMarkerSeriesW(
    _In_ PCV_PROVIDER  pProvider,
    _In_ LPCWSTR pSeriesName,
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);

_Check_return_ HRESULT CvCreateMarkerSeriesA(
    _In_ PCV_PROVIDER  pProvider,
    _In_ LPCSTR pSeriesName,
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);
```

#### <a name="parameters"></a>パラメーター
 `pProvider` CvInitProvider により以前に初期化されたプロバイダー オブジェクト。 Nll は指定できません。

 `pSeriesName` マーカー系列名。 NULL は指定できませんが、空の文字列は指定できます。

 `ppMarkerSeries` マーカー系列コンテキストを格納する出力変数のアドレス。 Nll は指定できません。

## <a name="return-value"></a>戻り値
 マーカー系列が作成されると S_OK を、エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkers.h*

 **Unicode:** CvCreateMarkerSeriesW

 **ANSI:** CvCreateMarkerSeriesA

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)