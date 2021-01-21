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
ms.openlocfilehash: f6e2b851057d924353e6e1e9a211fcbb294353c8
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761265"
---
# <a name="attach-to-a-process-running-on-a-docker-container"></a>Docker コンテナー上で実行されているプロセスにアタッチする 

Visual Studio を使用して、Windows Docker コンテナーまたは Linux .NET Core Docker コンテナーで実行されているアプリをデバッグできます。

## <a name="attach-to-a-process-running-on-a-linux-docker-container"></a> Linux Docker コンテナー上で実行されているプロセスにアタッチする

**[プロセスにアタッチ]** ダイアログ ボックスを使用して、ローカル コンピューターまたはリモート マシン上の Linux .NET Core Docker コンテナーで実行されているプロセスに Visual Studio デバッガーをアタッチできます。

> [!IMPORTANT]
> この機能を使用するには、.NET Core Cross-Platform Development ワークロードをインストールする必要があります。また、ソース コードへのローカル アクセス権を持っている必要があります。

**Linux Docker コンテナー内の実行中のプロセスにアタッチするには:**

1. Visual Studio で、 **[デバッグ] > [プロセスにアタッチ] (CTRL + ALT + P キー)** を選択して、 **[プロセスにアタッチ]** ダイアログ ボックスを開きます。

![Docker (Linux コンテナー) の接続の種類が表示されている Visual Studio の [プロセスにアタッチ] ダイアログのスクリーンショット。](../debugger/media/attach-process-menu.png "Attach_To_Process_Menu")

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

    ![Visual Studio の [プロセスにアタッチ] ダイアログのスクリーンショット。[接続の種類] が [Docker (Linux コンテナー)] に設定され、dotnet プロセスが選択されています。](../debugger/media/docker-attach-complete.png "入力された Linux Docker の [アタッチ] メニュー")

## <a name="attach-to-a-process-running-on-a-windows-docker-container"></a> Windows Docker コンテナー上で実行されているプロセスにアタッチする

**[プロセスにアタッチ]** ダイアログ ボックスを使用して、ローカル コンピューター上の Windows Docker コンテナーで実行されているプロセスに Visual Studio デバッガーをアタッチできます。

> [!IMPORTANT]
> この機能を .NET Core プロセスで使用するには、.NET Core Cross-Platform Development ワークロードをインストールする必要があります。また、ソース コードへのローカル アクセス権を持っている必要があります。

**Windows Docker コンテナーで実行中のプロセスにアタッチするには:**

1. Visual Studio で、 **[デバッグ] > [プロセスにアタッチ]** (**CTRL + ALT + P** キー) を選択して、 **[プロセスにアタッチ]** ダイアログ ボックスを開きます。

   ![Visual Studio の [プロセスにアタッチ] ダイアログのスクリーンショット。Docker (Windows コンテナー) の接続の種類が表示されています。](../debugger/media/attach-process-menu-docker-windows.png "Attach_To_Process_Menu")

2. **[接続の種類]** を **[Docker (Windows コンテナー)]** に設定します。
3. **[Docker コンテナーの選択]** ダイアログボックスを使用して **[検索]** を選択し、 **[接続先]** を設定します。

    > [!IMPORTANT]
    > ターゲット プロセスは、それが実行されている Docker Windows コンテナーと同じプロセッサ アーキテクチャを持つ必要があります。

   現在、SSH 経由でターゲットをリモート コンテナーに設定することはできません。Docker デーモンを使用して実行する必要があります。

    "**_[Docker デーモン](https://docs.docker.com/engine/reference/commandline/dockerd/)を介してプロセスを実行しているリモート コンテナーにターゲットを設定するには_* _"
    1. _ *[Docker ホスト (省略可能)]* * でデーモンのアドレス (つまり、TCP、IP など) を指定し、更新リンクをクリックします。

    1. デーモンに正常に接続した後にアタッチする実行中のコンテナーを選択し、[OK] を選択します。

4. **[使用可能なプロセス]** リストから対応するコンテナー プロセスを選択し、 **[アタッチ]** を選択して C# のデバッグを開始します。

    ![Visual Studio の [プロセスにアタッチ] ダイアログのスクリーンショット。[接続の種類] が [Docker (Windows コンテナー)] に設定され、dotnet.exe プロセスが選択されています。](../debugger/media/docker-attach-complete-windows.png "入力された Windows Docker の [アタッチ] メニュー")

5. Visual Studio で [使用可能なプロセス] リストから対応するコンテナー プロセスを選択し、 **[アタッチ]** を選択して C# のデバッグを開始します。