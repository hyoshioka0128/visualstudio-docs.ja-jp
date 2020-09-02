---
title: 'DA0004: プロセッサ使用率が高くなっています | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DAHighProcessorUsage
- vs.performance.rules.DA0004
- vs.performance.DA0004
- vs.performance.4
ms.assetid: 2c4fb569-929e-4f1d-8c50-b590ee371351
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a0e14a7400b937c56c2aac49a43d1d59cf96eba0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158699"
---
# <a name="da0004-high-processor-usage"></a>DA0004:プロセッサ使用率が高くなっています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0004 |  
|Category |プロファイルツール使用法 |  
|プロファイル方法 |インストルメンテーションサンプリング |  
|Message |プロセッサ使用率は、常に75% を超えています。 CPU 主体のアプリケーションに適したサンプリング モードを使用することを検討してください。|  
|ルールの種類 |情報 |  
  
 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  
  
## <a name="cause"></a>原因  
 プロセッサ (CPU) 使用率の大きな割合を、インストルメンテーション メソッドを使用して収集されたプロファイル データが占めていました。 CPU 主体のアプリケーションをプロファイリングするときは、サンプリング プロファイリング方式の使用を検討してください。  
  
## <a name="rule-description"></a>ルールの説明  
 このプロファイリングの実行中、プロセッサは常にビジー状態でした。 CPU 使用率はが高い場合、CPU 主体のアプリケーションであることを示している可能性があります。 インストルメント化によるプロファイリングは、通常、CPU 使用シナリオの調査には効果的ではありません。 ほとんどの時間をプロセッサ上の命令の実行に費やすアプリケーションをプロファイリングする場合、通常はサンプリングの方が効果的です。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 関数のタイミングが必要な場合、またはプロセッサのボトルネックよりも入出力に関心がある場合以外は、インストルメンテーション メソッドではなく、サンプリング メソッドでアプリケーションのプロファイリングをやり直すことを検討してください。
