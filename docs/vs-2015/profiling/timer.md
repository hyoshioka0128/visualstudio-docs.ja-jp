---
title: Timer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1971868e-89fa-4452-8ee7-76e4daf31b66
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1e5f6c6db903b3ecced2ac3ebc4aaa0a3e60910c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145500"
---
# <a name="timer"></a>タイマー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe の **Timer** オプションは、サンプリングするプロファイリング イベントをプロセッサのクロック サイクルに設定し、必要に応じて、サンプリング間隔のサイクル数を既定の 10,000,000 から変更します。 1 GHz のプロセッサでは、クロック サイクル数 10,000,000 の場合、1 秒あたりのサンプル数は約 100 になります。 指定できる最小サイクル数は、50,000 です。  
  
 **Timer** を使用できるのは、サンプリング プロファイリング メソッドを使用する場合のみであり、**Launch** または **Attach** オプションも含むコマンド ラインでのみ使用できます。  
  
 既定では、プロファイラーのサンプリング イベントは、プロセッサのクロック サイクルに設定され、サンプリング間隔は 10,000,000 に設定されます。 **Timer**、**PF**、**Sys**、**Counter** の各オプションを使用すると、サンプリング イベントおよびサンプリング間隔を設定できます。 **GC** オプションは、割り当ておよびガベージ コレクション イベントが発生するたびに、.NET メモリ データを収集します。 コマンド ラインには、上記のオプションのいずれか 1 つだけを指定できます。  
  
 サンプリング イベントおよびサンプリング間隔は、**Launch** オプションまたは **Attach** オプションを含む最初のコマンド ラインでのみ設定できます。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe {/Launch:AppName|/Attach:PID} /Timer[:Cycles] [Options]  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Cycles`  
 サンプリング間隔でのプロセッサのクロック サイクル数を指定する整数の値。 ‎`Cycles` が指定されていない場合、間隔は 10,000,000 に設定されます。 コンマを含めずに値を指定してください。  
  
## <a name="required-options"></a>必須オプション  
 **Timer** は、以下のいずれかのオプションを含むコマンド ラインでのみ指定できます。  
  
 **起動:**`AppName`  
 プロファイラーと、`AppName` で指定されたアプリケーションを起動します。  
  
 **アタッチ:**`PID`  
 プロファイラーをプロセス ID (`PID`) で指定されたプロセスにアタッチします。  
  
## <a name="invalid-options"></a>無効なオプション  
 以下のオプションは、**Timer** と同じコマンド ラインに指定することはできません。  
  
 **PF**[**:** `Events` ]  
 サンプリング イベントをページ フォールトに設定します。オプションで、サンプリング間隔を `Events` に設定します。 既定の PF 間隔は 10 です。  
  
 **Sys**[**:** `Events` ]  
 サンプリング イベントをオペレーティング システムの呼び出しに設定します。オプションで、サンプリング間隔を `Events` に設定します。 既定の Sys 間隔は 10 です。  
  
 **カウンタ**[**:** `Name,Reload,FriendlyName` ]  
 サンプリング イベントを、`Name` で指定された CPU パフォーマンス カウンターに設定し、サプリング間隔を `Reload` に設定します。  
  
 **GC**[**:**{**Allocation**&#124;**Lifetime**}]  
 .NET メモリ データを収集します。 既定 (**割り当て**) では、すべてのメモリ割り当てイベントでデータが収集されます。 **Lifetime**パラメーターを指定すると、ガベージコレクションイベントごとにデータも収集されます。  
  
## <a name="example"></a>例  
 プロファイラーのサンプリング間隔をプロセッサ サイクル数 1,000,000 に設定する方法を次の例に示します。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Timer:1000000  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
