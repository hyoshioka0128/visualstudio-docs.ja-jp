---
title: チーム エクスプローラーのリファレンス
ms.date: 12/04/2018
ms.topic: reference
ms.author: kaelli
author: KathrynEE
ms.manager: jillfra
ms.openlocfilehash: b1a956579b527de9df9d24bd09dda6ae48eff961
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74538568"
---
# <a name="team-explorer-reference"></a>チーム エクスプローラーのリファレンス

この記事では、**チーム エクスプローラー**のさまざまな機能に関する Azure DevOps 記事のリンクを紹介します。

**チーム エクスプローラー** ツール ウィンドウを使用し、プロジェクトの開発に必要なプログラミング作業を他のチーム メンバーとの間で調整し、自分、チーム、またはプロジェクトに割り当てられている作業を管理します。 **チーム エクスプローラー**は Git と GitHub のリポジトリ、Team Foundation バージョン管理 (TFVC) のリポジトリ、[Azure DevOps Services](/azure/devops/user-guide/what-is-azure-devops-services) またはオンプレミス [Azure DevOps Server](/azure/devops/index-all) (以前の TFS) でホストされているプロジェクトに Visual Studio を接続します。 ソース コード、作業項目、およびビルドを管理できます。

## <a name="home-page"></a>ホーム ページ

**チーム エクスプローラー**で[プロジェクトに接続する](../connect-team-project.md)と、 **[プロジェクト]** セクションで次のリンクが利用可能になります。

- [リポジトリのクローン](/azure/devops/repos/git/clone)
- [Web ポータル](/azure/devops/project/navigation/index)
- [タスク ボード](/azure/devops/boards/sprints/task-board)

[Git](/azure/devops/repos/git/gitquickstart?view=vsts&tabs=visual-studio) のリポジトリに接続するか、[Team Foundation バージョン管理 (TFVC)](/azure/devops/repos/tfvc/overview) のリポジトリに接続するかによって、 **[ホーム]** ページには異なる機能が表示されます。

> [!TIP]
> 2 つのバージョン管理システムの比較は、[プロジェクト用の最適なバージョン管理の選択 (Azure DevOps)](/azure/devops/repos/tfvc/comparison-git-tfvc) に関するページを参照してください。

| Git に接続されている場合の **[ホーム]** ページ | TFVC に接続されている場合の **[ホーム]** ページ |
| - | - |
| ![Git に接続されている場合のチーム エクスプローラー[ホーム] ページ (Visual Studio 2019)](media/team-explorer-reference/team-explorer-git.png) | ![TFVC に接続されている場合のチーム エクスプローラー[ホーム] ページ (Visual Studio)](media/team-explorer-reference/team-explorer-tfvc.png) |

## <a name="changes-page-git"></a>変更ページ (Git)

「[Save work with commits](/azure/devops/repos/git/commits)」 (コミットを使用して作業を保存する) を参照してください。

## <a name="branches-page-git"></a>ブランチ ページ (Git)

「[Create work in branches](/azure/devops/repos/git/branches)」 (ブランチで作業を作成する) を参照してください。

## <a name="pull-requests-page-git"></a>Pull Request ページ (Git)

「[Review code with pull requests](/azure/devops/repos/git/pullrequest)」(Pull Request を使用してコードを確認する) を参照してください。

## <a name="sync-page-git"></a>同期ページ (Git)

「[Update code with fetch and pull](/azure/devops/repos/git/pulling)」 (フェッチとプルを使用してコードを更新する) を参照してください。

## <a name="tags-page-git"></a>タグ ページ (Git)

「[Work with Git tags](/azure/devops/repos/git/git-tags)」 (Git タグを使用する) を参照してください。

## <a name="my-work-page-tfvc"></a>担当作業ページ (TFVC)

「[Suspend/resume work](/azure/devops/repos/tfvc/suspend-your-work-manage-your-shelvesets)」 (作業の中断/再開) と「[Code review](/azure/devops/repos/tfvc/day-life-alm-developer-suspend-work-fix-bug-conduct-code-review)」 (コードの確認) を参照してください。

## <a name="pending-changes-page-tfvc"></a>保留中の変更ページ (TFVC)

