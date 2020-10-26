---
title: メモリの割り当ておよびオブジェクトの有効期間のデータ値について | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- .NET memory profiling method
- Profiling Tools, .NET memory method
ms.assetid: a22445b3-39a6-4919-8506-2b5b0ceaf77e
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 816f750148cc30de86fc116f80f64b218b4699d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145446"
---
# <a name="understanding-memory-allocation-and-object-lifetime-data-values"></a>メモリの割り当ておよびオブジェクトの有効期間のデータ値について
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールの * .NET メモリ割り当て*のプロファイル方法は、イベントが発生したときの割り当てで作成されたオブジェクトやガベージ コレクションで破棄されたオブジェクトのサイズと数に関する情報と、関数の*呼び出し履歴*に関する追加情報を収集します。 *呼び出し履歴*は、プロセッサ上で実行されている関数に関する情報を格納する動的な構造です。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  メモリ プロファイラーは、プロファイリングされたアプリケーションで .NET Framework オブジェクトの割り当てが行われるたびに、コンピューター プロセッサに対して割り込みを行います。 オブジェクトの有効期間データも収集する場合は、.NET Framework のガベージ コレクションの実行後に、毎回プロファイラーがコンピューター プロセッサに対して割り込みを行います。 データは、プロファイル対象の関数、およびオブジェクトの種類ごとに集計されます。  
  
## <a name="allocation-data"></a>割り当てデータ  
 メモリ イベントが発生すると、割り当てられたメモリ オブジェクト、または破棄されたメモリ オブジェクトの合計カウントとサイズがインクリメントされます。  
  
 メモリの割り当てイベントが発生すると、プロファイラーは呼び出し履歴の各関数のサンプル カウントをインクリメントします。 データ収集時点では、関数本体のコードを現在実行している呼び出し履歴の関数は 1 つだけです。 スタック上の他の関数は、関数呼び出し階層内の親であり、呼び出し先の関数が復帰するまで待機しています。  
  
- 割り当てイベントが発生すると、プロファイラーは命令を現在実行している関数の*排他*サンプル数をインクリメントします。 排他サンプルは、関数の合計 (*包括*) サンプル数にも含まれるため、現在アクティブな関数の包括サンプル数もインクリメントされます。  
  
- プロファイラーは、呼び出し履歴上のすべての関数の包括サンプル数をインクリメントします。  
  
## <a name="lifetime-data"></a>有効期間データ  
 .NET Framework のガベージ コレクターは、アプリケーションのメモリの割り当ておよび解放を管理します。 ガベージ コレクターのパフォーマンスを最適化するために、マネージド ヒープは 0、1、および 2 の 3 つのジェネレーションに分割されます。 ランタイムのガベージ コレクターは、新しいオブジェクトをジェネレーション 0 に格納します。 ガベージ コレクションでごみではないと判断されたオブジェクトは昇格してジェネレーション 1 とジェネレーション 2 に格納されます。  
  
 ガベージ コレクターは、オブジェクトのジェネレーション全体の割り当てを解除して、メモリを解放します。 プロファイル対象アプリケーションで作成されたオブジェクトの場合、オブジェクトの有効期間ビューにはオブジェクトの数とサイズ、および解放時のジェネレーションが表示されます。
