---
title: DA0004:プロセッサ使用率が高くなっています | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DAHighProcessorUsage
- vs.performance.rules.DA0004
- vs.performance.DA0004
- vs.performance.4
ms.assetid: 2c4fb569-929e-4f1d-8c50-b590ee371351
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: b324d26d21920bae9f03f909b2eab0c1ce7ab419
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74777726"
---
# <a name="da0004-high-processor-usage"></a>DA0004:プロセッサ使用率が高くなっています

|||
|-|-|
|規則 ID|DA0004|
|カテゴリ|プロファイリング ツールの使用|
|プロファイル方法|インストルメンテーション<br /><br /> サンプリング|
|メッセージ|プロセッサ使用率が 75% を超えた状態が続いています。 CPU 主体のアプリケーションに適したサンプリング モードを使用することを検討してください。|
|規則の種類|情報|

 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。

## <a name="cause"></a>原因
 プロセッサ (CPU) 使用率は、インストルメンテーション メソッドを使用して収集されたプロファイル データで高くなっていました。 CPU 主体のアプリケーションをプロファイリングするときは、サンプリング プロファイリング方式の使用を検討してください。

## <a name="rule-description"></a>規則の説明
 このプロファイリングの実行中、プロセッサは常にビジー状態でした。 CPU 使用率はが高い場合、CPU 主体のアプリケーションであることを示している可能性があります。 インストルメント化によるプロファイリングは、CPU 使用率シナリオの調査には効果的ではありません。 ほとんどの時間をプロセッサ上の命令の実行に費やすアプリケーションをプロファイリングする場合、サンプリングの方が効果的です。

## <a name="how-to-fix-violations"></a>違反の修正方法
 関数のタイミングが必要な場合、またはプロセッサのボトルネックよりも入出力に関心がある場合以外は、インストルメンテーション メソッドではなく、サンプリング メソッドでアプリケーションのプロファイリングをやり直すことを検討してください。
