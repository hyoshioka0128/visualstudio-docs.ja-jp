---
title: Visual Studio 2017 の変更
titleSuffix: ''
description: Visual Studio を変更する方法について、ステップ バイ ステップで説明します。
ms.date: 10/12/2020
ms.topic: how-to
ms.custom: contperfq2
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: dad71e4f52350357106ee9a9ef9ce90d18204bfb
ms.sourcegitcommit: 4eb8fe6eb7f1dc639f1d213db05a7a3007e8087e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2020
ms.locfileid: "92157376"
---
# <a name="modify-visual-studio-by-adding-or-removing-workloads-and-components"></a>ワークロードやコンポーネントを追加または削除することで Visual Studio を変更する

::: moniker range="vs-2019"

必要なときに必要なものだけが含まれるように、Visual Studio を変更するのは簡単です。 これを行うには、Visual Studio インストーラー開き、ワークロードとコンポーネントを追加または削除します。

::: moniker-end

::: moniker range="vs-2017"

実行する作業に合わせて Visual Studio をより簡単にパーソナライズできるようになっただけでなく、Visual Studio をより簡単にカスタマイズできるようにもなりました。 これを行うには、新しい Visual Studio インストーラーを開いて、必要な変更を加えます。

::: moniker-end

次にその方法を示します。

>[!IMPORTANT]
>Visual Studio をインストール、更新、または変更するには、管理アクセス許可を持つアカウントでログオンする必要があります。 詳細については、「[ユーザー アクセス許可と Visual Studio](../ide/user-permissions-and-visual-studio.md)」を参照してください。

>[!NOTE]
> 次の手順では、インターネットに接続しているものとします。
>
> 前に作成した Visual Studio の[オフライン インストール](create-an-offline-installation-of-visual-studio.md)を変更する方法について詳しくは、「[Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)」ページと「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」ページの両方をご覧ください。

## <a name="open-the-visual-studio-installer"></a>Visual Studio インストーラーを開く

::: moniker range="vs-2017"

1. コンピューター上で Visual Studio インストーラーを見つけます。

     たとえば、Windows 10 を実行しているコンピューター上で、 **[スタート]** を選択し、 **Visual Studio インストーラー** としてリスト表示される **V** の文字までスクロールします。

     ![Visual Studio インストーラー](media/locate-the-visual-studio-installer.png "Microsoft Visual Studio インストーラーを見つける")

     >[!TIP]
     >一部のコンピューターでは、Visual Studio インストーラーが **Microsoft Visual Studio インストーラー** として **"M"** の項に表示される場合があります。<br/><br/> Visual Studio インストーラーは `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe` にもあります。

1. インストーラーを開いて、 **[変更]** を選択します。

     ![Visual Studio の起動または変更](media/modify-visual-studio.png "Visual Studio 2017 の変更")

     > [!IMPORTANT]
     > 保留中の更新プログラムがある場合、[変更] ボタンは別の場所にあります。 この方法で、更新せずに Visual Studio を変更するならそれができます。 **[詳細]** をクリックして、 **[変更]** を選択します。
     >
     > ![Visual Studio の更新または変更](media/modify-or-update-visual-studio.png "Visual Studio 2017 の更新または変更")

::: moniker-end

::: moniker range="vs-2019"

1. コンピューター上の **Visual Studio インストーラー** を見つけます。

     Windows の [スタート] メニューで "installer" を検索できます。

     ![Visual Studio インストーラー](media/vs-2019/visual-studio-installer.png "Visual Studio インストーラーを検索する")

     > [!NOTE]
     > また、Visual Studio インストーラーは次の場所にもあります。
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    続行する前に、インストーラーの更新が必要な場合があります。 その場合は、画面の指示に従います。

1. インストーラーで、インストールした Visual Studio のエディションを探し、 **[変更]** を選択します。

     ![Visual Studio のエディションを選択し、変更する](media/vs-2019/vs-installer-modify.png "Visual Studio 2019 エディションを選択し、変更する")

     > [!IMPORTANT]
     > 保留中の更新プログラムがある場合、[変更] ボタンは別の場所にあります。 この方法で、必要に応じて、更新せずに Visual Studio を変更することができます。 **[詳細]** を選択して、 **[変更]** を選択します。
     >
     > ![Visual Studio の更新または変更](media/vs-2019/modify-update-visual-studio.png "Visual Studio 2019 の更新または変更")

