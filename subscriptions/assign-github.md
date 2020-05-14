---
title: Visual Studio + GitHub Enterprise オファー | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: f271d623-dcde-442a-865c-4dca5ad8a9c5
ms.date: 03/17/2020
ms.topic: conceptual
description: Visual Studio + GitHub Enterprise オファーでのサブスクリプションの管理
ms.openlocfilehash: d7100c2b9cfdd12579419927fd0bf8885038048b
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "79509006"
---
# <a name="manage-visual-studio-subscriptions-with-github-enterprise"></a>GitHub Enterprise を使用して Visual Studio サブスクリプションを管理する
Microsoft と Enterprise Agreement (EA) を契約しているお客様は、Visual Studio Standard サブスクリプションと GitHub Enterprise が一体化した、新しいサブスクリプション オファーを購入できます。 この方法により、Visual Studio サブスクライバーは GitHub Enterprise を簡単かつ経済的に入手することができます。 

組織が Visual Studio Subscriptions with GitHub Enterprise を購入すると、2 つの部分に分かれてプロビジョニングおよび管理されます。

## <a name="manage-visual-studio-subscriptions"></a>Visual Studio サブスクリプションを管理する
組織が Visual Studio Subscriptions with GitHub Enterprise を購入すると、サブスクリプションの Visual Studio の部分がすぐにプロビジョニングされ、Visual Studio [サブスクリプション管理](https://manage.visualstudio.com)ポータルでの割り当てと管理に、そのサブスクリプションを使用できるようになります。 

サブスクリプションの管理の詳細については、次のトピックをご覧ください。
- [管理ポータルの使用](using-admin-portal.md)
- [サブスクリプションを割り当てる](assign-license.md)
- [サブスクリプションの編集](edit-license.md)
- [サブスクリプションの削除](delete-license.md)
- [超過](handle-overclaimed-license.md)

> [!Important]
> Visual Studio Subscriptions with GitHub Enterprise が Visual Studio サブスクリプション管理者によって割り当てられていて、これらのサブスクリプションが一度も購入されていない場合、これらは組織内の GitHub Enterprise 管理者に対して表示されません。 GitHub Enterprise サブスクリプションが表示されるようにするには、最初にサブスクリプションが割り当てられたときに、Visual Studio Professional with GitHub Enterprise または Visual Studio Enterprise with GitHub Enterprise の**少なくとも 1 つの**サブスクリプションを含む購入を行う必要があります。  
>
> 割り当てられている GitHub サブスクリプションごとに、このサブスクリプションのライセンス要件への準拠を維持するために、お客様の責任下で、Visual Studio サブスクリプション管理ポータルで対応する Visual Studio with GitHub サブスクリプションが割り当てられていることを確認します。

## <a name="manage-github-enterprise-subscriptions"></a>GitHub Enterprise サブスクリプションを管理する
GitHub Enterprise サブスクリプションが購入されると、GitHub ではお客様との連携がなされて、GitHub にアクセスする組織が作成および構成され、管理者が識別されます。  すると、これらの管理者は、管理者として設定されていることを示す通知を受け取ります。  

このプロセスは非常に複雑であるため、サブスクリプションの購入後、組織と管理者が完全に設定されるまで数日かかることがあります。

GitHub は、クラウド ベースの GitHub.com、またはオンプレミスの GitHub Enterprise Server のいずれかとして使用できます。  2 つのバージョンを管理するプロセスは異なります。  GitHub では、GitHub Enterprise サブスクリプションの管理に役立つ、さまざまなヘルプ トピックや管理者ガイドが提供されています。  選択したトピックへのリンクを次に示します。  

### <a name="githubcom"></a>GitHub.com 
GitHub.com の管理の詳細については、[GitHub ヘルプ](https://help.github.com/en)の次のトピックをご覧ください。
+ [ヘルプ トピックの完全な一覧](https://help.github.com/en)
+ [組織内のメンバーシップの管理](https://help.github.com/en/articles/managing-membership-in-your-organization)
+ [組織参加へのユーザーの招待](https://help.github.com/en/articles/inviting-users-to-join-your-organization)
    - [チーム/組織からのユーザーの削除](https://help.github.com/en/articles/removing-a-member-from-your-organization)
    - [組織の以前のメンバーの回復](https://help.github.com/en/articles/reinstating-a-former-member-of-your-organization)
+ [ロールを使用したアクセスの管理](https://help.github.com/en/articles/managing-peoples-access-to-your-organization-with-roles)
+ [チームへのユーザーの編成](https://help.github.com/en/articles/organizing-members-into-teams)
+ [組織のリポジトリへのアクセスの管理](https://help.github.com/en/articles/managing-access-to-your-organizations-repositories)

### <a name="github-enterprise-server"></a>GitHub Enterprise Server
GitHub ヘルプでは、組織における GitHub Enterprise Server の実装の管理について、質問に回答したりヒントを示すさまざまな管理者ガイドが提供されています。

+ [すべての管理者ガイドの表示](https://help.github.com/en/enterprise/2.16/admin)
+ [ユーザー管理](https://help.github.com/en/enterprise/2.16/admin/user-management)
    - [組織とチーム](https://help.github.com/en/enterprise/2.16/admin/user-management/organizations-and-teams)
        - [組織の作成](https://help.github.com/en/enterprise/2.16/admin/user-management/creating-organizations)
        - [チームの作成](https://help.github.com/en/enterprise/2.16/admin/user-management/creating-teams)
        - [チームへのユーザーの追加](https://help.github.com/en/enterprise/2.16/admin/user-management/adding-people-to-teams)
        - [チームおよび組織からのユーザーの削除](https://help.github.com/en/enterprise/2.16/admin/user-management/removing-users-from-teams-and-organizations)
    - [ユーザー セキュリティ](https://help.github.com/en/enterprise/2.16/admin/user-management/user-security)
+ [GitHub Enterprise Server のインストールと構成](https://help.github.com/en/enterprise/2.16/admin/installation)

## <a name="support-resources"></a>サポート リソース
- [GitHub ヘルプ](https://help.github.com/en)で、GitHub のさまざまなトピックに関する質問への回答を確認できます。
- [GitHub Community Forum](https://github.community/) で、他の GitHub ユーザーからサポートを得ることができます。
- Visual Studio サブスクリプションの販売、サブスクリプション、アカウント、課金のサポートについては、Visual Studio [サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/)にお問い合わせください。
- Visual Studio IDE、Azure DevOps Services、またはその他の Visual Studio の製品やサービスに関する質問がありますか。  [Visual Studio のサポート](https://visualstudio.microsoft.com/support/)にアクセスしてください。
- GitHub Enterprise の[テクニカル サポート](https://support.microsoft.com/en-us/supportforbusiness/productselection?sapId=b77fe80f-5417-80bd-4b2a-275cf0018c24)を利用してください。   

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
Visual Studio サブスクリプションの管理に関する詳細情報をご覧ください。
- [個別のサブスクリプションの割り当て](assign-license.md)
- [複数のサブスクリプションを管理する](assign-license-bulk.md)
- [サブスクリプションの編集](edit-license.md)
- [サブスクリプションの削除](delete-license.md)
- [最大使用量の確認](maximum-usage.md)

Visual Studio Subscriptions with GitHub Enterprise の管理の詳細については、Visual Studio の[サブスクリプション管理ポータル](https://visualstudio.microsoft.com/subscriptions-administration/)をご覧ください。


