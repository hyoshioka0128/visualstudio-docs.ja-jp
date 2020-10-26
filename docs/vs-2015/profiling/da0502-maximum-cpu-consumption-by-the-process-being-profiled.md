---
title: 'DA0502: プロセスによる最大 CPU 使用量をプロファイリングしています | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DA0502
- vs.performance.DA0502
- vs.performance.502
ms.assetid: 1ee53df5-b0dc-4265-9d4f-527830d08725
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a47a9c5964ccf15d2c609233eb600f39bc3ad2d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205934"
---
# <a name="da0502-maximum-cpu-consumption-by-the-process-being-profiled"></a>DA0502:プロセスにより CPU の最大使用量がプロファイリングされています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0502 |  
|Category |リソースの監視 |  
|プロファイル方法 |All |  
|Message |この規則は情報のためだけに使用されます。 Process()\\% Processor Time カウンターはプロファイリングを行っているプロセスの CPU 使用量を測定します。 報告される値は、全測定期間を通じて観察された最大値です。|  
|ルールの種類 |情報 |  
  
 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  
  
## <a name="rule-description"></a>ルールの説明  
 このメッセージにより、アプリケーションの命令の実行中にプロセッサがビジー状態になった最大時間がパーセントで報告されます。 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値のうち、最も大きな値がこのメッセージによって報告されます。 複数のプロセッサが搭載されたコンピューターの場合、パーセントが 100% を超える可能性があります。  
  
## <a name="how-to-use-the-rule-data"></a>規則データの使用方法  
 規則の値を使用して、特定のプログラムの異なるバージョンやビルドを比較したり、さまざまなプロファイリング シナリオにおけるアプリケーションのパフォーマンスを確認したりします。