「[Manage pending changes](/azure/devops/repos/tfvc/develop-code-manage-pending-changes)」 (保留中の変更の管理)、「[Find shelvesets](/azure/devops/repos/tfvc/suspend-your-work-manage-your-shelvesets)」 (シェルブセットの検索)、「[Resolve conflicts](/azure/devops/repos/tfvc/resolve-team-foundation-version-control-conflicts)」 (競合の解決) を参照してください。

## <a name="source-control-explorer-page-tfvc"></a>ソース管理エクスプローラー ページ (TFVC)

[ファイルとフォルダーの追加/表示](/azure/devops/repos/tfvc/add-files-server)に関するページを参照してください。

## <a name="work-items-page"></a>作業項目ページ

**[作業項目]** ページでは、[作業項目](/azure/devops/boards/work-items/about-work-items)クエリを確認できます。 参照:

- [作業項目の追加](/azure/devops/boards/backlogs/add-work-items)
- [クエリ エディターを使用してクエリを一覧表示し、管理する](/azure/devops/boards/queries/using-queries)
- [クエリ フォルダーを整理し、クエリのアクセス許可を設定する](/azure/devops/boards/queries/set-query-permissions)
- [クエリを Excel で開く](/azure/devops/boards/backlogs/office/bulk-add-modify-work-items-excel)
- [クエリを Project で開く](/azure/devops/boards/backlogs/office/create-your-backlog-tasks-using-project)
- [Outlook を使用してクエリ結果リストを電子メールで送信する](/azure/devops/boards/queries/share-plans)
- [Excel でクエリからレポートを作成する](/azure/devops/report/excel/create-status-and-trend-excel-reports) (TFS のみ)

::: moniker range=">= vs-2019"

> [!NOTE]
> Visual Studio 2019 では[作業項目ページが新しくなりました](/azure/devops/boards/work-items/set-work-item-experience-vs)。 Visual Studio 2019 で作業項目を表示する方法については、[作業項目の表示および追加](/azure/devops/boards/work-items/view-add-work-items)に関するページを参照してください。

::: moniker-end

## <a name="builds-page"></a>ビルドページ

**ビルド**ページでは、プロジェクトのビルド定義を確認できます。

参照:

- [ビルド パイプラインの作成](/azure/devops/pipelines/tasks/index)
- [ビルドの表示と管理](/azure/devops/pipelines/overview)
- [ビルド キューの管理](/azure/devops/pipelines/agents/pools-queues)
- [Visual Studio の継続的デリバリー (CD) をインストールする](/azure/devops/pipelines/apps/cd/azure/aspnet-core-to-acr#install-continuous-delivery-cd-tools-for-visual-studio-2017)
- [アプリの継続的デリバリー (CD) を構成し、実行する](/azure/devops/pipelines/apps/cd/azure/aspnet-core-to-acr#configure-and-execute-continuous-delivery-cd-for-your-app)

## <a name="settings-page"></a>設定ページ

**設定**ページでは、プロジェクトまたはプロジェクト コレクションの管理機能を構成できます。 次の記事をご覧ください。

| Project | プロジェクト コレクション | その他 |
| - | - | - |
| [セキュリティ、グループ メンバーシップ](/azure/devops/organizations/security/set-project-collection-level-permissions)<br/>[セキュリティ、ソース管理 (TFVC)](/azure/devops/organizations/security/set-git-tfvc-repository-permissions)<br/>[作業項目の区分](/azure/devops/organizations/settings/set-area-paths)<br/>[作業項目のイテレーション](/azure/devops/organizations/settings/set-iteration-paths-sprints)<br/>[ポータルの設定](/azure/devops/report/sharepoint-dashboards/configure-or-add-a-project-portal)<br/>[プロジェクト警告](/azure/devops/notifications/howto-manage-team-notifications) | [セキュリティ、グループ メンバーシップ](/azure/devops/organizations/security/set-project-collection-level-permissions)<br/>[ソース管理 (TFVC)](/azure/devops/repos/tfvc/decide-between-using-local-server-workspace)<br/>[プロセス テンプレート マネージャー](/azure/devops/boards/work-items/guidance/manage-process-templates) | [Git グローバル設定](/azure/devops/repos/git/git-config)<br/>[Git リポジトリ設定](/azure/devops/repos/git/git-config) |

## <a name="see-also"></a>参照

- [チーム エクスプローラーのプロジェクトに接続する](../../ide/connect-team-project.md)
