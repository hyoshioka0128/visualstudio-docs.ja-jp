---
title: Windows での Docker クライアント エラーのトラブルシューティング | Microsoft Docs
description: Visual Studio を使用して、Windows 上で Web アプリを作成し、Docker にデプロイする際に発生する問題のトラブルシューティングを行います。
ms.technology: vs-azure
author: ghogen
manager: jillfra
ms.custom: seodec18
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.devlang: dotnet
ms.topic: conceptual
ms.workload: multiple
ms.date: 01/27/2020
ms.author: ghogen
ms.openlocfilehash: d8aa3028a12bcfb49f2663b2bea688baf14fd7f2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77027283"
---
# <a name="troubleshoot-visual-studio-development-with-docker"></a>Docker を使用した Visual Studio 開発のトラブルシューティング

Visual Studio コンテナー ツールを使用する際、アプリケーションのビルドまたはデバッグしている間に問題が発生する可能性があります。 一般的なトラブルシューティング手順のいくつかを以下に示します。

## <a name="volume-sharing-is-not-enabled-enable-volume-sharing-in-the-docker-ce-for-windows-settings--linux-containers-only"></a>ボリューム共有が有効にならない。 Docker CE for Windows の設定でのボリューム共有の有効化 (Linux コンテナーのみ)

この問題を解決するには、次の操作を行います。

1. 通知領域で **[Windows 用の Docker]** を右クリックし、 **[設定]** を選択します。
1. **[Shared Drives]\(共有ドライブ\)** を選択し、システム ドライブと共に、プロジェクトが存在するドライブを共有します。

> [!NOTE]
> ファイルが共有されているように見える場合は、ダイアログ下部の [資格情報のリセット] リンクをクリックしてボリューム共有を再度有効にすることが必要な場合があります。 資格情報をリセットした後で続行するには、Visual Studio の再起動が必要な場合があります。

![共有ドライブ](media/troubleshooting-docker-errors/shareddrives.png)

> [!TIP]
> Visual Studio 2017 バージョン 15.6 以降の Visual Studio バージョンでは、**共有ドライブ**が構成されていない場合、プロンプトが表示されます。

### <a name="container-type"></a>コンテナーの種類

プロジェクトに Docker サポートを追加する場合は、Windows または Linux のいずれかのコンテナーを選択します。 Docker ホストが同じコンテナーの種類を実行している必要があります。 実行中の Docker インスタンスでコンテナーの種類を変更するには、システム トレイの Docker アイコンを右クリックして、 **[Switch to Windows containers...]\(Windows コンテナーに切り替える...\)** または **[Switch to Linux containers...]\(Linux コンテナーに切り替える...\)** を選択します。

## <a name="unable-to-start-debugging"></a>デバッグを開始できない

理由の 1 つとして、ユーザー プロファイル フォルダーに古いデバッグ コンポーネントが残っていることが考えられます。 次のコマンドを実行してこれらのフォルダーを削除し、次回のデバッグ セッションで最新のデバッグ コンポーネントがダウンロードされるようにしてください。

- del %userprofile%\vsdbg
- del %userprofile%\onecoremsvsmon

## <a name="errors-specific-to-networking-when-debugging-your-application"></a>アプリケーションのデバッグ時のネットワークに固有のエラー

[コンテナー ホスト ネットワークのクリーンアップ](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/master/windows-server-container-tools/CleanupContainerHostNetworking)に関するページでダウンロードできるスクリプトを実行してみてください。このスクリプトにより、ホスト コンピューター上のネットワーク関連のコンポーネントが更新されます。

## <a name="mounts-denied"></a>マウントが拒否される

MacOS 用の Docker を使用している場合、フォルダー /usr/local/share/dotnet/sdk/NuGetFallbackFolder を参照するとエラーが発生する可能性があります。 Docker で [ファイル共有] タブにフォルダーを追加する

## <a name="docker-users-group"></a>Docker users グループ

コンテナーを使用するときに、Visual Studio で次のエラーが発生する場合があります。

```
The current user must be in the 'docker-users' group to use Docker Desktop. 
Add yourself to the 'docker-users' group and then log out of Windows.
```

Docker コンテナーを使用する許可を得るには、'docker-users' グループのメンバーである必要があります。  Windows 10 で自分自身をグループに追加するには、次の手順を行います。

1. スタート メニューから、 **[コンピューターの管理]** を開きます。
1. **[ローカル ユーザーとグループ]** を展開し、 **[グループ]** を選択します。
1. **docker-users** グループを検索し、 **[グループに追加]** を右クリックして選択します。
1. お使いのユーザー アカウントまたはアカウントを追加します。
1. いったんサインアウトしてからもう一度サインインして、変更した内容を有効にします。

また、管理者の `net localgroup` コマンド プロンプトでコマンドを使用して、ユーザーを特定のグループに追加することもできます。

```cmd
net localgroup docker-users DOMAIN\username /add
```

PowerShell では、[Add-LocalGroupMember](/powershell/module/microsoft.powershell.localaccounts/add-localgroupmember) 関数を使用します。

## <a name="low-disk-space"></a>ディスク領域不足

Docker では既定で、 *%ProgramData%/Docker/* フォルダーにイメージが格納されます。このフォルダーは通常、システム ドライブ上にあり、*C:\ProgramData\Docker\* となります。 システム ドライブの大切な領域をイメージで占有してしまわないよう、イメージ フォルダーの場所を変更できます。  タスク バーの Docker アイコンから Docker 設定を開き、 **[デーモン]** を選択し、 **[基本]** を **[詳細]** に切り替えます。 編集ウィンドウで `graph` プロパティ設定を追加し、Docker イメージに任意の場所を指定します。

```json
    "graph": "D:\\mypath\\images"
```

![Docker イメージの場所設定のスクリーンショット](media/troubleshooting-docker-errors/docker-settings-image-location.png)

**[適用]** をクリックし、Docker を再起動します。 以上の手順で *%ProgramData%\docker\config\daemon.json* にある設定ファイルが変更されます。 以前に作成したイメージが移動されることはありません。

## <a name="microsoftdockertools-github-repo"></a>Microsoft/DockerTools GitHub リポジトリ

その他の問題が発生した場合は、[Microsoft/DockerTools](https://github.com/microsoft/dockertools/issues) の問題に関するページをご覧ください。