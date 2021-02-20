---
title: 不要項目の非表示の割合 | Microsoft Docs
description: 不要項目の非表示の割合の設定についてと、呼び出しツリーに表示されるエントリの数を制御する方法について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.filter
helpviewer_keywords:
- Concurrency Visualizer, Noise Reduction Percentage
ms.assetid: 1c10cd4c-2fdd-48c9-b562-a334b3b2df6c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 531ff082197ca1f7e63008aeda1c27e083b569de
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99922419"
---
# <a name="noise-reduction-percentage"></a>不要項目の非表示の割合
既定では、不要項目の非表示の割合の設定値は 2 です。 この設定値以上の包括時間の割合を持つエントリだけが、コール ツリーに表示されます。 設定を変更することによって、コール ツリーに表示されるエントリの数を制御できます。 たとえば、値を 10 に変更すると、10% 以上の包括時間を持つエントリだけがコール ツリーに表示されます。 この設定値を増やすと、プロセスのパフォーマンスに対する影響が大きいエントリに集中することができます。