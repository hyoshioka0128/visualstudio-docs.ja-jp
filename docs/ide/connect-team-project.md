---
title: チーム エクスプローラーのプロジェクトに接続する
description: Visual Studio でチーム エクスプローラーを使用し、チーム メンバーと連携してプロジェクトを開発および管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/17/2020
ms.topic: conceptual
ms.author: tglee
author: TerryGLee
ms.manager: jillfra
ms.openlocfilehash: fd482bd2225025b5cd8a14f0387e938626fad6d5
ms.sourcegitcommit: 66cda27b63c9b55782b1db223a6dbda9f8cabe13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "95006316"
---
# <a name="connect-to-projects-in-team-explorer"></a>チーム エクスプローラーのプロジェクトに接続する

::: moniker range="vs-2017"

**チーム エクスプローラー** ツール ウィンドウを使用し、プロジェクトの開発に必要なプログラミング作業を他のチーム メンバーとの間で調整し、自分、チーム、またはプロジェクトに割り当てられている作業を管理します。 **チーム エクスプローラー** は Git と GitHub のリポジトリ、Team Foundation バージョン管理 (TFVC) のリポジトリ、[Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) またはオンプレミス [Azure DevOps Server](/azure/devops/index-all) (以前の TFS) でホストされているプロジェクトに Visual Studio を接続します。 ソース コード、作業項目、およびビルドを管理できます。

::: moniker-end

::: moniker range="vs-2019"

**チーム エクスプローラー** ツール ウィンドウを使用して、自分のプログラミング作業を他のチーム メンバーとの間で調整してプロジェクトを開発し、自分、チーム、またはプロジェクトに割り当てられている作業を管理できます。

> [!IMPORTANT]
> Visual Studio 2019 [バージョン 16.8](/visualstudio/releases/2019/release-notes/) の最新のリリースでは、新しい Git バージョン管理エクスペリエンスが既定でオンになっています。 ただし、引き続きチーム エクスプローラーを使用したい場合は、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[プレビュー機能]** の順に移動してから、 **[New Git user experience]\(新しい Git ユーザー エクスペリエンス\)** チェックボックスを切り替えます。 詳細については、「[Visual Studio での Git エクスペリエンス](git-with-visual-studio.md)」ページを参照してください。

**チーム エクスプローラー** は Git と GitHub のリポジトリ、Team Foundation バージョン管理 (TFVC) のリポジトリ、[Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) またはオンプレミス [Azure DevOps Server](/azure/devops/index-all) (以前の TFS) でホストされているプロジェクトに Visual Studio を接続します。 ソース コード、作業項目、およびビルドを管理できます。

::: moniker-end

![チーム エクスプローラー[ホーム] ページ (Visual Studio)](media/team-explorer/team-explorer.png "チーム エクスプローラー - [ホーム] ページ (Visual Studio)。")

::: moniker range="vs-2017"

> [!TIP]
> Visual Studio を開いても **チーム エクスプローラー** が表示されない場合、メニュー バーで **[表示]**  >  **[チーム エクスプローラー]** の順に選択するか、**Ctrl**+ **&#92;** 、**Ctrl**+**M** の順に押して開いてください。

::: moniker-end

## <a name="connect-to-a-project-or-repository"></a>プロジェクトまたはリポジトリに接続する

**[接続]** ページでプロジェクトまたはリポジトリに接続します。

![チーム エクスプローラーの [接続] ページ](media/team-explorer/connect.png "チーム エクスプローラー - [接続] ページ (Visual Studio)")

プロジェクトに接続するには:

1. **[接続の管理]** アイコンを選択し、 **[接続]** ページを開きます。

   ![チーム エクスプローラーの [接続の管理] ボタン](media/team-explorer/manage-connections.png "チーム エクスプローラー - [接続の管理] ボタン (Visual Studio)。")

1. **[接続]** ページで、 **[接続の管理]** 、 **[プロジェクトに接続]** の順に選択します。

   ![チーム エクスプローラーのプロジェクトに接続する](media/team-explorer/connect-project.png "チーム エクスプローラー - [プロジェクトに接続] (Visual Studio)。")

> [!TIP]
> リポジトリからプロジェクトを開く場合は、[リポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo.md)方法に関するページを参照してください。 新しいプロジェクトを作成するか、ユーザーをプロジェクトに追加する場合、[プロジェクトの作成 (Azure DevOps)](/azure/devops/organizations/projects/create-project)と、[プロジェクトまたはチームへのユーザーの追加 (Azure DevOps)](/azure/devops/organizations/security/add-users-team-project)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio での新しい Git エクスペリエンス](git-with-visual-studio.md)
- [チュートリアル: リポジトリからプロジェクトを開く](../get-started/tutorial-open-project-from-repo.md)
- [チーム エクスプローラーのリファレンス](reference/team-explorer-reference.md)
- [プロジェクトに接続する (Azure DevOps)](/azure/devops/organizations/projects/connect-to-projects)
- [プロジェクトへの接続のトラブルシューティング](/azure/devops/user-guide/troubleshoot-connection?view=azure-devops&preserve-view=true)
