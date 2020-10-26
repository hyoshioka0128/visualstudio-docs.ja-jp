---
title: 'DA0505: プロセスに割り当てられた平均プライベート バイト数がプロファイリングされています | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0505
- vs.performance.rules.DA0505
- vs.performance.505
ms.assetid: 32c612ea-d077-44ba-8e6f-3a96333bad00
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 69a7eaeecd65ffdfbd575b59fbea15c476d0fbeb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75850864"
---
# <a name="da0505-average-private-bytes-allocated-for-the-process-being-profiled"></a>DA0505: プロセスに割り当てられた平均プライベート バイト数がプロファイリングされています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0505 |  
|Category |リソース管理 |  
|プロファイル方法 |All |  
|Message |この情報は情報収集のみを対象としています。 Process Private Bytes カウンターは、プロファイリングを行っているプロセスによって割り当てられた仮想メモリを測定します。 報告される値は、全測定期間を通じて計算された平均値です。|  
|ルールの種類 |情報 |  
  
 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。  
  
## <a name="rule-description"></a>ルールの説明  
 このメッセージにより、プロセスによって割り当てられた現在の仮想メモリ容量がバイト単位で報告されます (プライベート バイト)。 プライベート バイトは、プロセス内部で実行中のスレッドからのみアクセスできるプロセスによって割り当てられた仮想メモリの位置を表します。  
  
 32 ビット コンピューター上で実行されている 32 ビット プロセスの場合、プロセスのアドレス空間のプライベート領域の上限は 2 GB です。 [/3GB](https://msdn.microsoft.com/library/ff556232.aspx) Boot.ini スイッチを使用して、32 ビット プロセスは、最大 3 GB の仮想メモリを取得できます。 64 ビット コンピューター上で実行されている 32 ビット プロセスの場合、最大 4 GB のプライベート仮想メモリを取得できます。  
  
 64 ビット コンピューター上で実行されている 64 ビット プロセスの場合、最大 8 TB のプライベート仮想メモリを取得できます。  
  
 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値の平均値が、このメッセージによって報告されます。  
  
 プロセス アドレス空間の詳細については、Windows のメモリ管理のドキュメントの「[Virtual Address Space](https://msdn.microsoft.com/library/aa366912.aspx)」 (仮想アドレス空間) を参照してください。  
  
## <a name="how-to-use-rule-data"></a>規則データの使用方法  
 報告された値を使用して、特定のプログラムの異なるバージョンやビルドを比較したり、さまざまなプロファイリング シナリオにおけるアプリケーションのパフォーマンスを確認したりします。
