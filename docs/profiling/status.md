---
title: Status | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ba656fa4-ef9d-4d8c-a3b6-739c3b5d23ae
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: bf5e0fdf478e067f61b1d0e259cb1624380e4f02
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778246"
---
# <a name="status"></a>Status
*VSPerfCmd.exe* の **Status** オプションでは、プロファイラーの状態、および現在プロファイルを実行中の任意のプロセスに関する情報が表示されます。

 コマンド ラインで指定するオプションは **Status** オプションのみにする必要があります。 状態を表示するには、*VSPerfCmd.exe* の **Start** オプションを使用してプロファイラーを初期化しておく必要があります。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Status
```

#### <a name="parameters"></a>パラメーター
 なし

## <a name="remarks"></a>解説
 **Status** オプションでは、プロファイラーに関して、次の状態情報を表示します。

 **出力ファイル名**現在のプロファイラー データ ファイルのパスとファイル名。

 **コレクション モード** SAMPLE または TRACE

 **最大プロセス** 同時にプロファイルできる最大プロセス数と、現在アクティブなプロセス数。

 **最大スレッド** 同時にプロファイルできる最大スレッド数。

 **バッファー数** プロファイル データの書き込み専用のメモリ バッファー数。

 **バッファー サイズ** メモリ バッファーのサイズ (バイト単位)。

 **Status** オプションでは、現在プロファイルされている各プロセスに関して、次の状態情報を表示します。

 **Process** プロファイルされているプロセスの名前。

 **プロセス ID** プロセスのシステム ID。

 **Num スレッド** 現在実行中のスレッド数。

 **開始/停止数** このプロセスに対するデータ収集を制御するプライマリ内部プロファイラー カウント。 データを収集するには、このカウントが 1 である必要があります。 開始/停止数は、プロファイラー API、および VSPerfCmd オプションである **GlobalOn**、**GlobalOff**、**ProcessOn**、**ProcessOff**、**ThreadOn**、および **ThreadOff** によって操作できます。

 **保留/再開数** このプロセスに対するデータ収集を制御するセカンダリ内部プロファイラー カウント。 データを収集するには、このカウントが 0 以下である必要があります。 **保留/再開**数は、プロファイラー API によってのみ操作できます。

 **監視するアクセス権を伴うユーザー** プロファイラーにアクセスできるユーザーの名前を一覧表示します。 VSPerfCmd.exe の **Admin** オプションを使用して、追加ユーザーにアクセスを許可できます。

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
