---
title: Sys (VSPerfCmd) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 294a6f9e-b49f-4c83-b322-5ac5411b66fb
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 981b37fe1ebaad5e45f0308143ab0384ef1d559b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145605"
---
# <a name="sys-vsperfcmd"></a>Sys (VSPerfCmd)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe の **Sys** オプションは、システム呼び出しイベント (プロファイリングされたアプリケーションからオペレーティング システムへの関数呼び出し) にサンプリングされるプロファイリング イベントを設定し、必要に応じて、サンプリング間隔のシステム呼び出し数を既定値の 10 から変更します。  
  
 **Sys** は、**Launch** オプションまたは **Attach** オプションも含むコマンド ラインでのみ使用できます。  
  
 既定では、プロファイラーのサンプリング イベントは、プロセッサのクロック サイクルに設定され、サンプリング間隔は 10,000,000 に設定されます。 **Timer**、**PF**、**Sys**、**Counter** の各オプションを使用すると、サンプリング イベントおよびサンプリング間隔を設定できます。 **GC** オプションは、割り当ておよびガベージ コレクション イベントが発生するたびに、.NET メモリ データを収集します。 コマンド ラインには、上記のオプションのいずれか 1 つだけを指定できます。  
  
 サンプリング イベントおよびサンプリング間隔は、**Launch** オプションまたは **Attach** オプションを含む最初のコマンド ラインでのみ設定できます。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe {/Launch:AppName|Attach:PID} /Sys[:Events] [Options]  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Events`  
 サンプリング間隔におけるシステム呼び出しイベント数を指定する整数値。 ‎`Events` が指定されていない場合、間隔は 10 に設定されます。  
  
## <a name="required-options"></a>必須オプション  
 **Sys** には、次のオプションのいずれかが必要です。  
  
 **起動:**`AppName`  
 プロファイラーと、`AppName` で指定されたアプリケーションを起動します。  
  
 **アタッチ:**`PID`  
 プロファイラーを `PID` で指定されたプロセスにアタッチします。  
  
## <a name="invalid-options"></a>無効なオプション  
 以下のオプションは、**Sys** と同じコマンド ラインには指定できません。  
  
 **PF**[**:** `Events` ]  
 サンプリング イベントをページ フォールトに設定します。オプションで、サンプリング間隔を `Events` に設定します。 既定の PF 間隔は 10 です。  
  
 **タイマー**[**:** `Cycles` ]  
 サンプリング イベントをプロセッサのクロック サイクルに設定し、必要に応じてサンプリング間隔を `Cycles` に設定します。 既定の Timer 間隔は 10,000,000 です。  
  
 **カウンター:** `Name`[`,Reload`[`,FriendlyName`]]  
 サンプリング イベントを、`Name` で指定された CPU パフォーマンス カウンターに設定し、サプリング間隔を `Reload` に設定します。  
  
 **GC**[**:**{**Allocation**&#124;**Lifetime**}]  
 .NET メモリ データを収集します。 既定 (**割り当て**) では、すべてのメモリ割り当てイベントでデータが収集されます。 **Lifetime**パラメーターを指定すると、ガベージコレクションイベントごとにデータも収集されます。  
  
## <a name="example"></a>例  
 この例では、プロファイラーのサンプリング イベントをシステム呼び出しに設定し、サンプリング間隔をサンプルごとに 20 の呼び出しに設定する方法を示します。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Sys:20  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
