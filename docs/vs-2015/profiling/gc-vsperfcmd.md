---
title: GC (VSPerfCmd) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7c81e88b-a748-4cf5-a7a1-3429608e1b54
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2bdb28f74dd305dc497521e95d38e00192c21c54
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193603"
---
# <a name="gc-vsperfcmd"></a>GC (VSPerfCmd)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**GC** オプションは、.NET Framework メモリ割り当てとオブジェクト有効期間データを収集できます。 **GC** オプションはサンプリング プロファイリング方法でのみ、かつ、**Launch** オプションとの併用でのみ利用できます。  
  
 **GC** オプションを使用するとき、VSPerfClrEnv **/sampleon** コマンドは必要ありません。  
  
 パラメーターが指定されていない場合、あるいは **Allocation** パラメーターが指定されている場合、.NET Framework メモリ割り当てデータのみが収集されます。 **Lifetime** パラメーターが指定されている場合、.NET Framework メモリ割り当てと .NET Framework オブジェクト有効期間データの両方が収集されます。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /Launch:AppName /GC[:{Allocation|Lifetime}] [Options]  
```  
  
#### <a name="parameters"></a>パラメーター  
 **Allocation**  
 既定値。 .NET Framework メモリ割り当てデータを収集します。  
  
 **有効期間**  
 .NET Framework メモリ割り当てデータと .NET Framework オブジェクト有効期間データの両方を収集します。  
  
## <a name="required-options"></a>必須オプション  
 **GC** オプションは、**Launch** オプションと一緒に指定する場合にのみ使用できます。  
  
 **起動:**`AppName`  
 指定したアプリケーションを起動し、サンプリング メソッドでプロファイリングを開始します。  
  
## <a name="example"></a>例  
 次の例では、アプリケーションが起動し、.NET Framework メモリ割り当てデータが収集されます。  
  
```  
VSPerfCmd.exe /Launch:TestApp.exe /gc  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
