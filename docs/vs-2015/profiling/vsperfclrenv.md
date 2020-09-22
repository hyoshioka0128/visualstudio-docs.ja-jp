---
title: VSPerfCLREnv | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- command-line tools, VSPerfCLREnv
- command line, tools
- performance tools, VSPerfCLREnv
- profiling tools,VSPerfCLREnv
- VSPerfCLREnv tool
ms.assetid: 4bc9dd6e-379c-4930-9bba-59a4faa93303
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: afee2c56a7f29d50f46c7cbb734bc0297223845c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842196"
---
# <a name="vsperfclrenv"></a>VSPerfCLREnv
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCLREnv ツールは、.NET Framework アプリケーションをプロファイルするために必要な環境変数を設定するために使用されます。 このツールでは、次の構文が使用されます。  
  
```  
VsPerfCLREnv [/option]  
```  
  
 選択するオプションは、プロファイルの 3 つの種類 (サンプリング、インストルメンテーション、グローバル) のうち、どれを使用するかによって異なります。 プロファイル データに階層相互作用データを含めるには、別のオプションが必要です。 各オプションの構文については、以下の表で説明します。  
  
> [!NOTE]
> プロファイルが完了したら、 **/off** オプションまたは **/globaloff** オプションを指定して **VSPerfCLREnv** を実行し、プロファイルに必要な環境変数を削除します。 詳細については、以下で示される「環境設定を削除するための VSPerfCLREnv オプション」を参照してください。  
  
 **階層相互作用データを含めるための VSPerfCLREnv オプション**  
  
> [!WARNING]
> 階層相互作用プロファイル データは、[!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、または [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)] を使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] および [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]のみです。  
  
 階層相互作用のプロファイルでは、多階層アプリケーションの ADO.NET クエリに関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。 相互作用データは、プロファイル方法に関係なく、どのプロファイルの実行にも追加できます。  
  
 **InteractionOn** オプションおよび **GlobalInteractionOn** オプションを使用すると、階層相互作用データを収集できます。 相互作用オプションは、アプリケーションをプロファイルするために必要な VSPerfCLREnv 環境変数を設定した後に設定する必要があります。  
  
 次の例には、サンプリング メソッドを使用するプロファイル実行に階層相互作用データが含まれています。  
  
```  
VSPerfCLREnv /SampleOn  
VSPerfCLREnv /InteractionOn  
VSPerfCmd /Start:Sample /Output:MyApp.exe.vsp /Launch:MyApp.exe  
```  
  
 次の例には、Windows サービスのプロファイルの実行に階層相互作用データが含まれています。  
  
```  
VSPerfCLREnv /GlobalSampleOn  
VSPerfCLREnv /GlobalInteractionOn  
REM Restart the computer and start the service  
VSPerfCmd /Start:Sample /Output:MyService.exe.vsp   
VSPerfCmd /Attach:MyService.exe  
```  
  
 **プロセス インストルメンテーション プロファイル用の VSPerfCLREnv オプション**  
  
 次の表で、インストルメンテーション プロファイル用の VSPerfCLREnv オプションについて説明します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**TraceOn**|インストルメンテーション メソッドを使用したプロファイルを有効にします。 メモリ割り当てのプロファイルまたはオブジェクトの有効期間データの収集は有効にしません。|  
|**TraceGC**|インストルメンテーション メソッドを使用したメモリ割り当てのプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|  
|**TraceGCLife**|インストルメンテーション メソッドを使用したメモリ割り当てのプロファイルとオブジェクトの有効期間データの収集を有効にします。|  
  
 **プロセス サンプリング プロファイル用の VSPerfCLREnv オプション**  
  
 次の表で、サンプリング プロファイル用の VSPerfCLREnv オプションについて説明します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**SampleOn**|サンプリング メソッドを使用したプロファイルを有効にします。 メモリ割り当てのプロファイルまたはオブジェクトの有効期間データの収集は有効にしません。|  
|**SampleGC**|サンプリング メソッドを使用したメモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|  
|**SampleGCLife**|サンプリング メソッドを使用したメモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集も有効にします。|  
|**SampleLineOff**|.NET 行レベルのプロファイル データの収集を無効にします。|  
  
 **グローバル プロファイル用の VSPerfCLREnv オプション**  
  
 ユーザーではなくオペレーティング システムによって起動された ASP.NET Web アプリケーションなどのマネージド サービスをプロファイルするには、グローバル プロファイル用の VSPerfCLREnv オプションを使用します。 グローバル バージョンの VSPerfCLREnv オプションについての説明を次の表に示します。 これらのオプションにより、適切な環境変数がレジストリに設定されます。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**GlobalTraceOn**|インストルメンテーション メソッドを使用したグローバル プロファイルを有効にします。 メモリ割り当てイベントまたはオブジェクトの有効期間データは収集しません。|  
|**GlobalTraceGC**|インストルメンテーション メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|  
|**GlobalTraceGCLife**|インストルメンテーション メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集も有効にします。|  
|**GlobalSampleOn**|サンプリング メソッドを使用したグローバル プロファイルを有効にします。 メモリ割り当てイベントまたはオブジェクトの有効期間データの収集は有効にしません。|  
|**GlobalSampleGC**|サンプリング メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|  
|**GlobalSampleGCLife**|サンプリング メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集も有効にします。|  
  
 **環境設定を削除するための VSPerfCLREnv オプション**  
  
 マネージド アプリケーションのプロファイルが完了したら、次のいずれかのオプションを使用して、VSPerfCLREnv で追加した環境変数を削除します。 次の表で、標準的な環境変数とグローバル環境変数の両方を削除する方法について説明します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|**Off**|標準的な .NET プロファイル用の環境変数を削除します。 このオプションは、グローバルではない VSPerfClrEnv オプションを使用してプロファイラー環境変数を設定した場合に使用します。|  
|**GlobalOff**|グローバルな .NET プロファイル用の環境変数を削除します。 プロファイラーではなく、オペレーティング システムによってアプリケーションが起動された場合に、このオプションを使用します。|  
  
## <a name="remarks"></a>解説  
 IDE のパフォーマンス エクスプローラーを使用して起動されたマネージド アプリケーションの場合、アプリケーションのプロファイルにこれらのオプションは必要ありません。 必要なすべての環境設定は、パフォーマンス エクスプローラーによって設定されます。  
  
 プロファイル中に正しい環境が設定されていないと、分析時に警告が報告され、マネージド関数名は正しく解決されません。  
  
## <a name="see-also"></a>参照  
 [コマンドラインからのプロファイル](../profiling/using-the-profiling-tools-from-the-command-line.md)
