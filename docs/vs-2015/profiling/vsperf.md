---
title: VSPerf | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: b5854e62-279e-4850-bfeb-0c6ef82f4805
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a8042b228a481dc3d720d8b422963db41abbddcd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533836"
---
# <a name="vsperf"></a>VSPerf
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**VsPerf** コマンド ライン ツールを使用して、次を行います。  
  
1. Visual Studio がデバイスにインストールされていない場合、Windows ストア アプリをコマンド ラインからプロファイルします。  
  
2. サンプリング プロファイル方法を使用して、Windows 8 デスクトップ アプリケーションと Windows Server 2012 アプリケーションをプロファイルします。  
  
   プロファイル オプションの詳細については、「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容  
 このトピックでは、`vsperf.exe` コマンド ライン ツールで使用できるオプションについて説明します。 このトピックは、次のセクションで構成されています。  
  
 [Windows ストアアプリのみ](#BKMK_windows_store_apps_only)  
  
 [Windows 8 デスクトップアプリケーションと Windows Server 2012 アプリケーションのみ](#BKMK_Windows_8_classic_applications_and_Windows_Server_2012_applications_only)  
  
 [すべてのアプリケーション](#BKMK_All_applications)  
  
## <a name="windows-store-apps-only"></a><a name="BKMK_windows_store_apps_only"></a> Windows ストア アプリのみ  
 これらのオプションは、Windows ストア アプリにのみ適用されます。  
  
|オプション|説明|  
|-|-|  
|**/app:{AppName}**|プロファイラーを起動し、スタート メニューから起動される指定したアプリを待機します。<br /><br /> `vsperf /listapps` を実行して、インストール済みアプリの Name と PackageFullName を表示します。|  
|**/package:{PackageFullName}**|プロファイラーを起動し、スタート メニューから起動される指定したアプリを待機します。<br /><br /> `vsperf /listapps` を実行して、インストール済みアプリの Name と PackageFullName を表示します。|  
|**/js**|JavaScript アプリのプロファイルを行うために必要です。<br /><br /> JavaScript アプリからパフォーマンス データを収集します。<br /><br /> /package または /attach でのみ使用します。|  
|**/noclr**|省略可能。 CLR データは収集しません。<br /><br /> /package または /attach でのみ使用します。<br /><br /> 最適化で、マネージド シンボルは解決されません。|  
|**/listapps**|インストール済みアプリの Name と PackageFullName を一覧表示します。|  
  
## <a name="windows-8-desktop-applications-and-windows-server-2012-applications-only"></a><a name="BKMK_Windows_8_classic_applications_and_Windows_Server_2012_applications_only"></a> Windows 8 デスクトップ アプリケーション、および Windows Server 2012 のアプリケーションのみ  
 これらのオプションは、Windows ストア アプリでは機能しません。  
  
|オプション|説明|  
|-|-|  
|**/launch:{Executable}**|指定した実行可能ファイルのプロファイルを起動して開始します。|  
|**/args:{ExecutableArguments}**|**/launch** ターゲットに渡すようにコマンド ライン引数を指定します。|  
|**/console**|新しいコマンド ウィンドウで **/launch** ターゲットを実行します。|  
  
## <a name="all-applications"></a><a name="BKMK_All_applications"></a>すべてのアプリケーション  
 これらのオプションは、すべての Windows 8 アプリケーションまたは Windows Server 2012 アプリケーションに適用されます。  
  
|オプション|説明|  
|-|-|  
|**/attach:{PID&#124;ProcessName}[,PID&#124;ProcessName]...**|指定したプロセスからデータを収集します。<br /><br /> タスク マネージャーを使用して、実行中のアプリのプロセス ID (PID) とプロセス名を表示します。|  
|**/file:{ReportName}**|省略可能。 出力ファイルを指定します (既存のファイルを上書き)。<br /><br /> /package または /attach でのみ使用します。|  
|**/pause**|データ収集を一時停止します。|  
|**/resume**|データ収集を再開します。|  
|**/stop**|データ収集を停止し、ターゲット プロセスを終了します。|  
|**/detach**|データ収集を停止しますが、ターゲット プロセスの実行は続行します。|  
|**全**|プロファイラーの状態を表示します。|  
  
## <a name="see-also"></a>関連項目  
 [Windows 8 および Windows Server 2012 アプリケーションのパフォーマンスツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)   
 [コマンドラインからのプロファイル](../profiling/using-the-profiling-tools-from-the-command-line.md)
