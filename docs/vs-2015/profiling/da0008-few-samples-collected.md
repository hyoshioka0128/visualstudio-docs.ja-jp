---
title: 'DA0008: 少数のサンプルしか収集されていません | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DATooFewSamples
- vs.performance.8
- vs.performance.DA0008
- vs.performance.rules.DA0008
ms.assetid: 8a5b78aa-7b3d-476c-a47d-abfaff3fae7c
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 03fd9b6fd794320faf76119616900b79d5bf4333
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187854"
---
# <a name="da0008-few-samples-collected"></a>DA0008:少数のサンプルしか収集されていません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0008 |  
|Category |プロファイルツール使用法 |  
|プロファイル方法 |サンプリング |  
|Message |いくつかのサンプルだけが収集されました。 収集されるサンプル数を増やすには、実行時間を長くするか、サンプリング速度を上げてください。|  
|ルールの種類 |情報 |  
  
## <a name="cause"></a>原因  
 プロファイリング実行で少数のサンプルしか収集されませんでした。  
  
## <a name="rule-description"></a>ルールの説明  
 サンプリング メソッドを使用するときは、実際のプログラムの動作を表すようなデータを確実に得るために、統計的に有意な数のサンプルを収集する必要があります。 サンプリング エラーを最小限に抑えるには、プログラム命令の実行動作のサンプルを少なくとも 1000 個収集するようにしてください。 十分なサンプルを収集しない場合、プロファイル データを分析したときに誤った結果が得られる可能性があります。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 統計的に有意な結果を得るために、プロファイリングするアプリケーションの実行時間を長くするか、サンプリング速度を上げることを検討してください。 Visual Studio IDE でサンプリングレートを変更する方法の詳細については、「 [方法: サンプリングイベントを選択](../profiling/how-to-choose-sampling-events.md)する」を参照してください。 コマンド ラインからプロファイリング ツールを使用してサンプル速度を変更する方法の詳細については、「[VSPerfCmd](../profiling/vsperfcmd.md)」リファレンスの「[Timer](../profiling/timer.md)」を参照してください。
