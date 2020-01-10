---
title: 'DA0503: プロセスのワーキング セット平均バイト数がプロファイリングされています | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.503
- vs.performance.DA0503
- vs.performance.rules.DA0503
ms.assetid: 9047a494-eaaf-4679-b422-c64e8bde77a4
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 31d36a89473cd0c6a0b55e484fee2ce1d7045b15
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850892"
---
# <a name="da0503-average-working-set-in-bytes-for-the-process-being-profiled"></a>DA0503: プロセスのワーキング セット平均バイト数がプロファイリングされています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0503 |  
|Category |リソースの監視 |  
|プロファイル方法 |All |  
|Message |この情報は情報収集のみを対象としています。 Process Working Set カウンターは、プロファイリングを行っているプロセスによる物理メモリの使用量を測定します。 報告される値は、全測定期間を通じて計算された平均値です。|  
|ルールの種類 |情報 |  
  
 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  
  
## <a name="rule-description"></a>規則の説明  
 このメッセージにより、プロセスが現在使用している物理メモリ量 (ワーキング セット) の平均がバイト単位で報告されます。 プロセスのワーキング セットは、物理メモリに現在常駐しているプロセス アドレス空間のページを表します。  
  
 報告された値には、プロセスが参照する共有メモリ セグメントの常駐ページが含まれます。 プロセスが参照する共有 DLL は、測定対象の共有メモリ セグメントに含まれます。 プロセスのワーキング セットの値は、プロセスによって割り当てられた仮想メモリ量よりも大きくなる場合があります。これは、共有メモリ セグメントが存在するためです。  
  
 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値の平均値が、このメッセージによって報告されます。  
  
 プロセスのワーキング セットのサイズには、プロセスが現在使用している仮想メモリ量が反映されます。 これは、アプリケーションの実行に使用できる物理メモリ (または RAM) の量と、実行中の他のプロセスによる物理メモリの競合の影響も受けます。 物理メモリが制約されている場合、オペレーティング システムがプロセス ワーキング セットの非アクティブなページを定期的に適切にトリミングして、アクティブなプロセス全体でメモリ使用量を均衡化するため、プロセス ワーキング セットの値は大幅に変わる傾向があります。  
  
 プロセスのワーキング セットの詳細については、MSDN の Windows のメモリ管理のドキュメントの「[Working Set](https://msdn.microsoft.com/library/cc441804.aspx)」 (ワーキング セット) を参照してください。  
  
## <a name="how-to-use-rule-data"></a>規則データの使用方法  
 規則の値を使用して、特定のプログラムの異なるバージョンやビルドを比較したり、さまざまなプロファイリング シナリオにおけるアプリケーションのパフォーマンスを確認したりします。  
  
 [エラー一覧] ウィンドウに表示されたメッセージをダブルクリックして、プロファイル データの [[マーク] ビュー](../profiling/marks-view.md)のビューに移動します。 **Process\Working Set** 列と **Memory\Pages/sec** 列を見つけます。 2 つの列を比較し、ページングの入出力アクティビティの増加に関連すると思われる特定のプログラムの実行のフェーズがあるかどうかを確認します。
