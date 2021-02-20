---
title: ThreadOn と ThreadOff | Microsoft Docs
description: どのようにすれば、インストルメンテーション メソッドを使用するコマンド ライン プロファイリング セッションでのみ VSPerfCmd.exe の ThreadOff および ThreadOn サブコマンドが使用できるようになるかについて学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5cd5a695-0a14-484a-8952-ed47e13d8e92
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 059e7dfc9d7c16be3aa699eea47b1a64882e689e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949312"
---
# <a name="threadon-and-threadoff"></a>ThreadOn と ThreadOff
*VSPerfCmd.exe の* **ThreadOff** および **ThreadOn** サブコマンドは、インストルメンテーション メソッドを使用するコマンド ライン プロファイリング セッションでのみ使用できます。 **ThreadOff** および **ThreadOn** は、指定されたスレッドのプロファイリングを一時停止および再開します。 **ThreadOff** がスレッドのプロファイリングを停止し、**ThreadOn** がスレッドのプロファイリングを開始します。

 多くの場合、**ThreadOn** または **ThreadOff** を *VSPerfCmd.exe* コマンド ラインの唯一のオプションとして指定しますが、**GlobalOn**、**GlobalOff**、**ProcessOn**、**ProcessOff** の各サブコマンドと組み合わせて使用することもできます。

 **ThreadOn** サブコマンドと **ThreadOff** サブコマンドは、コマンド ライン プロファイリング セッションのすべてのプロセスについてのデータ収集を制御する **GlobalOn** サブコマンドと **GlobalOff** サブコマンド、および指定されたプロセスについてのデータ収集を制御する **ProcessOn** サブコマンドと **ProcessOff** サブコマンドと対話します。

 **ThreadOff** サブコマンドおよび **ThreadOn** サブコマンドは、プロファイラー API 関数によって操作されるスレッドの開始/停止数にも影響します。

- **ThreadOff** は、スレッドの開始/停止数を直ちに 0 に設定して、プロファイリングを一時停止します。

- **ThreadOn** は、スレッドの開始/停止数を直ちに 1 に設定して、プロファイリングを再開します。

  詳細については、「[プロファイル ツールの API](../profiling/profiling-tools-apis.md)」 を参照してください。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /{ThreadOff|ThreadOn}:TID [Options]

```

#### <a name="parameters"></a>パラメーター
 `TID` 開始または停止するスレッドの整数の ID。

## <a name="valid-options"></a>有効なオプション
 **ThreadOn** と **ThreadOff** は、次のサブコマンドも含むコマンド ラインで指定できます。

 **Start:** `Method` コマンド ライン プロファイル セッションを初期化し、指定されたプロファイル方法を設定します。

 **GlobalOff**&#124;**GlobalOn** コマンド ライン プロファイル セッションのすべてのプロセスのプロファイリングを停止または開始します。

 {**ProcessOff**&#124;**ProcessOn**} **:** `TID`指定されたプロセスのプロファイリングを停止または開始します。

## <a name="example"></a>例
 この例では、アプリケーションのスタートアップ データのみが収集されるように、**ThreadOff** サブコマンドを使用してプロファイル データの収集を停止します。

```cmd
; Initialize the profiler.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp
; Start the instrumented application.
; Stop profiling the thread after startup.
VSPerfCmd.exe /ThreadOff:12345
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
