---
title: VSPerfMon | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- VSPerfMon tool
- command line, tools
- command-line tools, VSPerfMon tool
- data [Visual Studio ALM], VSPerfMon tool
- performance data, VSPerfMon tool
- performance tools, VSPerfMon tool
- profilng tools,VSPerfCmd
ms.assetid: 37052afb-7a58-441f-bb17-f1587cc57068
caps.latest.revision: 35
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4a06a6632d62f853eef33cad00ad766e0d1aab87
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184013"
---
# <a name="vsperfmon"></a>VSPerfMon
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfMon ツールを使用すると、アプリケーションのパフォーマンス データを収集できます。通常、このツールは VSPerfCmd.exe によって起動されます。 VSPerfMon を使用した場合は、VSPerfCmd ツールでは入手できない、プロセスのアタッチやデタッチに関する追加情報を表示できます。 この情報を表示するには、VSPerfMon を別のウィンドウで起動します。 VSPerfMon を起動するには、次の構文を使用します。  
  
```  
VSPerfMon [/U] </TRACE [/COUNTER:cfg] | /SAMPLE | /COVERAGE> /CROSSSESSION /OUTPUT <file name> [/WINCOUNTER:cfg] [/USER [DOMAIN\]username]  
```  
  
 VSPerfMon ツールのオプションの説明を次の表に示します。  
  
|オプション|説明|  
|-------------|-----------------|  
|**U**|リダイレクトされたコンソール出力は Unicode として書き込まれます。  このオプションは、最初に指定する必要があります。|  
|**OUTPUT:** `<` *file name* `>`|指定したファイル名に出力をリダイレクトします。|  
|**TRACE**|インストルメンテーション プロファイル用のパフォーマンス モニターを開始します。|  
|**SAMPLE**|サンプリング プロファイル用のパフォーマンス モニターを開始します。|  
|**COVERAGE**|コード カバレッジ コレクション用のパフォーマンス モニターを開始します。|  
|**CONCURRENCY**|リソース競合プロファイル用のパフォーマンス モニターを開始します。|  
|**USER:** `[` *domain* `\]` *username*|指定したアカウントからパフォーマンス モニターへのクライアント アクセスを許可します。|  
|**CROSSSESSION**|セッション間プロファイルを有効にします。|  
|**COUNTER** `:cfg`|インストルメンテーション (TRACE) プロファイル方法を使用するときに、各インストルメンテーション ポイントで収集する CPU カウンターを指定します。 複数の COUNTER オプションを指定すると、複数のカウンター データを収集できます。<br /><br /> カウンター (*cfg*) データを指定するには、次の構文を使用します。<br /><br /> **CounterName** [ **,Reload**[,**FriendlyName**]]<br /><br /> -   **CounterName** は、VSPerfCmd /QueryCounters コマンドによって返されるカウンターの名前です。<br />-   **Reload** は、カウンター イベントのサンプリング間隔です。 インストルメンテーション メソッドで *Reload* を使用しないでください。<br />-   指定すると、プロファイル ツールのレポートの列名が **CounterName** から **FriendlyName** に置き換えられます。|  
|**WINCOUNTER** `:path`|マーク データと共に含める Windows パフォーマンス カウンターを指定します。 `path` は、PDH カウンター パス形式の Windows パフォーマンス カウンター文字列です。 次に例を示します。<br /><br /> \Processor(0)\\% Processor Time<br /><br /> \System\Context Switches/sec|  
|**AUTOMARK** `:n`|/WINCOUNTER を使用する際の自動的なマーク間の時間間隔 (ミリ秒単位) を指定します。 値は、500 ミリ秒単位で切り上げられます。<br /><br /> 0 を使用すると、自動的なマークは無効になります。 (指定しない場合、既定の 500 ミリ秒になります)|  
  
## <a name="see-also"></a>参照  
 [VSInstr](../profiling/vsinstr.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [VSPerfReport](../profiling/vsperfreport.md)   
 [パフォーマンスレポートのビュー](../profiling/performance-report-views.md)
