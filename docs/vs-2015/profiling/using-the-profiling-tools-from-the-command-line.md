---
title: コマンド ラインからのプロファイリング ツールの使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- command line, performance tools
- command-line tools, performance tools
- profiling tools,command line
- tools, command-line
- command line, tools
ms.assetid: 6593fa82-181e-4009-a0ed-02aa24c2c063
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ebd0fbabb73d4c77d1d888b207882e7403f46aab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842084"
---
# <a name="using-the-profiling-tools-from-the-command-line"></a>コマンド ラインからのプロファイリング ツールの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールのコマンド ライン ツールを使用して、コマンド プロンプトでアプリケーションをプロファイリングしたり、バッチ ファイルやスクリプトでプロファイリングを自動化したりできます。 コマンド プロンプトでレポート ファイルを生成することもできます。 スタンドアロンの簡易プロファイラーを使用すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされていないコンピューター上のデータを収集できます。  
  
> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 ｢[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**シンボルの場所を設定します。** 関数とパラメーターの名前を表示するには、プロファイラーがプロファイリングされたバイナリのシンボル (.pdb) ファイルにアクセスできる必要があります。 これらのファイルには、解析で表示する Microsoft オペレーティング システムとアプリケーション用のシンボル ファイルが含まれている必要があります。 パブリックの Microsoft シンボル サーバーを使用して、Microsoft バイナリ用の正しい .pdb ファイルがあるかどうかを確認できます。|-   [方法: コマンドラインからシンボルファイルの場所を指定する](../profiling/how-to-specify-symbol-file-locations-from-the-command-line.md)|  
|**アプリケーションのプロファイリング:** ターゲット アプリケーションのプロファイリングに使用するコマンド ライン ツールとオプションは、アプリケーションの種類、プロファイリングの方法、ターゲット アプリケーションがマネージド アプリケーションであるかネイティブ アプリケーションであるかによって異なります。|-   [コマンドラインからのプロファイル方法の使用](../profiling/using-profiling-methods-to-collect-performance-data-from-the-command-line.md)<br />-   [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)<br />-   [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)<br />-   [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)|  
|**.xml レポートおよび .csv レポートの作成:** コマンド プロンプトでプロファイリングを実行すると、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインターフェイスで表示できるデータ ファイルが作成されます。 VSPerfReport コマンド ライン ツールを使用して、データの .xml ファイルまたはコンマ区切り値 (.csv) ファイルを生成することもできます。|-   [コマンドラインからのプロファイラーレポートの作成](../profiling/creating-profiler-reports-from-the-command-line.md)<br />-   [VSPerfReport](../profiling/vsperfreport.md)|  
|**Visual Studio がインストールされていないコンピューター上のコードのプロファイリング:** プロファイリング ツールのスタンドアロンのプロファイラーを使用して、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされていないコンピューター上のアプリケーションのデータを収集できます。|-   [方法: スタンドアロンのプロファイラーをインストールする](../profiling/how-to-install-the-stand-alone-profiler.md)|  
  
## <a name="reference"></a>リファレンス  
 [コマンドラインプロファイルツールリファレンス](../profiling/command-line-profiling-tools-reference.md)  
  
## <a name="see-also"></a>参照  
 [パフォーマンス エクスプ ローラー](../profiling/performance-explorer.md)
