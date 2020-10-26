---
title: Launch | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: f81bde5c-3394-4b79-a315-c2f6491689b3
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c910ef1519181f1402cbec1d31686492e30f343d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68154757"
---
# <a name="launch"></a>Launch
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**Launch** オプションは、サンプリング メソッドを使用するプロファイラーを起動し、指定されたアプリケーションも起動します。  
  
 **Launch** オプションを使用するには、**Start** オプションで **Sample** メソッドを指定する必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /Launch:AppName [Options]  
```  
  
#### <a name="parameters"></a>パラメーター  
 `AppName`  
 起動するアプリケーションの名前。 現在のディレクトリからの完全パスおよび部分パスがサポートされます。  
  
## <a name="valid-options"></a>有効なオプション  
 **Launch** オプションと組み合わせて単一コマンド ラインで指定できる VSPerfCmd オプションを以下に示します。  
  
 **開始:**`Method`  
 コマンド ライン プロファイラー セッションを初期化し、指定されたプロファイル方法を設定します。  
  
 **Globalon** と **GlobalOff**  
 プロファイリングを再開 (**GlobalOn**) または一時停止 (**GlobalOff**) しますが、プロファイル セッションは終了しません。  
  
 **Processon:** `PID`**ProcessOff**:`PID`  
 指定されたプロセスのプロファイリングを再開 (**ProcessOn**) または一時停止 (**ProcessOff**) します。  
  
 **TargetCLR**  
 プロファイル セッションに複数バージョンの .NET Framework 共通言語ランタイム (CLR) が読み込まれている場合に、プロファイルを行う CLR のバージョンを指定します。 既定では、最初に読み込まれたバージョンがプロファイルされます。  
  
## <a name="exclusive-options"></a>排他的なオプション  
 次のオプションは、**Launch** オプションと共に指定する場合にのみ使用できます。  
  
 **コンソール**  
 指定されたコマンド ライン アプリケーションを新しいウィンドウで起動します。  
  
 **Args:**`ArgList`  
 アプリケーションに渡す引数リストを指定します。  
  
 **LineOff**  
 行レベルのプロファイル データの収集を無効にします。  
  
## <a name="sampling-options"></a>サンプリングのオプション  
 **Launch** コマンド ラインでは、次のサンプリング間隔オプションのいずれかを指定できます。 既定のサンプリング間隔は、10,000,000 プロセッサ クロック サイクルです。  
  
 **Timer**[**:** `Cycles` ]**PF**[**:** `Events` ]**Sys**[**:** `Events` ]**カウンター**[**:** `Name` , `Reload` , `FriendlyName` ]**GC**[:**割り当て**&#124;**有効期間**]  
 サンプリング間隔の数値と種類を指定します。  
  
- **Timer** - `Cycles` のプロセッサ クロック サイクル (停止なし) ごとにサンプリングを行います。 `Cycles` が指定されていない場合、10,000,000 サイクルが使用されます。  
  
- **PF** - `Events` のページ フォールトごとにサンプリングを行います。 `Events` が指定されていない場合は、10 ページ フォールトになります。  
  
- **Sys** - オペレーティング システムへの `Events` の呼び出しごとにサンプリングを行います。 `Events` が指定されていない場合は、10 システム呼び出しが使用されます。  
  
- **Counter** - `Name` で指定された CPU パフォーマンス カウンターの `Reload` の数値ごとにサンプリングを行います。 必要に応じて、`FriendlyName` でプロファイラー レポート内の列ヘッダーとして使用する文字列を指定できます。  
  
- **GC** - .NET メモリ データを収集します。 既定 (**allocation**) では、データはメモリの割り当てイベントごとに収集されます。 **lifetime** パラメーターが指定されている場合、ガベージ コレクション イベントごとのデータも収集されます。  
  
## <a name="example"></a>例  
 **Launch** を使用してアプリケーションを起動する例を以下に示します。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
