---
title: Events (VSPerfCmd) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: eb139327-4783-4f2a-874c-efad377a7be4
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 265dc7f84fbd1ec19b520e2e30d3554e2c66683b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302136"
---
# <a name="events-vsperfcmd"></a>Events (VSPerfCmd)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe **Events** オプションは、Windows イベント トレーシング (ETW) のログ記録を制御します。 ETW データは、プロファイラー データ ファイルとは別の .etl ファイルに保存されます。 このデータは、[VSPerfReport](../profiling/vsperfreport.md) /summary:etw コマンドを利用し、レポートで表示できます。  
  
 **Events** オプションは、VSPerfCmd **Shutdown** コマンドが呼び出され、プロファイリングを停止する前にいつでも呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /events {On|Off} {Guid|ProviderName} [,Flags[,Level]  
```  
  
#### <a name="parameters"></a>パラメーター  
 **On**&#124;**Off**  
 イベント データの収集を開始または停止します。  
  
 `Guid`  
 プロバイダー コントロールの GUID。  
  
 `ProviderName`  
 Windows Management Instrumentation (WMI) に登録されているプロバイダーの名前。  
  
 `Flags`  
 イベント プロバイダーによって定義され、先頭に "0x" が付く 16 進数のフラグ値。  
  
 `Level`  
 収集されるデータの量を指定します。 `Level` はイベント プロバイダーによって定義されます。  
  
 **Events** オプションは、プロバイダー名として次のカーネル キーワードを理解します。  
  
 **Process**  
 プロセス イベント  
  
 **スレッド**  
 スレッド イベント  
  
 **イメージ**  
 イメージのロードとアンロード イベント  
  
 **Disk**  
 ディスク I/O イベント  
  
 **ファイル**  
 ファイル I/O イベント  
  
 **Hardfault**  
 ハード ページ フォールト  
  
 **Pagefault**  
 ソフト ページ フォールト  
  
 **Network**  
 ネットワーク イベント  
  
 **Registry**  
 レジストリ アクセス イベント  
  
 カーネル プロバイダーのみを有効にできます。 モニターがシャットダウンするまで、無効にできません。そのフラグを変更することもできません。  
  
## <a name="remarks"></a>コメント  
  
> [!NOTE]
> CLR ETW イベントが有効になっていると、追加のスタートアップ データがトレース ビュー レポートでも集められます。 スタートアップ イベントがレポートに表示されないようにするには、次のコマンドを使用します。  
  
```  
C:\<path>VSPerfCmd -events on, \".NET Common Language Runtime\", 0x7fffffff, 5  
```  
  
> [!IMPORTANT]
> スタートアップ イベントを除外しない場合、スタートアップ イベントはマネージド オブジェクト フォーマット (MOF) ファイルに一覧表示されないため、レポートに GUID として表示されます。 詳細については、Microsoft Web サイトの「[Sample Managed Object Format (MOF) File](https://go.microsoft.com/fwlink/?linkid=37118)」 (マネージド オブジェクト フォーマット (MOF) ファイルのサンプル) を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [プロファイリング (サービスの)](../profiling/command-line-profiling-of-services.md)
