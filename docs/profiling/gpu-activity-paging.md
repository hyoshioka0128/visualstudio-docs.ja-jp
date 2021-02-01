---
title: GPU アクティビティ (ページング) | Microsoft Docs
description: コンカレンシー ビジュアライザーの [スレッド] タブの [GPU アクティビティ (ページング)] セグメントについて確認します。 このセグメントは、GPU がページング要求の処理に要した時間を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuactivity
- vs.cv.threads.timeline.gpupaging
ms.assetid: 95284ac5-3492-4f7b-a79f-7d2840a07679
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2bdf1fcffad90155baba8f92d11e31d1b316710b
ms.sourcegitcommit: 589d96700208bf22c8da9e26a1d2041fbf39b8f9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98801179"
---
# <a name="gpu-activity-paging"></a>GPU アクティビティ (ページング)
**[スレッド]** タブの **[GPU アクティビティ (ページング)]** セグメントは、GPU がページング要求の処理に要した時間を示します。  セグメントの長さは、GPU がダイレクト メモリ アクセス (DMA) ページング パケットを処理していた時間を表します。 通常、ページング パケットは CPU と GPU の間のメモリの転送に関連付けられています。

 GPU ページング セグメントを選択した場合、**[現在]** タブのレポートには処理された DMA パケットの情報が表示されます。 これには、パケットが DirectX に関連するハードウェア キューで待機していた時間、DMA パケットを送信したプロセス、パケットの処理に要した時間が含まれます。

## <a name="see-also"></a>関連項目
- [使用状況ビュー](../profiling/utilization-view.md)