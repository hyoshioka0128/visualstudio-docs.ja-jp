---
title: Microsoft Visual Studio リモート デバッグ モニターに接続できません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.error.remote_debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: a1d959fc-3817-491c-831b-e6b768a3877a
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d62e7ce1c419a9c53e40e1ecf2f71497d60d7a23
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77477066"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Microsoft Visual Studio リモート デバッグ モニターに接続できません。
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このエラー メッセージは、無効な Visual Studio リモート デバッグ モニターの名前を **[プロセスにアタッチ]** ダイアログ ボックスに入力すると表示されます。 リモート デバッグ モニターの名前は、通常、リモート デバッグを実行するために接続するコンピューターの名前と同じです。 このメッセージは、リモート コンピューターがネットワーク上に存在しない、リモート コンピューター上でリモート デバッグ モニターが適切に設定されていない、またはネットワークの問題またはファイアウォールが存在するためにリモート コンピューターにアクセスできない場合に発生することがあります。  
  
> [!IMPORTANT]
> その他の支援が必要な場合は、Microsoft へのお問い合わせ方法について、「 [Talk to Us](../ide/talk-to-us.md) 」を参照してください。  
  
## <a name="i-got-this-message-while-i-was-debugging-locally"></a>ローカルでのデバッグ中にこのメッセージが表示される  
 ローカルでのデバッグ中にこのメッセージが表示される場合、ウイルス対策ソフトウェアまたはサード パーティ製のファイアウォールに原因がある可能性があります。 Visual Studio は 32 ビット アプリケーションであるため、リモート デバッガーの 64 ビット バージョンを使用して 64 ビット アプリケーションをデバッグします。 2 つのプロセスは、ローカル コンピューター内のローカル ネットワークを使用して通信します。 コンピューターからネットワーク トラフィックが送信されることはありませんが、サード パーティのセキュリティ ソフトウェアが通信を妨げる可能性があります。  
  
 次のセクションでは、このメッセージが表示される他のいくつかの理由、および問題を解決するために実行できる事柄について示します。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- Visual Studio リモート デバッグ モニターがリモート コンピューターにインストールされ、実行されていることを確認します。 リモートデバッガーとそのインストール方法の詳細については、「 [リモートデバッグ](../debugger/remote-debugging.md)」を参照してください。  
  
- Visual Studio で、プロジェクトのプロパティ (**プロジェクト/プロパティ/デバッグ**) を確認します。 **[リモート サーバー名]** が正しいことを確認します。  
  
- ネットワーク上のリモート コンピューターにアクセスできることを確認します。  
  
## <a name="the-remote-machine-is-not-reachable"></a>リモート コンピューターに到達できません  
 リモート コンピューターに [ping](https://technet.microsoft.com/library/ee624059\(v=ws.10\).aspx) してみてください。 ping に応答しない場合は、リモート ツールも接続できません。 リモート コンピューターを再起動するか、またはネットワークでリモート コンピューターが正しく構成されていることを確認してください。  
  
## <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>リモート デバッガーのバージョンが Visual Studio のバージョンと一致していない  
 ローカルで実行している Visual Studio のバージョンは、リモート コンピューターで実行されているリモート デバッグ モニターのバージョンと一致している必要があります。 これを解決するには、リモート デバッグ モニターの一致するバージョンをダウンロードして、インストールします。 Visual [studio サブスクリプション](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015) にアクセスして、使用している visual studio のバージョンに対応する適切なバージョンのリモートデバッガーを検索します。

## <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>ローカル コンピューターとリモート コンピューターの認証モードが異なる  

 ローカル コンピューターとリモート コンピューターで、同じ認証モードを使用する必要があります。 これを解決するには、両方のマシンで同じ認証モードを使用するようにします。 リモート デバッガーの **[ツール] / [オプション]** ダイアログで、認証モードを変更することができます。  
  
 認証モードの詳細については、「 [Windows 認証の概要](https://technet.microsoft.com/library/hh831472.aspx)」を参照してください。  
  
## <a name="the-remote-debugger-is-running-under-a-different-user-account"></a>異なるユーザー アカウントを使用してリモート デバッガーを実行している  
 これは、次のいずれかの方法で解消できます。  
  
- リモート デバッガーを停止し、ローカル コンピューターで使用しているアカウントで再起動します。  
  
- コマンド ラインで **/allow \<username>** パラメーターに `msvsmon /allow <username@computer>` を指定してリモート デバッガーを開始します。  
  
- リモートデバッガーのアクセス許可にユーザーを追加することができます (リモートデバッガーウィンドウで、[ **ツール]/[アクセス許可**])。  
  
- 前の手順の方法を使用できない場合は、すべてのユーザーにリモート デバッグの実行を許可します。 リモート デバッガー ウィンドウで、 **[ツール] / [オプション]** ダイアログに移動します。 **[認証なし]** を選択すると、 **[すべてのユーザーにデバッグを許可する]** をチェックできるようになります。 ただし、このオプションの使用は、他に選択肢がない場合、またはプライベート ネットワーク上で作業している場合に限る必要があります。  
  
## <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a>リモート コンピューター上のファイアウォールがリモート デバッガーへの着信接続を許可しない  
 Visual Studio とリモート デバッガーの間の通信を許可するように、Visual Studio のコンピューター上のファイアウォールとリモート コンピューター上のファイアウォールを構成する必要があります。 リモート デバッガーが使用するポートについては、「 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)」を参照してください。 Windows ファイアウォールを構成する方法については、「 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。  
  
## <a name="anti-virus-software-is-blocking-the-connections"></a>ウイルス対策ソフトウェアが接続をブロックしている  
 Windows のウイルス対策ソフトウェアがリモート デバッガーの接続を許可しても、その他のサード パーティ製のウイルス対策ソフトウェアがそれらの接続をブロックする可能性があります。 これらの接続を許可する方法については、ウイルス対策ソフトウェアのマニュアルを参照してください。  
  
## <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>ネットワーク セキュリティ ポリシーによってリモート コンピューターと Visual Studio の間の通信がブロックされる  
 ネットワーク セキュリティを調べ、通信をブロックしていないことを確認します。 Windows ネットワーク セキュリティ ポリシーの詳細については、「 [セキュリティ管理](https://msdn.microsoft.com/library/windows/desktop/ms721855\(v=vs.85\).aspx)」を参照してください。  
  
## <a name="the-network-is-too-busy-to-support-remote-debugging"></a>ネットワークがビジー状態でリモート デバッグをサポートできない  
 リモート デバッグを別の時点で実行するか、ネットワークでの作業を別の時点にスケジュールし直す必要がある場合があります。  
  
## <a name="more-help"></a>その他のヘルプ  
 コマンド ライン スイッチを含む、その他のリモート デバッガーのヘルプを表示するには、ブラウザーで次を開きます。  
  
 **res://C:\Program%20Files\Microsoft%20Visual%20Studio%2014.0\Common7\IDE\Remote%20Debugger\x64\msvsmon.exe/help.htm**  
  
## <a name="see-also"></a>参照  
 [Remote Debugging](../debugger/remote-debugging.md)
