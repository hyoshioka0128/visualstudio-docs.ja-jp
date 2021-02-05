---
title: Linux 上で .NET Core をデバッグする
description: プロセスにアタッチして Secure Shell (SSH) を使用して Linux 上で .NET Core をデバッグします。 デバッグ用にアプリを準備します。 アプリをビルドしてデプロイします。 デバッガーをアタッチします。
ms.custom: SEO-VS-2020
ms.date: 02/26/2020
ms.topic: conceptual
helpviewer_keywords:
- remote debugging, linux
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 599ebe86867e78d17029b2787b9f35b6755c3040
ms.sourcegitcommit: 586369f5aa61d4a0330802f718f0ceaa55d7e9c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99224354"
---
# <a name="debug-net-core-on-linux-using-ssh-by-attaching-to-a-process"></a>プロセスにアタッチして SSH を使用して Linux 上で .NET Core をデバッグする

Visual Studio 2017 以降では、ローカルまたはリモートの Linux 配置で実行されている .NET Core プロセスに SSH 経由でアタッチできます。 この記事では、デバッグのセットアップ方法とデバッグ方法について説明します。 Docker コンテナーを使用したデバッグ シナリオについては、代わりに「[Docker コンテナー上で実行されているプロセスにアタッチする](../debugger/attach-to-process-running-in-docker-container.md)」と[コンテナー ツール](../containers/edit-and-refresh.md)に関する記事を参照してください。 WSL 2 で Linux を Visual Studio からデバッグするには (プロセスにアタッチしない)、「[Visual Studio を使用して WSL 2 で .NET Core アプリをデバッグする](../debugger/debug-dotnet-core-in-wsl-2.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

- Visual Studio コンピューターでは、**ASP.NET と Web 開発** ワークロードまたは **.NET Core クロスプラットフォーム開発** ワークロードのいずれかをインストールする必要があります。

- Linux サーバーでは、SSH サーバーをインストールする必要があります。curl または wget で解凍してインストールします。 たとえば、Ubuntu では、以下を実行して行うことができます。

  ``` cmd
  sudo apt-get install openssh-server unzip curl
  ```

- Linux サーバーで、[Linux に .NET ランタイムをインストール](/dotnet/core/install/linux)し、使用する Linux ディストリビューション (Ubuntu など) に一致するページを探します。 .NET SDK は必要ありません。

- 包括的な ASP.NET Core の手順については、「[Nginx 搭載の Linux で ASP.NET Core をホストする](/aspnet/core/host-and-deploy/linux-nginx)」と「[Apache 搭載の Linux で ASP.NET Core をホストする](/aspnet/core/host-and-deploy/linux-apache)」を参照してください。

## <a name="prepare-your-application-for-debugging"></a>デバッグ用にアプリケーションを準備する

デバッグ用にアプリケーションを準備するには:

- アプリケーションをビルドするときに、デバッグ構成の使用を検討します。 デバッグ コンパイルされたコードより、リテール コンパイルされたコード (リリース構成) をデバッグする方が非常に困難です。 リリース構成を使用する必要がある場合は、まず [マイ コードのみ] を無効にします。 この設定を無効にするには、 **[ツール]**  >  **[オプション]**  >  **[デバッグ]** の順に選択し、 **[マイ コードのみを有効にする]** をオフにします。

- [移植可能な PDB](https://github.com/OmniSharp/omnisharp-vscode/wiki/Portable-PDBs) (既定の設定) を生成するようにプロジェクトが構成されていることを確認し、PDB が DLL と同じ場所にあることを確認します。 Visual Studio でこれを構成するには、プロジェクトを右クリックし、 **[プロパティ]**  >  **[ビルド]**  >  **[詳細]**  >  **[デバッグ情報]** を選択します。

## <a name="build-and-deploy-the-application"></a>アプリケーションをビルドしてデプロイする

デバッグする前に、いくつかの方法を使用してアプリを配置できます。 たとえば、次のように操作できます。

- ソースをターゲット コンピューターにコピーし、Linux コンピューター上で ```dotnet build``` を使用してビルドします。

- Windows 上でアプリをビルドし、ビルド成果物を Linux コンピューターに転送します。 (ビルド成果物は、アプリケーション自体、移植可能な PDB、依存する可能性のあるランタイム ライブラリ、および *.deps.json* ファイルで構成されます。)

アプリが配置されたら、アプリケーションを起動します。

## <a name="attach-the-debugger"></a>デバッガーをアタッチします。

アプリケーションが Linux マシン上で実行されている場合は、デバッガーをアタッチする準備ができています。

1. Visual Studio で、 **[デバッグ]**  >  **[プロセスにアタッチ]** と選択します。

1. **[接続の種類]** の一覧で、 **[SSH]** を選択します。

1. **[接続ターゲット]** を、ターゲット コンピュータの IP アドレスまたはホスト名に変更します。

   資格情報をまだ指定していない場合は、パスワードや秘密キー ファイルを入力するように求められます。

   SSH サーバーが実行されているポートを除き、構成するポートの要件はありません。

1. デバッグするプロセスを見つけます。

   コードは、一意のプロセス名または dotnet という名前のプロセスで実行されます。 対象のプロセスを見つけるには、 **[タイトル]** 列を確認します。この列には、プロセスのコマンド ライン引数が表示されます。

   次の例では、SSH トランスポート経由のリモート Linux マシンからのプロセスの一覧が、 **[プロセスにアタッチ]** ダイアログ ボックスに表示されています。

   ![Linux プロセスにアタッチする](media/remote-debug-linux-over-ssh-attach.png)

1. **[アタッチ]** をクリックします。

1. 表示されるダイアログ ボックスで、デバッグするコードの種類を選択します。 **[マネージド (Unix 用 .NET Core)]** を選択します。

1. Visual Studio のデバッグ機能を使用して、アプリをデバッグします。

   次の例では、リモート Linux マシンで実行されているコード内のブレークポイントで Visual Studio デバッガーが停止していることがわかります。

   ![ブレークポイントに到達する](media/remote-debug-linux-over-ssh-hit-breakpoint.png)