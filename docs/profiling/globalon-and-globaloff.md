---
title: GlobalOn と GlobalOff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 24b0ed68-d19e-473e-9af3-252c11d82bcf
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 518f41557809cdeaaae9f9e1ac79e3797a854395
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74776967"
---
# <a name="globalon-and-globaloff"></a>GlobalOn と GlobalOff
*VSPerfCmd.exe* の **GlobalOff** オプションと **GlobalOn** オプションは、コマンド ライン プロファイル セッションのすべてのプロセスとスレッドのプロファイリングを一時停止および再開するために使用されます。

 **GlobalOn** および **GlobalOff** は、*VSPerfCmd.exe* コマンド ラインの唯一のオプションとして指定することも、**Start** オプション、**Launch** オプション、または **Attach** オプションを含んでいるコマンド ラインに含めることもできます。

 **GlobalOn** と **GlobalOff** は、**ProcessOn**、**ProcessOff**、**ThreadOn**、**ThreadOff** の各オプションと組み合わせて使用することもできます。

 **GlobalOn** オプションと **GlobalOff** オプションは、指定したプロセスのデータ収集を制御する **ProcessOn** オプションおよび **ProcessOff** オプション、指定したスレッドのデータ収集を制御する **ThreadOn** オプションおよび **ThreadOff** オプションと対話します。

 **GlobalOff** オプションと **GlobalOn** オプションは、プロファイラーの API 関数によって操作されるグローバルな開始/停止数にも影響します。

- **GlobalOff** は、グローバルな開始/停止数を直ちに 0 に設定して、プロファイリングを一時停止します。

- **GlobalOn** は、グローバルな開始/停止数を直ちに 1 に設定して、プロファイリングを再開します。

  詳細については、「[プロファイル ツールの API](../profiling/profiling-tools-apis.md)」 を参照してください。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /{GlobalOff|GlobalOn}

VSPerfCmd.exe /Start:Method /{GlobalOff|GlobalOn} [Options]

VSPerfCmd.exe {Launch:AppName|Attach:PID} /{GlobalOff|GlobalOn}[Options]
```

#### <a name="parameters"></a>パラメーター
 None

## <a name="valid-options"></a>有効なオプション
 **GlobalOn** と **GlobalOff** は、次のオプションを含んでいるコマンド ラインで指定できます。

 **Start:** `Method` コマンド ライン プロファイラー セッションを初期化し、指定されたプロファイル方法を設定します。

 **Launch:** `AppName` 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。

 **Attach:** `PID` 指定されたプロセスのプロファイリングを開始します。

 {**ProcessOff**&#124;**ProcessOn**} **:** `PID`指定されたプロセスのプロファイリングを停止または開始します。

 {**ThreadOff**&#124;**ThreadOn**} **:** `TID`指定されたプロセスのプロファイリングを停止または開始します (インストルメンテーション メソッドのみ)。

## <a name="example"></a>例
 次の例では、アプリケーションの起動およびシャットダウンのプロファイル データを収集しないようにするために、**GlobalOff** オプションと **GlobalOn** オプションを使用しています。

```cmd
; Initialize the profiler with profiling stopped.
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp /GlobalOff
; Start an instrumented application and wait for it to warm up.
; Start profiling.
VSPerfCmd.exe /GlobalOn
; Exercise the application functionality that you want to profile.
; Stop profiling.
VSPerfCmd.exe /GlobalOff
; Shut down the target application.
; Close the profiler.
VSPerfCmd /Shutdown

```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
