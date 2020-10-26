---
title: '方法: 行レベルのサンプリング データを収集する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, line-level sampling
ms.assetid: 44803aad-dd39-4c2e-9209-d35185d44983
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 65890bf31a1257c3a41bc1fd7ed3f732c50eda14
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185956"
---
# <a name="how-to-collect-line-level-sampling-data"></a>方法 : 行レベルのサンプリング データを収集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

行レベルのサンプリングとは、排他サンプル数が高い関数など、プロセッサ集中型の関数のコードで、プロセッサが大部分の時間を費やす必要のある場所を特定するためのプロファイラーの機能です。  
  
## <a name="overview"></a>概要  
 行レベルのサンプリングでは、設定された間隔でプログラムのコール スタックを走査し、その結果を集計します。 これらの結果では、サンプルの取得時にプロセッサが実行していた命令が示されます。 次に、排他サンプルについて収集されたデータが分析され、コード行と命令ポインター (IP) を識別します。  
  
 行レベルのサンプリングは、ネイティブ コードだけでなく、マネージド コードにも使用できます。 このデータが表示されるパフォーマンス レポートには、行ビューおよびモジュール ビューがあります。  
  
 文字の開始または終了情報は、ネイティブ コードでは使用できません。 複数行ステートメントの場合、ネイティブ コードでは、行の開始情報を使用できず、行の終了情報だけを使用できます。  
  
### <a name="available-data"></a>使用できるデータ  
 使用できる行レベルのサンプリング データには次の情報が含まれます。  
  
- 関数名。  
  
- 関数アドレス。  
  
- 行の開始情報 - サンプリングされるコードの行番号。  
  
- 行の終了情報 - ソースの終了行番号。 これは "行の開始情報" のデータと同じです (1 つのプログラム文が複数のソース コード行にまたがっている場合を除く)。  
  
- 文字の開始情報 - 集約サンプルの開始列。 通常、これは 0 です (1 つの行に複数のプログラム文が含まれる場合を除く)。  
  
- 文字の終了情報 - 集約サンプルの終了列。  
  
- IP - 集約サンプルが取得されたアドレス (IP ビューのみ)。  
  
  **[モジュール]** ビューでは、関数に行レベルの統計が含まれている場合、統計は各関数の下に入れ子になっています。 さらに、各行で入れ子になっている IP レベルの統計が表示されます。  
  
### <a name="turn-off-line-level-sampling-for-managed-code"></a>マネージド コードの行レベルのサンプリングの無効化  
 既定では、行レベルのサンプリングは有効になっています。 マネージド コードの行レベルのデータ収集を無効にするには、次のいずれかを実行します。  
  
- プロファイリングの前に、「**VSPerfCLREnv /samplelineoff**」と入力します。 これは、アプリケーションとサービスの両方に影響します。  
  
     または  
  
- アプリケーションの起動時に、「**VSPerfCmd /lineoff \<other arguments>** 」を入力します。  
  
## <a name="see-also"></a>参照  
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)   
 [パフォーマンス ツール データを分析する](../profiling/analyzing-performance-tools-data.md)
