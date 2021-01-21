---
title: C++ プロジェクトをリモート デバッグする | Microsoft Docs
description: 次の手順に従い、リモート コンピューターから Visual Studio C++ アプリケーションをデバッグする方法について説明します。
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
ms.openlocfilehash: a8d3b578e62b917a7553b42a04e53062c406c4fd
ms.sourcegitcommit: 105e7b5a486262bc92939980383ceee068098a11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/30/2020
ms.locfileid: "97815803"
---
# <a name="remote-debugging-a-c-project-in-visual-studio"></a>Visual Studio での C++ プロジェクトのリモート デバッグ
別のコンピューター上の Visual Studio アプリケーションをデバッグするには、アプリを配置したコンピューターにリモート ツールをインストールして実行し、Visual Studio からリモート コンピューターに接続するようにプロジェクトを構成してから、アプリを配置して実行します。

![リモート デバッガーのコンポーネント](../debugger/media/remote-debugger-client-apps.png "Remote_debugger_components")

ユニバーサル Windows アプリ (UWP) のリモート デバッグの詳細については、[インストールされているアプリ パッケージのデバッグ](debug-installed-app-package.md)に関するページを参照してください。

## <a name="requirements"></a>必要条件

リモート デバッガーは、Windows 7 以降 (Phone を除く) および Windows Server 2008 Service Pack 2 以降でサポートされています。 詳細な要件の一覧については、「[要件](../debugger/remote-debugging.md#requirements_msvsmon)」を参照してください。

> [!NOTE]
> プロキシ経由で接続された 2 台のコンピューター間のデバッグはサポートされていません。 待機時間の長い接続や低帯域幅の接続 (ダイヤルアップ インターネットなど)、または国をまたぐインターネット経由のデバッグは推奨されません。これらは、障害が発生するか、または過度に低速になる可能性があります。

## <a name="download-and-install-the-remote-tools"></a>リモート ツールのダウンロードおよびインストール

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

> [!TIP]
> 場合によっては、ファイル共有からリモート デバッガーを実行するのが最も効率的な場合があります。 詳細については、[ファイル共有からのリモート デバッガーの実行](../debugger/remote-debugging.md#fileshare_msvsmon)に関するページを参照してください。

## <a name="set-up-the-remote-debugger"></a><a name="BKMK_setup"></a> リモート デバッガーのセットアップ

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> 追加のユーザーのアクセス許可を追加し、認証モード、またはリモート デバッガーのポート番号を変更する必要がある場合は、「[リモート デバッガーを構成する](../debugger/remote-debugging.md#configure_msvsmon)」を参照してください。

## <a name="remote-debug-a-c-project"></a><a name="remote_cplusplus"></a> C++ Project プロジェクトをリモート デバッグする
 次の手順では、プロジェクトの名前とパスは C:\remotetemp\MyMfc で、リモート コンピューターの名前は **MJO-DL** です。

1. **mymfc** という名前の MFC アプリケーションを作成します。

2. ブレークポイントを、アプリケーション内の達しやすい任意の箇所 (たとえば、`CMainFrame::OnCreate` の開始時の **MainFrm.cpp**) に設定します。

3. ソリューション エクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。 **[デバッグ]** タブを開きます。

4. **[起動するデバッガー]** を **[リモート Windows デバッガー]** に設定します。

    ![Visual Studio ソリューション エクスプローラーのプロパティの [デバッグ] タブのスクリーンショット。 [起動するデバッガー] プロパティが [リモート Windows デバッガー] に設定されています。](../debugger/media/remotedebuggingcplus.png)

5. プロパティに次の変更を適用します。

   |設定|[値]|
   |-|-|
   |リモート コマンド|C:\remotetemp\mymfc.exe|
   |作業ディレクトリ|C:\remotetemp|
   |リモート サーバー名|MJO-DL:<*ポート番号*>|
   |Connection|Windows 認証を使用したリモート接続|
   |[デバッガーのタイプ]|ネイティブのみ|
   |[配置ディレクトリ]|C:\remotetemp|
   |[配置する追加ファイル]|C:\data\mymfcdata.txt|

    追加のファイルを配置する場合は (オプション)、フォルダーが両方のコンピューターに存在している必要があります。

6. ソリューション エクスプローラーで、ソリューションを右クリックして **[構成マネージャー]** を選択します。

7. **[デバッグ]** 構成の **[配置]** チェック ボックスをオンにします。

    ![Visual Studio ソリューション エクスプローラーの構成マネージャーのスクリーンショット。 [デバッグ] 構成が選択されています。[配置] がオンになっています。](../debugger/media/remotedebugcplusdeploy.png)

8. デバッグを開始します ( **[デバッグ] > [デバッグの開始]** 、または **F5** キー)。

9. 実行可能ファイルが、リモート コンピューターに自動的に配置されます。

10. メッセージが表示されたら、リモート コンピューターに接続するためのネットワーク資格情報を入力します。

     必要な資格情報は、ネットワークのセキュリティ構成に固有です。 たとえば、ドメイン コンピューターでは、セキュリティ証明書を選択するか、ドメイン名とパスワードを入力します。 ドメイン以外のコンピューターでは、コンピューター名と有効なユーザー アカウント名 (<strong>MJO-DL\name@something.com</strong> など) および正しいパスワードなどを入力します。

11. Visual Studio コンピューターで、実行がブレークポイントで停止したことを確認できるはずです。

    > [!TIP]
    > また、これらのファイルは別の手順でも配置できます。 **ソリューション エクスプローラー** で、 **[mymfc]** ノードを右クリックして **[配置]** を選択します。

    アプリケーションで必要なコード以外のファイルがある場合は、 **[リモート Windows デバッガー]** ページの **[追加の配置ファイル]** で指定できます。

    または、ファイルをプロジェクトに追加し、各ファイルの **[プロパティ]** ページで **[コンテンツ]** プロパティを **[はい]** に設定します。 これらのファイルは、 **[リモート Windows デバッガー]** ページで指定した **[配置ディレクトリ]** にコピーされます。 また、 **[配置ディレクトリ]** のサブフォルダーにファイルをコピーする必要がある場合は、 **[項目の種類]** を **[ファイルのコピー]** に変更し、そこで追加のプロパティを指定できます。

## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>関連項目
- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [リモート デバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)
- [リモートの IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)