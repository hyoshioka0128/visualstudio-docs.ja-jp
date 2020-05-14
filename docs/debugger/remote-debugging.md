---
title: リモート デバッグ |マイクロソフトドキュメント
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
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301057"
---
# <a name="remote-debugging"></a>リモート デバッグ
別のコンピューターに配置されている Visual Studio アプリケーションをデバッグすることができます。 このデバッグを行うには、Visual Studio リモート デバッガーを使用します。

リモート デバッグの詳細な手順については、次のトピックを参照してください。

|シナリオ|Link|
|-|-|-|
|Azure App Service|[Azure 上のスナップショット デバッガー](../debugger/debug-live-azure-applications.md)または[リモート デバッグ ASP.NET](../debugger/remote-debugging-azure.md)|
|Azure VM|[Azure での ASP.NET のリモート デバッグ](../debugger/remote-debugging-azure.md)|
|Azure Service Fabric|[Azure サービス ファブリック アプリケーションのデバッグ](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)|
|ASP.NET|[リモート デバッグ ASP.NET コア](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)または[リモート デバッグ ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|C# または Visual Basic|[C# プロジェクトまたは Visual Basic プロジェクトのリモート デバッグ](../debugger/remote-debugging-csharp.md)|
|C++|[C++ プロジェクトのリモート デバッグ](../debugger/remote-debugging-cpp.md)|
|ユニバーサル ウィンドウ アプリ (UWP)|[リモート コンピューターで UWP アプリを実行するか、](../debugger/run-windows-store-apps-on-a-remote-machine.md)[インストールされているアプリ パッケージをデバッグする](../debugger/debug-installed-app-package.md)|

リモート デバッガーをダウンロードしてインストールするだけで、シナリオに関する追加の手順が必要ない場合は、この記事の手順に従います。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="requirements"></a><a name="requirements_msvsmon"></a>要件

[!INCLUDE [remote-debugger-requirements](../debugger/includes/remote-debugger-requirements.md)]

## <a name="optional-to-run-the-remote-debugger-from-a-file-share"></a><a name="fileshare_msvsmon"></a>(オプション)ファイル共有からリモート デバッガーを実行するには

リモート デバッガー (*msvsmon.exe*) は、Visual Studio コミュニティ、プロフェッショナル、またはエンタープライズが既にインストールされているコンピューター上にあります。 一部のシナリオでは、リモート デバッグをセットアップする最も簡単な方法は、ファイル共有からリモート デバッガー (msvsmon.exe) を実行することです。 使用制限については、リモート デバッガーのヘルプ ページ (リモート デバッガーの**使用>ヘルプ**) を参照してください。

1. 使用しているバージョンの Visual Studio と一致するディレクトリで*msvsmon.exe*を検索します。

   ::: moniker range=">=vs-2019"

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end
   ::: moniker range="vs-2017"

   *Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end

2. Visual Studio コンピューターで**リモート デバッガー**フォルダーを共有します。

3. リモート コンピュータで、共有フォルダから*msvsmon.exe*を実行します。 [セットアップ手順](#bkmk_setup)に従います。

> [!TIP]
> コマンド ラインのインストールとコマンド ラインリファレンスについては、Visual Studio がインストールされているコンピューターの``msvsmon.exe /?``コマンド ラインに入力して*msvsmon.exe*のヘルプ ページを参照してください (またはリモート デバッガーで**の使用>ヘルプ**に移動します)。

## <a name="set-up-the-remote-debugger"></a><a name="bkmk_setup"></a>リモート デバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

### <a name="configure-the-remote-debugger"></a><a name="configure_msvsmon"></a>リモート デバッガーを構成する
リモート デバッガーを初めて起動した後、リモート デバッガーの構成の一部を変更できます。

- 他のユーザーがリモート デバッガに接続するためのアクセス許可を追加する必要がある場合は、[**ツール] >アクセス許可**を選択します。 アクセス許可を付与または拒否するには、管理者特権が必要です。

     > [!IMPORTANT]
     > Visual Studio コンピューターで使用しているユーザー アカウントとは異なるユーザー アカウントでリモート デバッガーを実行できますが、リモート デバッガーのアクセス許可に別のユーザー アカウントを追加する必要があります。

     または、コマンド ラインから **、/allow \<username>** パラメータ**msvsmon \< username@computer /allow>** を使用してリモート デバッガを起動することもできます。

- 認証モードまたはポート番号を変更する必要がある場合、またはリモート ツールのタイムアウト値を指定する必要がある場合は、[**ツール > オプション**] を選択します。

     既定で使用されるポート番号の一覧については、「[リモート デバッガー ポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください。

     > [!WARNING]
     > リモート ツールを認証なしモードで実行することも選択できますが、このモードの使用は避けることを強く推奨します。 このモードで実行した場合、ネットワーク セキュリティはまったく提供されません。 [認証なし] モードは、ネットワークに悪意のあるコードや悪意のあるトラフィックのリスクがないことが確実である場合にのみ選択してください。

## <a name="optional-configure-the-remote-debugger-as-a-service"></a><a name="bkmk_configureService"></a>(オプション)リモート デバッガーをサービスとして構成する
ASP.NETおよびその他のサーバー環境でデバッグを行うには、リモート デバッガーを管理者として実行するか、常に実行する場合は、リモート デバッガーをサービスとして実行する必要があります。

 リモート デバッガーをサービスとして構成する場合は、次の手順を実行します。

1. **リモート デバッガー構成ウィザード** (rdbgwiz.exe) を見つけます (これはリモート デバッガーとは別のアプリケーションです)。リモート ツールをインストールする場合にのみ使用できます。 Visual Studio と共にはインストールされません。

2. 構成ウィザードの実行を開始します。 最初のページが表示されたら、 **[次へ]** をクリックします。

3. **[Visual Studio 2015 リモート デバッガー サービスを実行する]** チェック ボックスをオンにします。

4. ユーザー アカウントの名前とパスワードを追加します。

    サービス**としてログオン**ユーザー権利をこのアカウントに追加する必要があります (**スタート**ページまたはウィンドウで**ローカル セキュリティ ポリシー**の検索 (secpol.msc) (またはコマンド プロンプトで**secpol**と入力) します。 ウィンドウが表示されたら、 **[ユーザー権利の割り当て]** をダブルクリックし、右ペインで **[サービスとしてログオン]** を見つけます。 これをダブルクリックします。 ユーザー アカウントを **[プロパティ]** ウィンドウに追加して **[OK]** をクリックします)。 **[次へ]** をクリックします。

5. リモート ツールが通信するネットワークの種類を選択します。 少なくとも 1 つのネットワークの種類を選択する必要があります。 コンピューターがドメインを介して接続されている場合は、最初の項目を選択する必要があります。 コンピューターがワークグループまたはホーム グループを介して接続されている場合は、2 番目または 3 番目の項目を選択する必要があります。 **[次へ]** をクリックします。

6. サービスを開始できた場合は、「 **Visual Studio リモート デバッガー構成ウィザードは正常に完了しました**」と表示されます。 サービスを開始できなかった場合は、「 **Visual Studio リモート デバッガー構成ウィザードを完了できませんでした**」と表示されます。 このページには、サービスを開始するために従う必要があるヒントもいくつか提供されます。

7. **[完了]** をクリックします。

   この時点で、リモート デバッガーはサービスとして実行されています。 これを確認するには、**コントロール パネル> サービス**に移動し **、Visual Studio 2015 リモート デバッガー**を探します。

   リモート デバッガー サービスは、**コントロール パネルの [> サービス**] から停止および開始できます。

## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>関連項目

- [まずデバッガを見てください](../debugger/debugger-feature-tour.md)
- [リモート デバッグ用に Windows ファイアウォールを構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモート IIS コンピュータ上のリモート デバッグ ASP.NET コア](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)