---
title: GPU アクティビティ グラフ | Microsoft Docs
description: コンカレンシー ビジュアライザーで、システム上の DirectX アクティビティのレベルを表示する、GPU アクティビティ グラフについて理解します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.cpu.graph.gpu
ms.assetid: d7c769af-95fb-49a3-b5ab-deafecee46fa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 46f3e4ce7f155679bc3c701af90ff51e0fb20239
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907277"
---
# <a name="gpu-activity-graph"></a>GPU アクティビティ グラフ
コンカレンシー ビジュアライザーの GPU アクティビティ グラフには、一定期間使用した DirectX エンジン数によってシステム上の DirectX アクティビティのレベルが測定され、表示されます。  グラフには、具体的にどのエンジンが使用されたかは表示されません。  GPU の作業を処理しているエンジンは使用中と見なされます。

## <a name="gpu-activity-graph-colors"></a>GPU アクティビティ グラフの色
 緑は現在のプロセスによる DirectX エンジンの消費量を示しています。

 淡い灰色は、システム上の他のプロセスによる DirectX エンジンの消費量を示しています。 他のプロセスによる DirectX エンジンの消費量を減らすには、システム上で実行される他のプロセスの数を削減します。

 白はシステム上で利用可能な未使用の DirectX エンジンを示します。 さらに用途が見つかればプロセスで使用できるエンジンです。 一部のエンジンは、特定のタスクにしか使用できません。

## <a name="see-also"></a>関連項目
- [使用状況ビュー](../profiling/utilization-view.md)