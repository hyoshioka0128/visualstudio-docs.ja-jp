---
title: AutoMark | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: c4de965e-0364-4f78-9936-1f509e85df74
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4fb849b43e21010d9183f53e31ccf6bbc70736b6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157191"
---
# <a name="automark"></a>AutoMark
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**AutoMark** オプションは、Windows ソフトウェア パフォーマンス カウンター イベントを収集する間隔をミリ秒単位で指定します。 Windows パフォーマンス カウンターは **WinCounter** オプションで指定されます。  
  
 **AutoMark** オプションはコマンド ラインで 1 つだけ指定できます。 **AutoMark** によって指定される **WinCounter** サンプリング間隔はメインのサンプリング間隔には依存しません。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /Start:Method /WinCounter:Path /AutoMark:Milliseconds  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Milliseconds`  
 Windows パフォーマンス カウンター イベントを収集する間隔をミリ秒単位で指定します。  
  
## <a name="required-options"></a>必須オプション  
 **Wincounter:**`Path`  
 収集する Windows パフォーマンス カウンターを指定します。 インストルメンテーション メソッドを使用するとき、複数の Windows カウンターを指定できます。 サンプリング メソッドを使用するとき、ソフトウェア カウンターを 1 つだけ指定できます。 **WinCounter** オプションは、**Start** オプションが含まれるコマンド ラインに指定する必要があります。  
  
## <a name="example"></a>例  
 この例では、2 つの Windows パフォーマンス カウンターに対して 1000 ミリ秒単位のサンプリング間隔が設定されます。  
  
```  
VSPerfCmd.exe /Start:Trace /Output:TestApp.exe.vsp /WinCounter:"\Process(*)\% Processor Time" /WinCounter:"\ASP.NET\Pages/sec" /AutoMark:1000  
VSPerfCmd.exe /Launch:TestApp.exe  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
