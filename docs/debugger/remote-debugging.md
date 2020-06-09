---
title: リモート デバッグ | Microsoft Docs
ms.custom:
- remotedebugging
- seodec18
ms.date: 07/02/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.overview
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9918a2de67693c0232c94a736f12c7af0a0b959c
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301057"
---
# <a name="remote-debugging"></a>Remote Debugging
別のコンピューターに配置されている Visual Studio アプリケーションをデバッグすることができます。 このデバッグを行うには、Visual Studio リモート デバッガーを使用します。

リモート デバッグの詳細な手順については、次のトピックを参照してください。

|シナリオ|Link|
|-|-|-|
|Azure App Service|[スナップショット デバッガー](../debugger/debug-live-azure-applications.md)または[Azure での ASP.NET のリモート デバッグ](../debugger/remote-debugging-azure.md)|
|Azure 仮想マシン|[Azure での ASP.NET のリモート デバッグ](../debugger/remote-debugging-azure.md)|
|Azure Service Fabric|[Azure Service Fabric アプリケーションのデバッグ](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)|
|ASP.NET|[ASP.NET Core のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)または [ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|C# または Visual Basic|[C# プロジェクトまたは Visual Basic プロジェクトのリモート デバッグ](../debugger/remote-debugging-csharp.md)|
|C++|[C++ Project プロジェクトのリモート デバッグ](../debugger/remote-debugging-cpp.md)|
|ユニバーサル Windows アプリ (UWP)|[リモート コンピューターでの UWP アプリの実行](../debugger/run-windows-store-apps-on-a-remote-machine.md)または[インストールされているアプリ パッケージのデバッグ](../debugger/debug-installed-app-package.md)|

リモート デバッガーをダウンロードしてインストールするだけで、シナリオに関する追加の手順が不要な場合は、この記事の手順に従ってください。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="requirements"></a><a name="requirements_msvsmon"></a> 要件

[!INCLUDE [remote-debugger-requirements](../debugger/includes/remote-debugger-requirements.md)]

## <a name="optional-to-run-the-remote-debugger-from-a-file-share"></a><a name="fileshare_msvsmon"></a> (オプション) ファイル共有からリモート デバッガーを実行するには

リモート デバッガー (*msvsmon.exe*) は、Visual Studio Community、Professional、または Enterprise が既にインストールされているコンピューターにあります。 場合によっては、リモート デバッグをセットアップする最も簡単な方法は、ファイル共有からリモート デバッガー (msvsmon.exe) を実行することです。 使用に関する制限事項については、リモート デバッガーの [ヘルプ] ページ (リモート デバッガーの **[ヘルプ] > [使用法]** ) を参照してください。

1. お使いの Visual Studio のバージョンと一致するディレクトリで、*の msvsmon.exe* を見つけます。

   ::: moniker range=">=vs-2019"

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end
   ::: moniker range="vs-2017"

   *Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end

2. Visual Studio コンピューターで**リモート デバッガー** フォルダーを共有します。

3. リモート コンピューターで、共有フォルダーから *msvsmon.exe* を実行します。 [セットアップの手順](#bkmk_setup)に従います。

> [!TIP]
> コマンド ライン インストールおよびコマンド ライン参照については、Visual Studio がインストールされているコンピューターのコマンド ラインで「``msvsmon.exe /?``」と入力して、*msvsmon.exe* のヘルプ ページを参照してください (または、リモート デバッガーで **[ヘルプ] > [使用法]** に移動)。

## <a name="set-up-the-remote-debugger"></a><a name="bkmk_setup"></a> リモート デバッガーのセットアップ

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

### <a name="configure-the-remote-debugger"></a><a name="configure_msvsmon"></a> リモート デバッガーの構成
リモート デバッガーを初めて起動した後、リモート デバッガーの構成の一部を変更できます。

- 他のユーザーがリモート デバッガーに接続するためにアクセス許可を追加する必要がある場合は、 **[ツール] > [アクセス許可]** を選択します。 アクセス許可を付与または拒否するには、管理者特権が必要です。

     > [!IMPORTANT]
     > リモート デバッガーは、Visual Studio コンピューターに対して使用しているユーザー アカウントとは別のユーザー アカウントで実行できますが、その場合、リモート デバッガーのアクセス許可に別のユーザー アカウントを追加する必要があります。

     または、コマンド ラインで **/allow \<username>** パラメーターを使用してリモート デバッガーを開始できます: **msvsmon /allow \<username@computer>** 。

- 認証モードまたはポート番号を変更したり、リモート ツールのタイムアウト値を指定したりする必要がある場合は、 **[ツール] > [オプション]** を選択します。

     既定で使用されるポート番号の一覧については、「[リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください。

     > [!WARNING]
     > リモート ツールを認証なしモードで実行することも選択できますが、このモードの使用は避けることを強く推奨します。 このモードで実行した場合、ネットワーク セキュリティはまったく提供されません。 [認証なし] モードは、ネットワークに悪意のあるコードや悪意のあるトラフィックのリスクがないことが確実である場合にのみ選択してください。

## <a name="optional-configure-the-remote-debugger-as-a-service"></a><a name="bkmk_configureService"></a> (オプション) サービスとしてリモート デバッガーを構成する
ASP.NET および他のサーバー環境でのデバッグでは、リモート デバッガーを管理者として実行するか、常に実行する場合は、リモート デバッガーをサービスとして実行する必要があります。

 リモート デバッガーをサービスとして構成する場合は、次の手順のようにします。

1. **リモート デバッガー構成ウィザード** (rdbgwiz.exe) を見つけます (このアプリケーションは、リモート デバッガーとは別のアプリケーションです)。このアプリケーションは、リモート ツールをインストールした場合にのみ入手でき、 Visual Studio と共にはインストールされません。

2. 構成ウィザードの実行を開始します。 最初のページが表示されたら、 **[次へ]** をクリックします。

3. **[Visual Studio 2015 リモート デバッガー サービスを実行する]** チェック ボックスをオンにします。

4. ユーザー アカウントの名前とパスワードを追加します。

    このアカウントに、 **[サービスとしてログオン]** のユーザー権限を追加することが必要になる場合があります。 **[ローカル セキュリティ ポリシー]** (secpol.msc) を **[スタート]** ページまたはウィンドウで見つけます (または、コマンド プロンプトで「**secpol**」と入力します)。 ウィンドウが表示されたら、 **[ユーザー権利の割り当て]** をダブルクリックし、右ペインで **[サービスとしてログオン]** を見つけます。 これをダブルクリックします。 ユーザー アカウントを **[プロパティ]** ウィンドウに追加して **[OK]** をクリックします)。 **[次へ]** をクリックします。

5. リモート ツールが通信するネットワークの種類を選択します。 少なくとも 1 つのネットワークの種類を選択する必要があります。 コンピューターがドメインを介して接続されている場合は、最初の項目を選択する必要があります。 コンピューターがワークグループまたはホーム グループを介して接続されている場合は、2 番目または 3 番目の項目を選択する必要があります。 **[次へ]** をクリックします。

6. サービスを開始できた場合は、「 **Visual Studio リモート デバッガー構成ウィザードは正常に完了しました**」と表示されます。 サービスを開始できなかった場合は、「 **Visual Studio リモート デバッガー構成ウィザードを完了できませんでした**」と表示されます。 このページには、サービスを開始するために従う必要があるヒントもいくつか提供されます。

7. **[完了]** をクリックします。

   この時点で、リモート デバッガーはサービスとして実行されています。 これを確認するには、 **[コントロール パネル] > [サービス]** に移動して **[Visual Studio 2015 リモート デバッガー]** を探します。

   リモート デバッガー サービスは、 **[コントロール パネル] > [サービス]** で停止してから開始することができます。

## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>関連項目

- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモート IIS コンピューターでの ASP.NET Core のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)