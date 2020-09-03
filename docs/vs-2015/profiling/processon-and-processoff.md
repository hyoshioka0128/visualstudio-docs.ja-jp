---
title: ProcessOn と ProcessOff | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: d3dc6a7e-bc0f-48a6-a4ec-f386348bb296
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 77e21a280700520b6861dd42e01a4aefa4faa704
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180204"
---
# <a name="processon-and-processoff"></a>ProcessOn と ProcessOff
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe の **ProcessOff** サブコマンドと **ProcessOn** サブコマンドでは、コマンド ライン プロファイル セッションの指定されたプロセスのプロファイリングを一時停止および再開します。 **ProcessOff** がプロセスのプロファイリングを停止し、**ProcessOn** がプロセスのプロファイリングを開始します。  
  
 多くの場合、**ProcessOn** または **ProcessOff** を VSPerfCmd.exe コマンド ラインの唯一のオプションとして指定しますが、これらを **GlobalOn**、**GlobalOff**、**ThreadOn**、および **ThreadOff** の各サブコマンドと組み合わせて使用することもできます。  
  
 **ProcessOn** サブコマンドと **ProcessOff** サブコマンドは、コマンド ライン プロファイル セッションのすべてのプロセスについてのデータ収集を制御する **GlobalOn** サブコマンドと **GlobalOff** サブコマンド、および指定されたスレッドについてのデータ収集を制御する **ThreadOn** サブコマンドと **ThreadOff** サブコマンドと対話します。  
  
 **ProcessOff** サブコマンドと **ProcessOn** サブコマンドは、プロファイラー API 関数によって操作されるプロセスの開始/停止数にも影響します。  
  
- **ProcessOff** は、プロセスの開始/停止数を直ちに 0 に設定して、プロファイリングを一時停止します。  
  
- **ProcessOn** は、プロセスの開始/停止数を直ちに 1 に設定して、プロファイリングを再開します。  
  
  詳細については、[「プロファイリング ツールの API」](../profiling/profiling-tools-apis.md) を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /{ProcessOff|ProcessOn}:PID [Options]  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 `PID`  
 開始または停止するプロセスの整数の ID。 プロセス ID は、Windows タスク マネージャーの [プロセス] タブにリストされます。  
  
## <a name="required-subcommands"></a>必須のサブコマンド  
 None  
  
## <a name="valid-subcommands"></a>有効なサブコマンド  
 **ProcessOn** と **ProcessOff** は、次のサブコマンドも含むコマンド ラインで指定できます。  
  
 **開始:**`Method`  
 コマンド ライン プロファイル セッションを初期化し、指定されたプロファイル方法を設定します。  
  
 **起動:**`AppName`  
 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。  
  
 **アタッチ:**`PID`  
 指定されたプロセスのプロファイリングを開始します。  
  
 **GlobalOff**&#124;**GlobalOn**  
 コマンド ライン プロファイル セッションのすべてのプロセスのプロファイリングを停止または開始します。  
  
 {**Threadoff**&#124;**threadoff**}**:**`TID`  
 指定されたスレッドのプロファイリングを停止または開始します (インストルメンテーション メソッドのみ)。  
  
## <a name="example"></a>例  
 この例では、**ProcessOff** サブコマンドを使用してアプリケーション起動のプロファイル データを収集します。  
  
```  
; Initialize the profiler.  
VSPerfCmd.exe /Start:Trace /Output:Instrument.vsp   
; Start the instrumented application.  
; Stop profiling the process after startup.  
VSPerfCmd.exe /ProcessOff:12345  
; Shut down the target application.  
; Close the profiler.  
VSPerfCmd /Shutdown  
  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
