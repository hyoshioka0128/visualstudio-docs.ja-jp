---
title: Events (VSPerfCmd) | Microsoft Docs
description: VSPerfCmd.exe コマンドライン ツールの Events オプションを使用して、Event Trace for Windows (ETW) のログを制御します。 構文パラメーターを確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: eb139327-4783-4f2a-874c-efad377a7be4
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1ec92cae275d9f73f24f983905bc0013950e9d37
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899566"
---
# <a name="events-vsperfcmd"></a>Events (VSPerfCmd)
*VSPerfCmd.exe* **Events** オプションは、Windows イベント トレーシング (ETW) のログ記録を制御します。 ETW データは、プロファイラー データ ファイルとは別の .etl ファイルに保存されます。 このデータは、[VSPerfReport](../profiling/vsperfreport.md) /summary:etw コマンドを利用し、レポートで表示できます。

 **Events** オプションは、VSPerfCmd **Shutdown** コマンドが呼び出され、プロファイリングを停止する前にいつでも呼び出すことができます。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /events {On|Off} {Guid|ProviderName} [,Flags[,Level]
```

#### <a name="parameters"></a>パラメーター
 **On**&#124;**Off** イベント データの収集を開始または停止します。

 `Guid` プロバイダー コントロールの GUID。

 `ProviderName` Windows Management Instrumentation (WMI) に登録されているプロバイダーの名前。

 `Flags` イベント プロバイダーによって定義され、先頭に "0x" が付く 16 進数のフラグ値。

 `Level` 収集されるデータの量を指定します。 `Level` はイベント プロバイダーによって定義されます。

 **Events** オプションは、プロバイダー名として次のカーネル キーワードを理解します。

 **Process** プロセス イベント

 **Thread** スレッド イベント

 **Image** イメージのロードとアンロード イベント

 **Disk** ディスク I/O イベント

 **File** ファイル I/O イベント

 **Hardfault** ハード ページ フォールト

 **Pagefault** ソフト ページ フォールト

 **Network** ネットワーク イベント

 **Registry** レジストリ アクセス イベント

 カーネル プロバイダーのみを有効にできます。 モニターがシャットダウンするまで、無効にできません。そのフラグを変更することもできません。

## <a name="remarks"></a>解説

> [!NOTE]
> CLR ETW イベントが有効になっていると、追加のスタートアップ データがトレース ビュー レポートでも集められます。 スタートアップ イベントがレポートに表示されないようにするには、次のコマンドを使用します。

```cmd
C:\<path>VSPerfCmd -events on, \".NET Common Language Runtime\", 0x7fffffff, 5
```

> [!IMPORTANT]
> スタートアップ イベントを除外しない場合、スタートアップ イベントはマネージド オブジェクト フォーマット (MOF) ファイルに一覧表示されないため、レポートに GUID として表示されます。 詳細については、Microsoft Web サイトの「[MOF (Managed Object Format) ファイルのサンプル](https://msdn.microsoft.com/library/default.aspx)」を参照してください。

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
