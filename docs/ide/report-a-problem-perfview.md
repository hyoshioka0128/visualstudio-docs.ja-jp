---
description: PerfView は、Windows イベント トレーシングに基づいて ETL (イベント トレース ログ) ファイルを作成するツールです。これは Visual Studio に関する一部の問題のトラブルシューティングを行うのに役立ちます。
title: PerfView で ETL トレースを収集する
ms.date: 09/27/2019
ms.topic: how-to
helpviewer_keywords:
- perfview
- ETL Trace
author: corob-msft
ms.author: corob
manager: jmartens
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Use perfview.exe to collect ETL traces for troubleshooting issues with Visual Studio
ms.openlocfilehash: 81cf6469a14fb3559d37056ba5193d9018ccc1c8
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221068"
---
# <a name="collect-an-etl-trace-with-perfview"></a>PerfView で ETL トレースを収集する

PerfView は、[Windows イベント トレーシング](/windows/desktop/ETW/event-tracing-portal)に基づいて ETL (イベント トレース ログ) ファイルを作成するツールです。これは Visual Studio に関する一部の問題をトラブルシューティングするのに役立ちます。 お客様が問題を報告したときに、製品チームから、PerfView を実行して追加情報を収集していただくようお願いする場合があります。

## <a name="install-perfview"></a>PerfView のインストール

[GitHub](https://github.com/Microsoft/perfview/blob/master/documentation/Downloading.md) から PerfView をダウンロードします。

## <a name="run-perfview"></a>PerfView の実行

1. Windows エクスプローラーで **PerfView.exe** を右クリックし、管理者として **[管理者として実行]** を選択します
1. [収集] メニューで、**[収集]** を選択します
1. **[Zip]**、**[結合]**、**[ThreadTime]** をチェックします。
1. **[Circular MB]\(循環 MB\)** を 1000 に増やします。
1. **[Current Dir]\(現在のディレクトリ\)** を変更し、指定したフォルダーに ETL トレースを保存します。2 回以上収集する場合は、[データ ファイル] も変更します。
1. データの記録を開始するには、**[収集の開始]** ボタンを選択します。
1. データの記録を停止するには、**[収集の停止]** ボタンを選択します。 PrefView.etl.zip ファイルが指定したディレクトリに保存されます。

PerfView を使って保存できるのは、そのバッファーに収まる最新のデータのみです。 そのため、Visual Studio がフリーズしたり、速度が低下したりしたら、できるだけ早く収集を停止するようにしてください。 問題が発生した後 30 秒以上収集を行わないようにしてください。

詳細については、[Channel9 のPerfView チュートリアル](https://channel9.msdn.com/Series/PerfView-Tutorial/PerfView-Tutorial-1-Collecting-data-with-the-Run-command)に関するページをご覧ください。
