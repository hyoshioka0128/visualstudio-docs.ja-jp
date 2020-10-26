---
title: Args | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 20c35949-1f29-4282-ac75-4e6c237d71bc
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 65759da4363891c713f906e6cb10f00443bcbceb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197910"
---
# <a name="args"></a>Args
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe **Args** オプションは、**Launch** サブコマンドの対象アプリケーションに渡される引数のリストを指定します。  
  
 **Args** は、コマンド ラインで **Launch** も指定された場合にのみ使用できます。 **Args** は、**Launch** を指定した場合のオプションです。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /Launch:AppName /Args:Arguments [Options]  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Arguments`  
 **Launch** コマンドのターゲット アプリケーションへの引数のリスト。  
  
## <a name="required-options"></a>必須オプション  
 **起動:**`AppName`  
 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。  
  
## <a name="example"></a>例  
 次の例では、**Args** オプションを使用して引数を TestApp.exe に渡します。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe /Args:"123, 'Hello World'"  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
