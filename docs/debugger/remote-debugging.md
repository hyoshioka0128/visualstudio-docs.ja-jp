---
title: リモートデバッグ |Microsoft Docs
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
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78409263"
---
# <a name="remote-debugging"></a>リモート デバッグ
別のコンピューターに配置されている Visual Studio アプリケーションをデバッグすることができます。 このデバッグを行うには、Visual Studio リモート デバッガーを使用します。

リモートデバッグの詳細な手順については、次のトピックを参照してください。

|シナリオ|Link|
|-|-|-|
|Azure App Service|Azure での[スナップショットデバッガー](../debugger/debug-live-azure-applications.md)または[リモートデバッグ ASP.NET](../debugger/remote-debugging-azure.md)|
|Azure VM|[Azure での ASP.NET のリモート デバッグ](../debugger/remote-debugging-azure.md)|
|Azure Service Fabric|[Azure Service Fabric アプリケーションのデバッグ](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)|
|ASP.NET|[リモートデバッグ ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)または[リモートデバッグ ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|C# または Visual Basic|[C# プロジェクトまたは Visual Basic プロジェクトのリモート デバッグ](../debugger/remote-debugging-csharp.md)|
|C++|[C++ Project プロジェクトのリモート デバッグ](../debugger/remote-debugging-cpp.md)|
|ユニバーサル Windows アプリ (UWP)|[リモートコンピューターで UWP アプリを実行する](../debugger/run-windows-store-apps-on-a-remote-machine.md)か[、インストールされているアプリケーションパッケージをデバッグする](../debugger/debug-installed-app-package.md)|

リモートデバッガーをダウンロードしてインストールするだけで、シナリオに関する追加の手順が不要な場合は、この記事の手順に従ってください。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="requirements_msvsmon"></a> 必要条件

[!INCLUDE [remote-debugger-requirements](../debugger/includes/remote-debugger-requirements.md)]

## <a name="fileshare_msvsmon"></a>Optionalファイル共有からリモートデバッガーを実行するには

リモートデバッガー (*msvsmon*) は、Visual Studio Community、Professional、または Enterprise が既にインストールされているコンピューターで見つけることができます。 場合によっては、リモートデバッグをセットアップする最も簡単な方法は、ファイル共有からリモートデバッガー (msvsmon) を実行することです。 使用に関する制限事項については、リモートデバッガーのヘルプページ (リモートデバッガーの**ヘルプ > 使用方法**) を参照してください。

1. 使用している Visual Studio のバージョンと一致するディレクトリで、 *msvsmon*を見つけます。

   ::: moniker range=">=vs-2019"

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end
   ::: moniker range="vs-2017"

   *Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end

2. Visual Studio コンピューターで**リモートデバッガー**フォルダーを共有します。

3. リモートコンピューターで、共有フォルダーから*msvsmon*を実行します。 セットアップの[指示](#bkmk_setup)に従います。

> [!TIP]
> コマンドラインインストールおよびコマンドラインリファレンスについては、Visual Studio がインストールされているコンピューターのコマンドラインで ``msvsmon.exe /?`` を入力して、 *msvsmon*のヘルプページを参照してください (または、リモートデバッガーの [**ヘルプ > 使用状況]** を参照してください)。

## <a name="bkmk_setup"></a> リモート デバッガーのセットアップ

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

### <a name="configure_msvsmon"></a> リモート デバッガーの構成
リモート デバッガーを初めて起動した後、リモート デバッガーの構成の一部を変更できます。

- 他のユーザーがリモートデバッガーに接続するためのアクセス許可を追加する必要がある場合は、 **[ツール > のアクセス許可]** を選択します。 アクセス許可を付与または拒否するには、管理者特権が必要です。

     > [!IMPORTANT]
     > リモートデバッガーは、Visual Studio コンピューターで使用しているユーザーアカウントとは異なるユーザーアカウントで実行できますが、リモートデバッガーのアクセス許可には、別のユーザーアカウントを追加する必要があります。

     または、コマンドラインからリモートデバッガーを起動することもできます。これには、次のように指定します。 **\<ユーザー名 >** パラメーター: **msvsmon/allow \<username@computer>** 。

- 認証モードまたはポート番号を変更する必要がある場合、またはリモートツールのタイムアウト値を指定する場合: **[ツール > オプション]** を選択します。

     既定で使用されるポート番号の一覧については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください。

     > [!WARNING]
     > リモート ツールを認証なしモードで実行することも選択できますが、このモードの使用は避けることを強く推奨します。 このモードで実行した場合、ネットワーク セキュリティはまったく提供されません。 [認証なし] モードは、ネットワークに悪意のあるコードや悪意のあるトラフィックのリスクがないことが確実である場合にのみ選択してください。

## <a name="bkmk_configureService"></a>Optionalリモートデバッガーをサービスとして構成する
ASP.NET およびその他のサーバー環境でのデバッグでは、リモートデバッガーを管理者として実行するか、常に実行する場合は、リモートデバッガーをサービスとして実行する必要があります。

 リモートデバッガーをサービスとして構成する場合は、次の手順を実行します。

1. **リモート デバッガー構成ウィザード** (rdbgwiz.exe) を見つけます (これは、リモートデバッガーとは別のアプリケーションです)。リモートツールをインストールする場合にのみ使用できます。 Visual Studio と共にはインストールされません。

2. 構成ウィザードの実行を開始します。 最初のページが表示されたら、 **[次へ]** をクリックします。

3. **[Visual Studio 2015 リモート デバッガー サービスを実行する]** チェック ボックスをオンにします。

4. ユーザー アカウントの名前とパスワードを追加します。

    **[サービスとしてログオン**] ユーザー権利をこのアカウントに追加する必要がある場合があります (**ローカルセキュリティポリシー** (secpol.msc) を**スタート**ページまたはウィンドウで検索します (または、コマンドプロンプトで「 **secpol.msc** 」と入力します)。 ウィンドウが表示されたら、 **[ユーザー権利の割り当て]** をダブルクリックし、右ペインで **[サービスとしてログオン]** を見つけます。 これをダブルクリックします。 ユーザー アカウントを **[プロパティ]** ウィンドウに追加して **[OK]** をクリックします)。 **[次へ]** をクリックします。

5. リモート ツールが通信するネットワークの種類を選択します。 少なくとも 1 つのネットワークの種類を選択する必要があります。 コンピューターがドメインを介して接続されている場合は、最初の項目を選択する必要があります。 コンピューターがワークグループまたはホーム グループを介して接続されている場合は、2 番目または 3 番目の項目を選択する必要があります。 **[次へ]** をクリックします。

6. サービスを開始できた場合は、「 **Visual Studio リモート デバッガー構成ウィザードは正常に完了しました**」と表示されます。 サービスを開始できなかった場合は、「 **Visual Studio リモート デバッガー構成ウィザードを完了できませんでした**」と表示されます。 このページには、サービスを開始するために従う必要があるヒントもいくつか提供されます。

7. **[完了]** をクリックします。

   この時点で、リモート デバッガーはサービスとして実行されています。 これを確認するには、 **[コントロール パネル] > [サービス]** に移動して **[Visual Studio 2015 リモート デバッガー]** を探します。

   リモート デバッガー サービスは、 **[コントロール パネル] > [サービス]** で停止してから開始することができます。

## <a name="set-up-debugging-with-remote-symbols"></a>リモートシンボルを使用したデバッグの設定

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>参照

- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモートの IIS コンピューターでのリモートデバッグ ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)