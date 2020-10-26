---
title: '方法: スクリプトにアタッチする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- script debugging, attaching to script
- script, attaching to
- processes, attaching to script
- remote debugging, attaching to script
ms.assetid: 82013e9a-ef53-4fd2-b451-a6891cdc6307
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 719654916087e7c7f4249ff52abbed628a2c56a2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704493"
---
# <a name="how-to-attach-to-script"></a>方法 : スクリプトにアタッチする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、デバッグを目的として Visual Studio デバッガーを手動でスクリプト ファイルにアタッチする方法について説明します。  
  
### <a name="to-attach-to-a-running-process"></a>実行中のプロセスにアタッチするには  
  
1. **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします (開いているプロジェクトがない場合は、**[ツール]** メニューの **[プロセスにアタッチ]** を選択します。)  
  
2. **[プロセスにアタッチ]** ダイアログ ボックスの **[選択可能なプロセス]** リストで、アタッチするスクリプト プロセスを探します。 **[型]** 列を参照することで、スクリプト プロセスを識別できます。  
  
   1. デバッグするプロセスが別のコンピューターで実行中の場合は、最初にリモート コンピューターを選択する必要があります。 詳細については、[リモート コンピューターを選択する](https://msdn.microsoft.com/4332ba8e-2f0b-4f62-b96a-e762b9f3c3ba)」を参照してください。  
  
   2. プロセスが別のユーザー アカウントで実行されている場合は、 **[すべてのユーザーからのプロセスを表示する]** チェック ボックスをオンにします。  
  
   3. **リモート デスクトップ接続**経由で接続している場合は、**[すべてのセッションのプロセスを表示する]** チェック ボックスをオンにします。  
  
3. アタッチするプロセスをクリックします。  
  
4. **にアタッチ**ボックスを表示する必要があります**スクリプト コード**または**自動: スクリプト コード**します。 何も表示されない場合は、次の手順に従います。  
  
   1. **[選択]** をクリックします。  
  
   2. **[コードの種類の選択]** ダイアログ ボックスの **[次のコードの種類をデバッグする]** をクリックし、**[スクリプト]** を選択します。  
  
   3. **[OK]** をクリックします。  
  
5. **[アタッチ]** をクリックします。  
  
    このとき、スクリプトのデバッグが Internet Explorer で無効になっていることを知らせる警告が表示されることがあります。 その場合を参照してください。[警告: スクリプト デバッグが無効](../debugger/warning-script-debugging-disabled.md)します。  
  
   **[プロセス]** ダイアログ ボックスを開くと、 **[選択可能なプロセス]** ボックスが自動的に表示されます。 このダイアログ ボックスが開いている間に、プロセスをバックグラウンドで開始および停止できます。 このため、表示内容に現在の状態が反映されていないこともあります。 **[更新]** を押すと、いつでもリストを更新して、現在のプロセス一覧を確認できます。  
  
   デバッグ中には複数のプログラムにアタッチできますが、デバッガーでアクティブになっているプログラムは常に 1 つだけです。 アクティブなプログラムは、[デバッグの場所] ツール バーで設定できます。 詳細については、「 [方法: 現在のプロセスを設定する](https://msdn.microsoft.com/7e1d7fa5-0e40-44cf-8c41-d3dba31c969e)」を参照してください。  
  
   **[デバッグ]** メニューのすべての実行コマンドは、アクティブ プログラムに影響します。 [プロセス] ダイアログボックスから、デバッグされているプログラムを中断できます。「 [ブレークポイントの使用」を](../debugger/using-breakpoints.md)参照してください。  
  
> [!NOTE]
> 信頼関係のないユーザー アカウントによって所有されているプロセスにアタッチしようとすると、セキュリティ警告の確認ダイアログ ボックスが表示されます。 詳細については、「[セキュリティ警告: 信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。以下の情報に関して疑わしい点がある場合や、不明な場合は、このプロセスにアタッチしないでください](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015)」を参照してください。  
  
 ターミナル サービス (リモート デスクトップ) セッションでのデバッグ時には、[選択可能なプロセス] ボックスに、使用可能なプロセスのすべてが表示されない場合があります。 [!INCLUDE[WinXPSvr](../includes/winxpsvr-md.md)] 以降のバージョンでは、Visual Studio を制限付きユーザーとして実行している場合、[選択可能なプロセス] ボックスには、セッション 0 で実行しているプロセスは表示されません。セッション 0 は、サービスおよび w3wp.exe を含むその他のサーバー プロセス用に使用されます。 この問題を解決するには、管理者アカウントで Visual Studio を実行するか、ターミナル サービス セッションではなくサーバー コンソールから Visual Studio を実行します。 どちらの回避策も実行できない場合、3 つ目のオプションとして、Windows コマンド ラインで「vsjitdebugger.exe -p ProcessId」と入力することで、プロセスにアタッチできます。 プロセス ID は tlist.exe を使用して確認できます。 tlist.exe を入手するには、[Windows Hardware Developer Central](https://developer.microsoft.com/windows/hardware) で Windows 対応のデバッグ ツールをダウンロードし、インストールします。  
  
## <a name="see-also"></a>参照  
 [クライアント側スクリプトのデバッグ](../debugger/client-side-script-debugging.md)   
 [実行中のプロセスにアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [セキュリティ警告: 信頼されていないユーザーが所有するプロセスにアタッチすることは危険な場合があります。次の情報が疑わしいと思われる場合や、不明な場合は、このプロセスにアタッチしないでください。](/visualstudio/debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user?view=vs-2015)   
 [デバッガーのセキュリティ](../debugger/debugger-security.md)
