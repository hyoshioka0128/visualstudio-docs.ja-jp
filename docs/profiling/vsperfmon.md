---
title: VSPerfMon | Microsoft Docs
description: VSPerfMon ツールを使用して、アプリケーションのパフォーマンス データを収集する方法について学習します。 通常、このツールは VSPerfCmd.exe によって起動されます。
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSPerfMon tool
- command line, tools
- command-line tools, VSPerfMon tool
- data [Visual Studio ALM], VSPerfMon tool
- performance data, VSPerfMon tool
- performance tools, VSPerfMon tool
- profilng tools,VSPerfCmd
ms.assetid: 37052afb-7a58-441f-bb17-f1587cc57068
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 919153699299c2f39ad0353ed484a9f9c9f46846
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98719176"
---
# <a name="vsperfmon"></a>VSPerfMon
VSPerfMon ツールを使用すると、アプリケーションのパフォーマンス データを収集できます。通常、このツールは *VSPerfCmd.exe* によって起動されます。 VSPerfMon を使用した場合は、VSPerfCmd ツールでは入手できない、プロセスのアタッチやデタッチに関する追加情報を表示できます。 この情報を表示するには、VSPerfMon を別のウィンドウで起動します。 VSPerfMon を起動するには、次の構文を使用します。

```cmd
VSPerfMon [/U] </TRACE [/COUNTER:cfg] | /SAMPLE | /COVERAGE> /CROSSSESSION /OUTPUT <file name> [/WINCOUNTER:cfg] [/USER [DOMAIN\]username]
```

 VSPerfMon ツールのオプションの説明を次の表に示します。

|Options|説明|
|-------------|-----------------|
|**U**|リダイレクトされたコンソール出力は Unicode として書き込まれます。  このオプションは、最初に指定する必要があります。|
|**OUTPUT:** `<` *ファイル名* `>`|指定したファイル名に出力をリダイレクトします。|
|**TRACE**|インストルメンテーション プロファイル用のパフォーマンス モニターを開始します。|
|**SAMPLE**|サンプリング プロファイル用のパフォーマンス モニターを開始します。|
|**COVERAGE**|コード カバレッジ コレクション用のパフォーマンス モニターを開始します。|
|**CONCURRENCY**|リソース競合プロファイル用のパフォーマンス モニターを開始します。|
|**USER:** `[` *ドメイン* `\]` *ユーザー名*|指定したアカウントからパフォーマンス モニターへのクライアント アクセスを許可します。|
|**CROSSSESSION**|セッション間プロファイルを有効にします。|
|**COUNTER** `:cfg`|インストルメンテーション (TRACE) プロファイル方法を使用するときに、各インストルメンテーション ポイントで収集する CPU カウンターを指定します。 複数の COUNTER オプションを指定すると、複数のカウンター データを収集できます。<br /><br /> カウンター (*cfg*) データを指定するには、次の構文を使用します。<br /><br /> **CounterName** [**,Reload**[,**FriendlyName**]]<br /><br /> -   **CounterName** は、VSPerfCmd /QueryCounters コマンドによって返されるカウンターの名前です。<br />-   **Reload** は、カウンター イベントのサンプリング間隔です。 インストルメンテーション メソッドで *Reload* を使用しないでください。<br />-   指定すると、プロファイル ツールのレポートの列名が **CounterName** から **FriendlyName** に置き換えられます。|
|**WINCOUNTER** `:path`|マーク データと共に含める Windows パフォーマンス カウンターを指定します。 `path` は、PDH カウンター パス形式の Windows パフォーマンス カウンター文字列です。 次に例を示します。<br /><br /> \Processor(0)\\% Processor Time<br /><br /> \System\Context Switches/sec|
|**AUTOMARK** `:n`|/WINCOUNTER を使用する際の自動的なマーク間の時間間隔 (ミリ秒単位) を指定します。 値は、500 ミリ秒単位で切り上げられます。<br /><br /> 0 を使用すると、自動的なマークは無効になります。 (指定しない場合、既定の 500 ミリ秒になります)|

## <a name="see-also"></a>関連項目
- [VSInstr](../profiling/vsinstr.md)
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [VSPerfReport](../profiling/vsperfreport.md)
- [パフォーマンス レポートのビュー](../profiling/performance-report-views.md)
