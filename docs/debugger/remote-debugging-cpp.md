---
title: C++ プロジェクトのリモート デバッグ |マイクロソフトドキュメント
ms.custom: remotedebugging
ms.date: 08/14/2018
ms.topic: conceptual
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 8b8eca0d-122f-4eda-848a-cf0945f207d0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 0173ed557afa47129e0cc92d9ef9b2d94a7b198f
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301087"
---
# <a name="remote-debugging-a-c-project-in-visual-studio"></a>Visual Studio での C++ プロジェクトのリモート デバッグ
別のコンピューターで Visual Studio アプリケーションをデバッグするには、インストールし、アプリを配置するコンピューター上のリモート ツールを実行し、Visual Studio からリモート コンピューターに接続するプロジェクトを構成し、アプリを展開して実行します。

![リモート デバッガー コンポーネント](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

ユニバーサル Windows アプリ (UWP) のリモート デバッグの詳細については、「[インストールされているアプリ パッケージのデバッグ](debug-installed-app-package.md)」を参照してください。

## <a name="requirements"></a>必要条件

リモート デバッガーは、Windows Server 2008 サービス パック 2 以降の Windows 7 以降 (電話ではない) および Windows Server のバージョンでサポートされています。 要件の完全なリストについては、[要件](../debugger/remote-debugging.md#requirements_msvsmon)を参照してください。

> [!NOTE]
> プロキシ経由で接続された 2 台のコンピュータ間のデバッグはサポートされていません。 ダイヤルアップ インターネットやインターネット経由など、遅延が長い接続や帯域幅の低い接続を介したデバッグは推奨されず、失敗したり、許容できないほど遅くなる可能性があります。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> シナリオによっては、ファイル共有からリモート デバッガーを実行するのが最も効率的な場合があります。 詳細については、「[ファイル共有からリモート デバッガーを実行する](../debugger/remote-debugging.md#fileshare_msvsmon)」を参照してください。

## <a name="set-up-the-remote-debugger"></a><a name="BKMK_setup"></a>リモート デバッガーを設定する

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> リモート デバッガーの認証モードまたはポート番号を変更する、追加のユーザーのアクセス許可を追加する必要がある場合は、[リモート デバッガーの構成を](../debugger/remote-debugging.md#configure_msvsmon)参照してください。

## <a name="remote-debug-a-c-project"></a><a name="remote_cplusplus"></a>C++ プロジェクトのリモート デバッグ
 次の手順では、プロジェクトの名前とパスは C:\remotetemp\MyMfc で、リモート コンピュータの名前は**MJO-DL**です。

1. **mymfc** という名前の MFC アプリケーションを作成します。

2. ブレークポイントを、アプリケーション内の達しやすい任意の箇所 (たとえば、`CMainFrame::OnCreate` の開始時の **MainFrm.cpp**) に設定します。

3. ソリューション エクスプローラで、プロジェクトを右クリックし、[**プロパティ]** を選択します。 **[デバッグ]** タブを開きます。

4. **[起動するデバッガー]** を **[リモート Windows デバッガー]** に設定します。

    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")

5. プロパティに次の変更を適用します。

   |設定|Value|
   |-|-|
   |リモート コマンド|C:\remotetemp\mymfc.exe|
   |作業ディレクトリ|C:\remotetemp|
   |リモート サーバー名|MJO DL:*ポート番号*|
   |Connection|Windows 認証を使用したリモート接続|
   |[デバッガーのタイプ]|ネイティブのみ|
   |[配置ディレクトリ]|C:\remotetemp|
   |[配置する追加ファイル]|C:\data\mymfcdata.txt|

    追加のファイルを展開する場合 (オプション)、フォルダーは両方のコンピューターに存在する必要があります。

6. ソリューション エクスプローラーでソリューションを右クリックし、[**構成マネージャー**] を選択します。

7. **[デバッグ]** 構成の **[配置]** チェック ボックスをオンにします。

    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")

8. デバッグを開始します (**[デバッグ] > [デバッグの開始]**、または **F5** キー)。

9. 実行可能ファイルが、リモート コンピューターに自動的に配置されます。

10. プロンプトが表示されたら、リモート コンピューターに接続するためのネットワーク資格情報を入力します。

     必要な資格情報は、ネットワークのセキュリティ構成に固有です。 たとえば、ドメイン コンピューターで、セキュリティ証明書を選択したり、ドメイン名とパスワードを入力したりできます。 ドメイン以外のマシンでは、マシン名と有効なユーザー アカウント名<strong>MJO-DL\name@something.com</strong>を入力できます。

11. Visual Studio コンピューターで、実行がブレークポイントで停止したことを確認できるはずです。

    > [!TIP]
    > また、これらのファイルは別の手順でも配置できます。 **ソリューション エクスプローラー**で、**[mymfc]** ノードを右クリックして **[配置]** を選択します。

    アプリケーションで必要なコード以外のファイルがある場合は、[**リモート Windows デバッガー** ] ページの **[追加ファイルを配置する]** で指定できます。

    または、プロジェクトにファイルを含め、各ファイルの **[プロパティ**] ページで**Content**プロパティを **[はい**] に設定することもできます。 これらのファイルは、[**リモート Windows デバッガ**] ページで指定した**展開ディレクトリ**にコピーされます。 また、**ファイルの種類**を **[ファイルのコピー]** に変更し、ファイルを**配置ディレクトリ**のサブフォルダにコピーする必要がある場合は、追加のプロパティを指定することもできます。

## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [まずデバッガを見てください](../debugger/debugger-feature-tour.md)
- [リモート デバッグ用に Windows ファイアウォールを構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモートの IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)