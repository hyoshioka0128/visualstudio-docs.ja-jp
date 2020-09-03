---
title: マルチスレッド アプリケーションのデバッグ
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.gputthreads
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], high-performance computing
- debugging [Visual Studio], multithreaded
- multithreaded debugging
- high-performance debugging
ms.assetid: 9d175bc2-1d95-4c47-9bc3-9755af968a9c
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8cb43c9a32f3dfd0a6383d466f7cd283acf0ab3a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65691279"
---
# <a name="debug-multithreaded-applications-in-visual-studio"></a>マルチスレッド アプリケーションのデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スレッドは、オペレーティング システムでプロセッサ時間を割り当てる命令のシーケンスです。 オペレーティング システムで実行されているプロセスは、いずれも 1 つ以上のスレッドで構成されます。 複数のスレッドで構成されるプロセスをマルチスレッド プロセスといいます。

 複数のプロセッサ、マルチコア プロセッサ、またはハイパースレッディング プロセッサを搭載したコンピューターでは、同時に複数のスレッドを実行できます。 複数のスレッドを同時に実行すると、プログラムのパフォーマンスは大幅に向上しますが、複数のスレッドを追跡する必要があるため、デバッグは難しくなります。

 また、マルチスレッドには新しい種類の潜在的な問題が伴います。 たとえば、複数のスレッドが同じリソースにアクセスする必要があり、一度に 1 つのスレッドだけがそのリソースに安全にアクセスできるということがよくあります。 一度に 1 つのスレッドだけがリソースにアクセスできるようにするには、相互排他を適用する必要があります。 相互排他が正しく実行されない場合は、スレッドを実行できない *デッドロック* 状態が発生する可能性があります。 デッドロックは、デバッグが特に困難な問題の 1 つです。

 Visual Studio には、[ **スレッド** ] ウィンドウ、GPU スレッドウィンドウ、並列ウォッチウィンドウ、およびマルチスレッドデバッグを容易にするその他の機能が用意されています。 スレッド機能の詳細について確認するには、チュートリアルを完了することをお勧めします。 「 [チュートリアル: マルチスレッドアプリケーションのデバッグ](../debugger/walkthrough-debugging-a-multithreaded-application.md) 」および「 [チュートリアル: C++ AMP アプリケーションのデバッグ](https://msdn.microsoft.com/library/40e92ecc-f6ba-411c-960c-b3047b854fb5)」を参照してください。

 Visual Studio には、強力なブレークポイントとトレースポイントも用意されており、マルチスレッド アプリケーションのデバッグに役立ちます。 ブレークポイント フィルターを使用すると、個々のスレッドにブレークポイントを配置できます。 「[ブレークポイントの使用」を](../debugger/using-breakpoints.md)参照

 ユーザー インターフェイスを含むマルチスレッド アプリケーションは、特にデバッグが困難になることがあります。 その場合には、アプリケーションを別のコンピューターで実行し、リモート デバッグを使用することを検討してください。 詳細については、「 [リモートデバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [スレッドとプロセスのデバッグ](../debugger/debug-threads-and-processes.md) スレッドとプロセスのデバッグの基本について説明します。

 [複数のプロセスをデバッグ](../debugger/debug-multiple-processes.md) する複数のプロセスをデバッグする方法について説明します。

 [方法: [スレッド] ウィンドウを使用](../debugger/how-to-use-the-threads-window.md) する[ **スレッド** ] ウィンドウでスレッドをデバッグするための便利な手順です。

 [方法: デバッグ中に別のスレッドに切り替える](../debugger/how-to-switch-to-another-thread-while-debugging.md) デバッグコンテキストを別のスレッドに切り替えるには、3つの方法があります。

 [方法: スレッドに対してフラグの実行とフラグの](../debugger/how-to-flag-and-unflag-threads.md) 解除を行うデバッグ中に特に注意する必要があるスレッドにマークを付けたり、フラグを設定したりします。

 [方法: ネイティブコードでスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-native-code.md) スレッドに、[ **スレッド** ] ウィンドウに表示される名前を付けます。

 [方法: マネージコードでスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-managed-code.md) スレッドに、[ **スレッド** ] ウィンドウに表示される名前を付けます。

 [チュートリアル: マルチスレッドアプリケーションのデバッグ](../debugger/walkthrough-debugging-a-multithreaded-application.md)
[!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] の方法に重点を置いてスレッドのデバッグ機能を紹介するガイド ツアーです。

 [方法: 高パフォーマンスクラスターでデバッグ](../debugger/how-to-debug-on-a-high-performance-cluster.md) する高パフォーマンスクラスターで実行されるアプリケーションをデバッグするための手法。

 [ネイティブコードでのスレッドのデバッグに関するヒント](../debugger/tips-for-debugging-threads-in-native-code.md) ネイティブスレッドのデバッグに役立つ単純な手法。

 [[タスク] ウィンドウの使用](../debugger/using-the-tasks-window.md) すべてのマネージタスクオブジェクトまたはネイティブタスクオブジェクトの状態やその他の有用な情報を含む一覧が表示されます。

 [[並列スタック] ウィンドウの使用](../debugger/using-the-parallel-stacks-window.md) 複数のスレッド (またはタスク) の呼び出し履歴を1つのビューに表示します。また、スレッド (またはタスク) 間で共通しているスタックセグメントを結合します。

 [チュートリアル: 並列アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md) [並列タスク] ウィンドウと [並列スタック] ウィンドウの使用方法を示すチュートリアルです。

 [方法: [並列ウォッチ] ウィンドウを使用](../debugger/how-to-use-the-parallel-watch-window.md) する複数のスレッド間で値と式を検査します。

 [方法: GPU スレッドウィンドウを使用](../debugger/how-to-use-the-gpu-threads-window.md) するデバッグ中に GPU 上で実行されているスレッドを調べて操作します。

## <a name="related-sections"></a>関連項目

[ブレークポイントの使用](../debugger/using-breakpoints.md)
- 個々のスレッドにブレークポイントを配置する場合にブレークポイント フィルターを使用する方法について説明します。

- トレースポイントを使用すると、プログラムの実行を中断なしでトレースできます。 この方法はデッドロックなどの問題を調べる場合に役立ちます。

  [スレッド処理](https://msdn.microsoft.com/library/7b46a7d9-c6f1-46d1-a947-ae97471bba87) プログラミングにおけるスレッドの概念 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] (コード例を含む)。

  [コンポーネントでのマルチスレッド](https://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779) コンポーネントでマルチスレッドを使用する方法 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

  [古いコードのマルチスレッドサポート (Visual C++)](https://msdn.microsoft.com/library/24425b1f-5031-4c6b-aac7-017115a40e7c) MFC を使用した C++ プログラマ向けのスレッドの概念とコード例。

## <a name="see-also"></a>参照
 [スレッドとプロセスのデバッグ](../debugger/debug-threads-and-processes.md)[リモートデバッグ](../debugger/remote-debugging.md)
