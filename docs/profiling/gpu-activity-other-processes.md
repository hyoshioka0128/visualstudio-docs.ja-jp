---
title: GPU アクティビティ (他のプロセス) | Microsoft Docs
description: コンカレンシー ビジュアライザーのスレッド ビューの [GPU アクティビティ (他のプロセス)] セグメントについて学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuother
- vs.cv.threads.timeline.gpuactivity
ms.assetid: 8a68df65-eb63-452f-9285-fb4ffc92f2b2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e57d40910dfdff9b2eb1d5a9db76bac6ec8657d2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907246"
---
# <a name="gpu-activity-other-processes"></a>GPU アクティビティ (他のプロセス)
コンカレンシー ビジュアライザーのスレッド ビューの **[GPU アクティビティ (他のプロセス)]** セグメントは、GPU がシステム上の他のプロセスのために要求を処理していた時間を示します。 これらの要求はダイレクト メモリ アクセス (DMA) パケットとして GPU に送信されます。  セグメントの長さは GPU でパケットが処理されていた時間を表します。

 このようなセグメントを選択した場合、**[現在]** タブのレポートには処理されたパケットの情報が表示されます。  情報には、パケットが DirectX に関連するハードウェア キューで待機していた時間、パケットを送信したプロセス、パケットの処理に要した時間が含まれます。