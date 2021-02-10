---
title: ProcessOn と ProcessOff | Microsoft Docs
description: VSPerfCmd.exe の ProcessOff サブコマンドと ProcessOn サブコマンドでは、コマンド ライン プロファイル セッションの指定されたプロセスのプロファイリングを一時停止および再開する方法について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d3dc6a7e-bc0f-48a6-a4ec-f386348bb296
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 82a976700137255a5c6adb074058b33b15fb7c5f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910690"
---
# <a name="processon-and-processoff"></a>ProcessOn と ProcessOff
VSPerfCmd.exe の **ProcessOff** サブコマンドと **ProcessOn** サブコマンドでは、コマンド ライン プロファイル セッションの指定されたプロセスのプロファイリングを一時停止および再開します。 **ProcessOff** がプロセスのプロファイリングを停止し、**ProcessOn** がプロセスのプロファイリングを開始します。

 多くの場合、**ProcessOn** または **ProcessOff** を VSPerfCmd.exe コマンド ラインの唯一のオプションとして指定しますが、これらを **GlobalOn**、**GlobalOff**、**ThreadOn**、および **ThreadOff** の各サブコマンドと組み合わせて使用することもできます。

 **ProcessOn** サブコマンドと **ProcessOff** サブコマンドは、コマンド ライン プロファイル セッションのすべてのプロセスについてのデータ収集を制御する **GlobalOn** サブコマンドと **GlobalOff** サブコマンド、および指定されたスレッドについてのデータ収集を制御する **ThreadOn** サブコマンドと **ThreadOff** サブコマンドと対話します。

 **ProcessOff** サブコマンドと **ProcessOn** サブコマンドは、プロファイラー API 関数によって操作されるプロセスの開始/停止数にも影響します。

- **ProcessOff** は、プロセスの開始/停止数を直ちに 0 に設定して、プロファイリングを一時停止します。

- **ProcessOn** は、プロセスの開始/停止数を直ちに 1 に設定して、プロファイリングを再開します。

  詳細については、[「プロファイリング ツールの API」](../profiling/profiling-tools-apis.md) を参照してください。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /{ProcessOff|ProcessOn}:PID [Options]

```

#### <a name="parameters"></a>パラメーター
 `PID` 開始または停止するプロセスの整数の ID。 プロセス ID は、Windows タスク マネージャーの **[プロセス]** タブにリストされます。

## <a name="required-subcommands"></a>必須のサブコマンド
 なし

## <a name="valid-subcommands"></a>有効なサブコマンド
 **ProcessOn** と **ProcessOff** は、次のサブコマンドも含むコマンド ラインで指定できます。

 **Start:** `Method` コマンド ライン プロファイル セッションを初期化し、指定されたプロファイル方法を設定します。

 **Launch:** `AppName` 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。

 **Attach:** `PID` 指定されたプロセスのプロファイリングを開始します。

 **GlobalOff**&#124;**GlobalOn** コマンド ライン プロファイル セッションのすべてのプロセスのプロファイリングを停止または開始します。

 {**ThreadOff**&#124;**ThreadOn**} **:** `TID`指定されたスレッドのプロファイリングを停止または開始します (インストルメンテーション メソッドのみ)。

## <a name="example"></a>例
 この例では、**ProcessOff** サブコマンドを使用してアプリケーション起動のプロファイル データを収集します。

```cmd
; Initialize the profiler.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp
; Start the instrumented application.
; Stop profiling the process after startup.
VSPerfCmd.exe /ProcessOff:12345
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