::: moniker-end

## <a name="modify-workloads"></a>ワークロードの変更

::: moniker range="vs-2017"

 [ワークロード](https://visualstudio.microsoft.com/vs/support/selecting-workloads-visual-studio-2017/)には、使用するプログラミング言語またはプラットフォームに必要な機能が含まれています。 ワークロードを使用することで、必要に応じて、実行する作業に合わせ、Visual Studio を変更できます。

1. Visual Studio インストーラーで、 **[ワークロード]** タブを選択し、目的のワークロードを選択または選択解除します。

    ![Visual Studio 2017 のセットアップ ダイアログ](media/modify-workloads.png "Visual Studio 2019 でのワークロードの選択")

1. 既定の **[ダウンロードしながらインストールする]** オプションをそのまま使用するか、または **[全部ダウンロードしてからインストールする]** オプションを使用するかを選択します。

    ![Visual Studio 2017 のセットアップ オプション](media/vs-2019/vs-installer-choose-install-or-download.png "ダウンロードしながらインストールするか、または最初にダウンロードしてからインストールするかを選択する")

    最初にダウンロードしてからインストールする場合は、[全部ダウンロードしてからインストールする] オプションが便利です。

1. **[変更]** を選択します。

1. 新しいワークロードがインストールされたら、Visual Studio インストーラーで **[起動]** を選択し、Visual Studio を開きます。

::: moniker-end

::: moniker range="vs-2019"

 ワークロードには、使用するプログラミング言語またはプラットフォームに必要な機能が含まれています。 ワークロードを使用することで、必要に応じて、実行する作業に合わせ、Visual Studio を変更できます。

 > [!TIP]
>開発に必要なツールとコンポーネントのバンドルについて詳しくは、「[Visual Studio ワークロード](https://visualstudio.microsoft.com/vs/#workloads)」をご覧ください。

1. Visual Studio インストーラーで、 **[ワークロード]** タブを選択し、目的のワークロードを選択または選択解除します。

    ![Visual Studio 2019 のセットアップ ダイアログ](media/vs-2019/vs-installer-modify-workloads.png "Visual Studio 2019 でのワークロードの選択")

1. 既定の **[ダウンロードしながらインストールする]** オプションをそのまま使用するか、または **[全部ダウンロードしてからインストールする]** オプションを使用するかを選択します。

    ![Visual Studio 2019 のセットアップ オプション](media/vs-2019/vs-installer-choose-install-or-download.png "ダウンロードしながらインストールするか、または最初にダウンロードしてからインストールするかを選択する")

    最初にダウンロードしてからインストールする場合は、[全部ダウンロードしてからインストールする] オプションが便利です。

1. **[変更]** を選択します。

1. 新しいワークロードがインストールされたら、Visual Studio インストーラーで **[起動]** を選択し、Visual Studio を開きます。

::: moniker-end

## <a name="modify-individual-components"></a>個々のコンポーネントの変更

ワークロードを使用せずに Visual Studio のインストールをカスタマイズする場合は、Visual Studio インストーラーで **[個別のコンポーネント]** タブを選択し、必要なコンポーネントを選択して、画面の指示に従います。

>[!TIP]
> SQL Server Data Tools (SSDT) については、「[Visual Studio の SQL Server Data Tools (SSDT) をダウンロードし、インストールする](/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15&preserve-view=true)」を参照してください。

## <a name="modify-language-packs"></a>言語パックの変更

既定では、インストーラーが最初に実行されるときに、オペレーティング システムの言語に一致させます。 しかし、必要に応じていつでも言語を変更できます。 これを行うには、Visual Studio インストーラーの **[言語パック]** タブを選択し、希望する言語を選択して、画面の指示に従います。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>参照

* [Visual Studio のワークロードとコンポーネント ID の一覧](workload-and-component-ids.md)
* [Visual Studio の更新](update-visual-studio.md)
* [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
* [サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
