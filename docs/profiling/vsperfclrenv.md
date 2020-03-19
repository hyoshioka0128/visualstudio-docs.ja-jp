---
title: VSPerfCLREnv | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command-line tools, VSPerfCLREnv
- command line, tools
- performance tools, VSPerfCLREnv
- profiling tools,VSPerfCLREnv
- VSPerfCLREnv tool
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 2163ebb9b363de8ee638998dbe56fd76f5a891c8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779910"
---
# <a name="vsperfclrenv"></a>VSPerfCLREnv

VSPerfCLREnv ツールは、.NET Framework アプリケーションをプロファイルするために必要な環境変数を設定するために使用されます。 このツールでは、次の構文が使用されます。

```cmd
VsPerfCLREnv [/option]
```

選択するオプションは、プロファイルの 3 つの種類 (サンプリング、インストルメンテーション、グローバル) のうち、どれを使用するかによって異なります。 プロファイル データに階層相互作用データを含めるには、別のオプションが必要です。 各オプションの構文については、以下の表で説明します。

> [!NOTE]
> プロファイルが完了したら、 **/off** オプションまたは **/globaloff** オプションを指定して **VSPerfCLREnv** を実行し、プロファイルに必要な環境変数を削除します。 詳細については、以下で示される「環境設定を削除するための VSPerfCLREnv オプション」を参照してください。

## <a name="vsperfclrenv-options-for-including-tier-interaction-data"></a>階層相互作用データを含めるための VSPerfCLREnv オプション

> [!WARNING]
> 階層相互作用プロファイル データは、Visual Studio の任意のエディションを使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、Visual Studio Enterprise のみです。

階層相互作用のプロファイルでは、多階層アプリケーションの ADO.NET クエリに関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。 相互作用データは、プロファイル方法に関係なく、どのプロファイルの実行にも追加できます。

**InteractionOn** オプションおよび **GlobalInteractionOn** オプションを使用すると、階層相互作用データを収集できます。 相互作用オプションは、アプリケーションをプロファイルするために必要な VSPerfCLREnv 環境変数を設定した後に設定する必要があります。

次の例には、サンプリング メソッドを使用するプロファイル実行に階層相互作用データが含まれています。

```cmd
VSPerfCLREnv /SampleOn
VSPerfCLREnv /InteractionOn
VSPerfCmd /Start:Sample /Output:MyApp.exe.vsp /Launch:MyApp.exe
```

次の例には、Windows サービスのプロファイルの実行に階層相互作用データが含まれています。

```cmd
VSPerfCLREnv /GlobalSampleOn
VSPerfCLREnv /GlobalInteractionOn
REM Restart the computer and start the service
VSPerfCmd /Start:Sample /Output:MyService.exe.vsp
VSPerfCmd /Attach:MyService.exe
```

## <a name="vsperfclrenv-options-for-process-instrumentation-profiling"></a>プロセス インストルメンテーション プロファイル用の VSPerfCLREnv オプション

次の表で、インストルメンテーション プロファイル用の VSPerfCLREnv オプションについて説明します。

|オプション|[説明]|
|------------|-----------------|
|**TraceOn**|インストルメンテーション メソッドを使用したプロファイルを有効にします。 メモリ割り当てのプロファイルまたはオブジェクトの有効期間データの収集は有効にしません。|
|**TraceGC**|インストルメンテーション メソッドを使用したメモリ割り当てのプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|
|**TraceGCLife**|インストルメンテーション メソッドを使用したメモリ割り当てのプロファイルとオブジェクトの有効期間データの収集を有効にします。|

## <a name="vsperfclrenv-options-for-process-sampling-profiling"></a>プロセス サンプリング プロファイル用の VSPerfCLREnv オプション

次の表で、サンプリング プロファイル用の VSPerfCLREnv オプションについて説明します。

|オプション|[説明]|
|------------|-----------------|
|**SampleOn**|サンプリング メソッドを使用したプロファイルを有効にします。 メモリ割り当てのプロファイルまたはオブジェクトの有効期間データの収集は有効にしません。|
|**SampleGC**|サンプリング メソッドを使用したメモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|
|**SampleGCLife**|サンプリング メソッドを使用したメモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集も有効にします。|
|**SampleLineOff**|.NET 行レベルのプロファイル データの収集を無効にします。|

## <a name="vsperfclrenv-options-for-global-profiling"></a>グローバル プロファイル用の VSPerfCLREnv オプション

ユーザーではなくオペレーティング システムによって起動された ASP.NET Web アプリケーションなどのマネージド サービスをプロファイルするには、グローバル プロファイル用の VSPerfCLREnv オプションを使用します。 グローバル バージョンの VSPerfCLREnv オプションについての説明を次の表に示します。 これらのオプションにより、適切な環境変数がレジストリに設定されます。

|オプション|[説明]|
|------------|-----------------|
|**GlobalTraceOn**|インストルメンテーション メソッドを使用したグローバル プロファイルを有効にします。 メモリ割り当てイベントまたはオブジェクトの有効期間データは収集しません。|
|**GlobalTraceGC**|インストルメンテーション メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|
|**GlobalTraceGCLife**|インストルメンテーション メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集も有効にします。|
|**GlobalSampleOn**|サンプリング メソッドを使用したグローバル プロファイルを有効にします。 メモリ割り当てイベントまたはオブジェクトの有効期間データの収集は有効にしません。|
|**GlobalSampleGC**|サンプリング メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集は有効にしません。|
|**GlobalSampleGCLife**|サンプリング メソッドを使用したグローバル メモリ割り当てプロファイルを有効にします。 オブジェクトの有効期間データの収集も有効にします。|

## <a name="vsperfclrenv-options-to-delete-environment-settings"></a>環境設定を削除するための VSPerfCLREnv オプション

 マネージド アプリケーションのプロファイルが完了したら、次のいずれかのオプションを使用して、VSPerfCLREnv で追加した環境変数を削除します。 次の表で、標準的な環境変数とグローバル環境変数の両方を削除する方法について説明します。

|オプション|[説明]|
|------------|-----------------|
|**Off**|標準的な .NET プロファイル用の環境変数を削除します。 このオプションは、グローバルではない VSPerfClrEnv オプションを使用してプロファイラー環境変数を設定した場合に使用します。|
|**GlobalOff**|グローバルな .NET プロファイル用の環境変数を削除します。 プロファイラーではなく、オペレーティング システムによってアプリケーションが起動された場合に、このオプションを使用します。|

## <a name="remarks"></a>解説

IDE のパフォーマンス エクスプローラーを使用して起動されたマネージド アプリケーションの場合、アプリケーションのプロファイルにこれらのオプションは必要ありません。 必要なすべての環境設定は、パフォーマンス エクスプローラーによって設定されます。

プロファイル中に正しい環境が設定されていないと、分析時に警告が報告され、マネージド関数名は正しく解決されません。

## <a name="see-also"></a>参照

[コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
