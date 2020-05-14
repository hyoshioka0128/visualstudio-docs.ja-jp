---
title: CvWriteAlert 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvWriteAlertVA
- cvmarkers/CvWriteAlertVW
- cvmarkers/CvWriteAlertA
- cvmarkers/CvWriteAlertW
helpviewer_keywords:
- CvWriteAlertVW method
- CvWriteAlertA method
- CvWriteAlertVA method
- CvWriteAlertW method
ms.assetid: 937aa9d6-278a-4df3-bef7-151441df16d5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4b7cc2316168d14c6c996c4d55065771c85ffdfc
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62989773"
---
# <a name="cvwritealert-function"></a>CvWriteAlert 関数
コンカレンシー ビジュアライザーのトレース ファイルにアラートを書き込みます。

## <a name="syntax"></a>構文

```C
HRESULT CvWriteAlertW(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ PCWSTR pMessage,
    ...
    );

HRESULT CvWriteAlertA(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ PCSTR pMessage,
    ...
    );

HRESULT CvWriteAlertVW(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ PCWSTR pMessage,
    _In_ va_list argList);

HRESULT CvWriteAlertVA(
    _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries,
    _In_ PCSTR pMessage,
    _In_ va_list argList);
```

#### <a name="parameters"></a>パラメーター
 `argList` 引数リスト。

 `pMarkerSeries` 有効なマーカー シリーズ コンテキスト。 Nll は指定できません。

 `pMessage` メッセージの書式設定文字列。 Nll は指定できません。

## <a name="return-value"></a>戻り値
 メッセージが書き込まれると S_OK を返します。 エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。

## <a name="requirements"></a>必要条件
 **ヘッダー:** *cvmarkers.h*

 **Unicode:** CvWriteAlertW、CvWriteAlertVW

 **ANSI:** CvWriteAlertA、CvWriteAlertVA

## <a name="see-also"></a>関連項目
- [C++ ライブラリ リファレンス](../profiling/cpp-library-reference.md)