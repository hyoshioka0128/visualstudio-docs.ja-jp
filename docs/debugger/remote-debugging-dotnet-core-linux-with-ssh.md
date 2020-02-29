---
title: Linux での .NET Core のリモートデバッグ |Microsoft Docs
ms.date: 02/26/2020
ms.topic: conceptual
helpviewer_keywords:
- remote debugging, linux
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 23bc0fa990a79b1855ec382f42248a0f847c3c9c
ms.sourcegitcommit: 3d64bfb9bf85395357effe054db9a9afaa0be5ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/29/2020
ms.locfileid: "78200867"
---
# <a name="remote-debug-net-core-on-linux-using-ssh"></a>SSH を使用した Linux での .NET Core のリモートデバッグ

Visual Studio 2017 以降、SSH 経由で Linux で実行されている .NET Core プロセスにアタッチできるようになります。 この記事では、デバッグのセットアップ方法とデバッグ方法について説明します。

## <a name="prerequisites"></a>前提条件

Visual Studio コンピューターで、 **ASP.NET と web 開発**のワークロードまたは **.net Core クロスプラットフォームの開発**ワークロードのいずれかをインストールする必要があります。

Linux サーバーでは、curl または wget のいずれかを使用して、SSH サーバーをインストールし、解凍して、インストールする必要があります。 たとえば、Ubuntu では、次のコードを実行してこれを行うことができます。

``` cmd
sudo apt-get install openssh-server unzip curl
```

## <a name="build-and-deploy-the-application"></a>アプリのビルドと配置

デバッグ用にアプリケーションを準備するには:

- アプリケーションをビルドするときは、デバッグ構成の使用を検討してください。 デバッグによってコンパイルされたコードよりも、リテールコンパイルコード (リリース構成) をデバッグするのは非常に困難です。 リリース構成を使用する必要がある場合は、まずマイコードのみを無効にします。 この設定を無効にするには、 **[ツール]**  >  **[デバッグ]**  >  **[オプション]** を選択し、 **[マイコードのみを有効に]** する をオフにします

- プロジェクトが[ポータブル pdb](https://github.com/OmniSharp/omnisharp-vscode/wiki/Portable-PDBs) (既定の設定) を生成するように構成されていることを確認し、PBDS が DLL と同じ場所にあることを確認します。 Visual Studio でこれを構成するには、プロジェクトを右クリックし、 **[プロパティ]**  > [**ビルド** > **詳細** > **デバッグ情報**] の順に選択します。

デバッグする前に、いくつかの方法を使用してアプリを配置できます。 たとえば、次のように操作できます。

- ソースをターゲットコンピューターにコピーし、Linux コンピューター上の ```dotnet build``` でビルドします。

- Windows でアプリをビルドし、ビルドアーティファクトを Linux マシンに転送します。 (ビルド成果物は、アプリケーション自体、依存する可能性のあるランタイムライブラリ、および. *json*ファイルで構成されます)。

## <a name="attach-the-debugger"></a>デバッガーをアタッチする

コンピューターの構成が完了したら、Linux コンピューターでアプリケーションを起動し、デバッガーをアタッチする準備ができていることを確認します。

1. Visual Studio で、**デバッグ** > **プロセスにアタッチ** を選択します。

1. **[接続の種類]** ボックスの一覧で **[SSH]** を選択します。

1. **接続ターゲット**を、ターゲットコンピュータの IP アドレスまたはホスト名に変更します。

1. デバッグするプロセスを見つけます。

   コードは、一意のプロセス名または dotnet という名前のプロセスで実行されます。 目的のプロセスを見つけるには、 **[タイトル]** 列に、プロセスのコマンドライン引数が表示されていることを確認します。

   次の例では、リモート Linux マシンのプロセスの一覧が、 **[プロセスにアタッチ]** ダイアログボックスに表示される SSH トランスポートを介して表示されます。

   ![Linux プロセスにアタッチ](media/remote-debug-linux-over-ssh-attach.png)

1. **[アタッチ]** をクリックします。

1. 表示されるダイアログボックスで、デバッグするコードの種類を選択します。 **[管理 (Unix 用 .Net Core)]** を選択します。

1. Visual Studio のデバッグ機能を使用して、アプリをデバッグします。

   次の例では、リモート Linux マシンで実行されているコード内のブレークポイントで Visual Studio デバッガーが停止していることがわかります。

   ![ブレークポイントに到達する](media/remote-debug-linux-over-ssh-hit-breakpoint.png)