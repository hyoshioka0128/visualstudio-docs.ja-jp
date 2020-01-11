---
title: Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a704215d-d252-4087-921b-ac81ebe2a9c9
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a2fa9581d94b3b70ca427c292c147562a11d55a4
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75847995"
---
# <a name="performance-tools-on-windows-8-and-windows-server-2012-applications"></a>Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio パフォーマンス ツールがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 このトピックでは、Windows 8 および Windows Server 2012 のプラットフォームでのパフォーマンス ツールの変更点について説明します。  
  
> [!NOTE]
> その他のサポートされている Windows バージョン (Windows 7、Windows Server 2008 R2) でのパフォーマンス ツールに変更点はありません。  
  
## <a name="BKMK_In_this_topic"></a> このトピックの内容  
 [Visual Studio IDE から Windows ストア アプリ上のデータを収集する](#BKMK_Profiling_Windows_Store_apps_from_the_Visual_Studio_IDE)  
  
 [Windows 8 デスクトップまたは Windows Server 2012 で実行中のアプリ上のデータを Visual Studio IDE から収集する](#BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_from_the_Visual_Studio_IDE)  
  
- [Windows 8 デスクトップまたは Windows Server 2012 で実行中のアプリ上のデータを Visual Studio IDE からサンプリングを使用して収集する](#BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_by_using_sampling_from_the_Visual_Studio_IDE)  
  
  [コマンド ラインからのプロファイリング](#BKMK_Profiling_from_the_command_line)  
  
  [階層の相互作用 (TIP) データを収集する](#BKMK_Collecting_tier_interaction__TIP__data)  
  
## <a name="BKMK_Profiling_Windows_Store_apps_from_the_Visual_Studio_IDE"></a>Visual Studio IDE から Windows ストア アプリ上のデータを収集する  
 JavaScript および HTML 5 で記述された Windows ストア アプリのプロファイリングを行う場合は、JavaScript コードのインストルメンテーション データを収集します。 Visual C++、Visual C#、または Visual Basic で記述された Windows ストア アプリまたはコンポーネントのプロファイリングを行う場合は、ネイティブ コードおよびマネージド コードのサンプリング データを収集します。 ローカル コンピューターまたはリモート コンピューター上のアプリをプロファイリングすることもできます。  
  
 Windows ストア アプリのプロファイリングを行う場合、次のプロファイル機能およびオプションはサポートされていません。  
  
- サンプリング メソッドを使用した JavaScript アプリのプロファイリング。  
  
- インストルメンテーション メソッドを使用したマネージド コードおよびネイティブ コードのプロファイリング。  
  
- コンカレンシー プロファイル  
  
- .NET メモリ プロファイル。  
  
- 階層相互作用プロファイリング (TIP)。  
  
- サンプリング イベントや時間間隔の設定、追加のパフォーマンス カウンター データの収集などのサンプリング オプション。  
  
- パフォーマンス カウンター データや Windows カウンター データの収集、追加のコマンド ライン オプションの指定などのインストルメンテーション オプション。  
  
  Windows ストア アプリのプロファイリングの詳細については、Windows デベロッパー センターの次のトピックを参照してください。  
  
  [ローカル コンピューターでの Windows ストア アプリの実行](../debugger/run-windows-store-apps-on-the-local-machine.md)  
  
  [リモート コンピューターでの Windows ストア アプリの実行](../debugger/run-windows-store-apps-on-a-remote-machine.md)  
  
  [アプリのパフォーマンスの分析](https://msdn.microsoft.com/library/58acb30b-8428-41a6-b195-b0fdedb89575)  
  
- [JavaScript 関数タイミング](https://msdn.microsoft.com/library/b2bf49fc-aea7-4d9c-8fcf-cff8b8dd0c03)  
  
- [リモートデバイスでの JavaScript 関数タイミング](https://msdn.microsoft.com/library/d78812b6-a97e-46dc-8d99-e724d1d725d8)  
  
- [JavaScript 関数タイミング データの分析](https://msdn.microsoft.com/library/b5aea8d8-36df-47ba-a7ca-95406700ca9b)  
  
- [ローカル コンピューターでの Windows ストア アプリの Visual C++、Visual C#、および Visual Basic コードのプロファイリング](https://msdn.microsoft.com/2d0c939e-0bac-48c5-b727-46f6c6113060)  
  
- [リモート デバイスでの Windows ストア アプリの Visual C++、Visual C#、および Visual Basic コードのプロファイリング](https://msdn.microsoft.com/b932a2be-11b0-40fd-b996-75c6b6a79d22)  
  
- [Windows ストア アプリの Visual C++、Visual C#、および Visual Basic コードのパフォーマンス データの分析](https://msdn.microsoft.com/5de4a413-d924-425f-afc4-e1ecfb0fca18)  
  
  [このトピックの内容](#BKMK_In_this_topic)  
  
## <a name="BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_from_the_Visual_Studio_IDE"></a> Windows 8 デスクトップまたは Windows Server 2012 で実行中のアプリ上のデータを Visual Studio IDE から収集する  
 インストルメンテーション メソッドを使用したプロファイリングについては、Windows 8 での変更点はありません。  
  
 サンプリング メソッドを使用した階層相互作用プロファイリング (TIP) は、サポートされていません。  
  
### <a name="BKMK_Profiling_apps_running_on_the_Windows_8_desktop_or_on_Windows_Server_2012_by_using_sampling_from_the_Visual_Studio_IDE"></a> Windows 8 デスクトップまたは Windows Server 2012 で実行中のアプリ上のデータを Visual Studio IDE からサンプリングを使用して収集する  
 サンプリング メソッドを使用して Windows 8 デスクトップ アプリケーションまたは Windows Server 2012 アプリケーションのプロファイリングを行う場合、次のプロファイル機能およびオプションはサポートされていません。  
  
- 階層相互作用プロファイリング (TIP)。 インストルメンテーションを使用した TIP データの収集はサポートされます。  
  
- サンプリング イベントや時間間隔の設定、追加のパフォーマンス カウンター データの収集などのサンプリング オプション。  
  
## <a name="BKMK_Profiling_from_the_command_line"></a> コマンド ラインからのプロファイリング  
 Visual Studio がインストールされていないデバイスを含めて、Windows 8 デバイスおよび Windows Server 2012 デバイスでプロファイル データを収集するには、次の 2 つのコマンド ライン ツールを使用します。  
  
|ツール名|説明|  
|---------------|-----------------|  
|[VSPerf](../profiling/vsperf.md)|Windows ストア アプリからプロファイル データを収集し、Windows 8 デスクトップ アプリケーションおよび Windows Server 2012 アプリケーションからサンプル プロファイル データを収集します。|  
|[VSPerfCmd](../profiling/vsperfcmd.md)|Windows 8 デスクトップまたは Windows Server 2012 で実行されるアプリから、インストルメンテーション、コンカレンシー、および階層相互作用プロファイル データを収集します。 以前のバージョンの Windows からすべてのタイプのプロファイル データを収集します。|  
  
 これらのツールはどちらも、Visual Studio と共にローカル コンピューターにインストールされます。  
  
 Visual Studio がインストールされていないデバイスでアプリケーションをプロファイリングするには、次のいずれかを実行します。  
  
- [MSDN Web サイト](https://www.microsoft.com/visualstudio/eng#downloads+d-additional-software)から、Visual Studio 用のリモート ツールの一部としてツールをダウンロードします。  
  
- 既存の Visual Studio コンピューターから、スタンドアロンのプロファイラー ツール インストール プログラムをコピーして実行します。 インストールプログラムは *% VSInstallDir%* **\ Team ツールパフォーマンスツールセットアップ**フォルダーにあります。 リモート コンピューターのオペレーティング システム (x86/x64) に対応するセットアップ プログラムを選択します。  
  
> [!NOTE]
> TIP プロファイル データを収集するには、Visual Studio コンピューターにあるスタンドアロン プロファイラーをリモート コンピューターにインストールする必要があります。  
  
 コマンド ラインから Windows 8 アプリケーションおよび Windows Server 2012 アプリケーションのプロファイリングを行う場合、次のプロファイル機能およびオプションはサポートされていません。  
  
- [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md)でサンプリング モードを使用して、Windows 8 と Windows Server 2012 の Web アプリからデータを収集します。  
  
- VsPerfCmd.exe を使用したサンプリング データの収集。  
  
- サンプリング イベントや時間間隔の設定、追加のパフォーマンス カウンター データの収集などのサンプリング オプション。  
  
## <a name="BKMK_Collecting_tier_interaction__TIP__data"></a> 階層の相互作用 (TIP) データを収集する  
 階層相互作用プロファイリングにより、ADO.NET サービスを通じてデータベースと通信する多階層アプリケーションの関数の実行時間に関する追加情報が提供されます。 データは同期の関数呼び出しについてのみ収集されます。  
  
 **Visual Studio のエディション**  
  
 階層相互作用プロファイル データは、 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、または [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)]を使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、[!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] および [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] のみです。  
  
 **Windows 8 と Windows Server 2012**  
  
1. Windows 8 デスクトップまたは Windows Server 2012 で実行されるアプリから相互作用データを収集するには、インストルメンテーション メソッドを使用する必要があります。  
  
2. Windows ストア アプリの階層相互作用データを収集することはできません。  
  
3. 階層相互作用データは、サポートされている他のバージョンの Windows で、すべてのプロファイル方法に含めることができます。  
  
   **パフォーマンス ウィザードとパフォーマンス エクスプローラー**  
  
   パフォーマンス エクスプローラーから、階層相互作用データの収集オプションをプロファイリング実行に追加する必要があります。 また、パフォーマンス エクスプローラーのターゲット ノードに、プロジェクト、実行可能ファイル、または Web サイトを追加する必要があります。 「[Visual Studio IDE を使用した階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)」をご覧ください。  
  
   **リモート コンピューターでの TIP データの収集**  
  
   リモート コンピューターで階層相互作用データを収集するには、Visual Studio コンピューターの _%VSInstallDir%_ **\Team Tools\Performance Tools\Setups** フォルダーから **vs\_profiler\_** _\<プラットフォーム>_ **\_** _\<言語>_ **.exe** ファイルをリモート コンピューターにコピーしてインストールする必要があります。 [Visual Studio Remote Tools](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) のダウンロード パッケージにあるプロファイリング ツールを使用することはできません。  
  
   プロファイル データを収集するには、[VSPerfCmd](../profiling/vsperfcmd.md) または [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) を使用できます。  
  
   **TIP レポート**  
  
   階層相互作用データは、 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] または [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] IDE でのみ表示できます。 [VSPerfReport](../profiling/vsperfreport.md) の使用による、ファイル ベースの階層相互作用レポートは利用できません。  
  
## <a name="see-also"></a>参照  
 [パフォーマンス エクスプローラー](../profiling/performance-explorer.md)   
 [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)   
 [コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
