---
title: コマンド ラインからレポートをフィルター処理する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 6e9b140f-b44f-4a5c-bd65-d868ddc94023
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1b6408975e8a3d7189db26913f3de75ad1c7c595
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851139"
---
# <a name="how-to-filter-reports-from-the-command-line"></a>方法: コマンド ラインからレポートをフィルター処理する
**VSPerfReport** コマンドのオプションを利用すると、レポートをフィルター処理し、プロファイリング データ ファイルの特定の時間区分に絞り込むか、1 つ以上のプロセスまたはスレッドに絞り込むことができます。 このコマンドの詳細については、「[VSPerfReport](../profiling/vsperfreport.md)」を参照してください。

|オプション|説明|
|-------------|-----------------|
|**StartTime:** [*Value*]|ミリ秒単位の時間 (value) よりも後に収集されたデータのみを表示します。|
|**EndTime:** [*Value*]|ミリ秒単位の時間 (value) よりも前に収集されたデータのみを表示します。|
|**FilterFile:** `VSPFFile`|Visual Studio の **[パフォーマンス レポート]** ウィンドウから生成されたフィルター ファイルの場所を指定します。|
|**MsFilter:** [*StartTime,Duration*]|開始時刻 (`StartTime`) からミリ秒単位の時間 (`Duration`) 内のみのデータを表示します。|
|**Process:** [*Pid*]|指定されたプロセスのデータのみを表示します。|
|**Thread:** [*ThreadID*]|指定されたスレッドのデータのみを表示します。|
|**Thread:** [*ThreadID,ProcessID*]|指定されたプロセスに関連付けられている指定されたスレッドのデータのみを表示します。|
