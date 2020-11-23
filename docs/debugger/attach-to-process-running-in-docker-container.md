---
title: Docker コンテナー上で実行されているプロセスにアタッチする
description: Visual Studio を使用して Docker コンテナーで実行しているアプリをデバッグする方法について説明します
ms.date: 11/11/2020
ms.topic: conceptual
helpviewer_keywords:
- debugging, linux Docker container
- debugging, Docker container
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 5b32b402e2bbf85cf5c028ec2dc94821ec463644
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674790"
---
# <a name="attach-to-a-process-running-on-a-docker-container"></a>Docker コンテナー上で実行されているプロセスにアタッチする 

Visual Studio を使用して、Windows Docker コンテナーまたは Linux .NET Core Docker コンテナーで実行されているアプリをデバッグできます。

## <a name="attach-to-a-process-running-on-a-linux-docker-container"></a> Linux Docker コンテナー上で実行されているプロセスにアタッチする

**[プロセスにアタッチ]** ダイアログ ボックスを使用して、ローカル コンピューターまたはリモート マシン上の Linux .NET Core Docker コンテナーで実行されているプロセスに Visual Studio デバッガーをアタッチできます。

> [!IMPORTANT]
> この機能を使用するには、.NET Core Cross-Platform Development ワークロードをインストールする必要があります。また、ソース コードへのローカル アクセス権を持っている必要があります。

**Linux Docker コンテナー内の実行中のプロセスにアタッチするには:**

1. Visual Studio で、 **[デバッグ] > [プロセスにアタッチ] (CTRL + ALT + P キー)** を選択して、 **[プロセスにアタッチ]** ダイアログ ボックスを開きます。

![[プロセスにアタッチ] メニュー](../debugger/media/attach-process-menu.png "Attach_To_Process_Menu")

2. **[接続の種類]** を **[Docker (Linux コンテナー)]** に設定します。
3. **[Docker コンテナーの選択]** ダイアログボックスを使用して **[検索]** を選択し、 **[接続先]** を設定します。

    Docker コンテナー プロセスは、ローカルでもリモートでもデバッグできます。

    **Docker コンテナー プロセスをローカルでデバッグするには:**
    1. **[Docker CLI ホスト]** を **[ローカル コンピューター]** に設定します。
    1. アタッチする実行中のコンテナーをリストから選択し、 **[OK]** をクリックします。

    ![[Docker コンテナーの選択] メニュー](../debugger/media/select-docker-container.png "Select_Docker_Container_Menu")

    **B.Docker コンテナー プロセスをリモートでデバッグするには:**

    > [!NOTE]
    > Docker コンテナーで実行中のプロセスにリモート接続するには、2 つのオプションがあります。 SSH を使用するという 1 つ目のオプションは、ローカル コンピューターに Docker ツールがインストールされていない場合に最適です。  ローカルに Docker ツールをインストールしていて、リモートの要求を受け入れるように構成されている Docker デーモンがある場合は、2 つ目のオプションである Docker デーモンの使用を試してください。

    1. "**_SSH を使用してリモート マシンに接続するには:_* _"
        1. _ *[追加]* * を選択してリモート システムに接続します。<br/>
        ![リモート システムに接続する](../debugger/media/connect-remote-system.png "リモート システムに接続する")
        1. SSH またはデーモンに正常に接続した後にアタッチする実行中のコンテナーを選択し、 **[OK]** をクリックします。

    1. "**_[Docker デーモン](https://docs.docker.com/engine/reference/commandline/dockerd/)を介してプロセスを実行しているリモート コンテナーにターゲットを設定するには_* _"
        1. _ *[Docker ホスト (省略可能)]* * でデーモンのアドレス (つまり、TCP、IP など) を指定し、更新リンクをクリックします。
        1. デーモンに正常に接続した後にアタッチする実行中のコンテナーを選択し、 **[OK]** をクリックします。

4. Visual Studio で **[使用可能なプロセス]** リストから対応するコンテナー プロセスを選択し、 **[アタッチ]** を選択して C# のデバッグを開始します。

    ![入力された Docker の [アタッチ] メニュー](../debugger/media/docker-attach-complete.png "入力された Linux Docker の [アタッチ] メニュー")

## <a name="attach-to-a-process-running-on-a-windows-docker-container"></a> Windows Docker コンテナー上で実行されているプロセスにアタッチする

**[プロセスにアタッチ]** ダイアログ ボックスを使用して、ローカル コンピューター上の Windows Docker コンテナーで実行されているプロセスに Visual Studio デバッガーをアタッチできます。

> [!IMPORTANT]
> この機能を .NET Core プロセスで使用するには、.NET Core Cross-Platform Development ワークロードをインストールする必要があります。また、ソース コードへのローカル アクセス権を持っている必要があります。

**Windows Docker コンテナーで実行中のプロセスにアタッチするには:**

1. Visual Studio で、 **[デバッグ] > [プロセスにアタッチ]** (**CTRL + ALT + P** キー) を選択して、 **[プロセスにアタッチ]** ダイアログ ボックスを開きます。

   ![[プロセスにアタッチ] メニュー](../debugger/media/attach-process-menu-docker-windows.png "Attach_To_Process_Menu")

2. **[接続の種類]** を **[Docker (Windows コンテナー)]** に設定します。
3. **[Docker コンテナーの選択]** ダイアログボックスを使用して **[検索]** を選択し、 **[接続先]** を設定します。

    > [!IMPORTANT]
    > ターゲット プロセスは、それが実行されている Docker Windows コンテナーと同じプロセッサ アーキテクチャを持つ必要があります。

   現在、SSH 経由でターゲットをリモート コンテナーに設定することはできません。Docker デーモンを使用して実行する必要があります。

    "**_[Docker デーモン](https://docs.docker.com/engine/reference/commandline/dockerd/)を介してプロセスを実行しているリモート コンテナーにターゲットを設定するには_* _"
    1. _ *[Docker ホスト (省略可能)]* * でデーモンのアドレス (つまり、TCP、IP など) を指定し、更新リンクをクリックします。

    1. デーモンに正常に接続した後にアタッチする実行中のコンテナーを選択し、[OK] を選択します。

4. **[使用可能なプロセス]** リストから対応するコンテナー プロセスを選択し、 **[アタッチ]** を選択して C# のデバッグを開始します。

    ![入力された Docker の [アタッチ] メニュー](../debugger/media/docker-attach-complete-windows.png "入力された Windows Docker の [アタッチ] メニュー")

5.  Visual Studio で [使用可能なプロセス] リストから対応するコンテナー プロセスを選択し、 **[アタッチ]** を選択して C# のデバッグを開始します。