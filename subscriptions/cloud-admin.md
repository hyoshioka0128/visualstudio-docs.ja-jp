---
title: 月次サブスクリプションの管理者を設定する | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/02/2020
ms.topic: conceptual
description: 月次サブスクリプションの管理者を設定する
ms.openlocfilehash: d9ae6f8aac48b9d54b851d543a72fd98854c1131
ms.sourcegitcommit: 9eff8371b7a79a637ebb6850f775dd3eed343d8b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2020
ms.locfileid: "78235213"
---
# <a name="set-up-administrators-for-visual-studio-monthly-subscriptions"></a>Visual Studio 月次サブスクリプションの管理者を設定する

Visual Studio 月次サブスクリプションは管理者によって管理されます。 各管理者は、サブスクリプションの割り当て、割り当ての編集、サブスクリプションの追加または削除、その他のサブスクリプション管理タスクを実行できます。

## <a name="the-azure-subscription-owner-is-the-first-administrator"></a>Azure サブスクリプションの所有者が最初の管理者です。

Visual Studio 月次サブスクリプションを購入すると、その購入を行うために使用された Azure サブスクリプションの所有者となり、そのサブスクリプションの管理者に自動的に設定されます。

月次サブスクリプションを購入するには、[Visual Studio Marketplace](https://marketplace.visualstudio.com/subscriptions) を使用するか、クラウド ソリューション プロバイダーにお問い合わせください。 Visual Studio Marketplace を使用して購入した場合、購入エクスペリエンスの終了時にユーザーの管理を実行できます。 そのオプションを選択すると、Visual Studio サブスクリプション管理ポータル ([https://manage.visualstudio.com](https://manage.visualstudio.com)) が表示されます。

サブスクリプションを購入したら、いつでも[管理ポータル](https://manage.visualstudio.com)にアクセスできます。 ポータルにサインインし、左上にある適切な Azure サブスクリプションを選択してください。

月次サブスクリプションの購入に使用された Azure サブスクリプションの所有者は、追加の管理者を割り当てることもできます。

## <a name="add-administrators"></a>管理者を追加する

管理者を追加するには:

1. Azure Portal ([portal.azure.com](https://portal.azure.com)) にアクセスします。
2. Visual Studio 月次サブスクリプションの購入に使用したアカウントを使ってサインインします。
3. 左側のナビゲーション ウィンドウで、 **[コストの管理と請求]** まで下にスクロールします。
4. **[個人用サブスクリプション]** リストで、購入に使用した Azure サブスクリプションを選択します。
5. 左側のナビゲーション ウィンドウのリストの一番上の近くにある **[アクセス制御]** をクリックします。
6. ページの上部にある **[追加]** タブをクリックします。
7. **[ロールの割り当ての追加]** をクリックします。
8. 右側のポップアップ ウィンドウで、ウィンドウの一番上にある **[ロール]** ドロップダウンをクリックし、下にスクロールして **[ユーザー アクセス管理者]** を選択します。
9. ユーザーの一覧で、管理者にするユーザーまで下にスクロールして、選択します。 
10. **[保存]** をクリックします。
11. **[ロールの割り当て]** タブをクリックし、選択したユーザーがユーザー アクセス管理者として表示されることを確認します。

新しい管理者は、[管理ポータル](https://manage.visualstudio.com)にサインインし、ページの左上のリストから月次サブスクリプションの購入に使用したものと同じ Azure サブスクリプションを選択して、それらのサブスクリプションの管理を開始できます。

> [!NOTE]
> 管理者として設定しなかったユーザーが、月次サブスクリプションを編集するアクセス権を持っている場合は、基になる Azure サブスクリプションで、サブスクリプションの管理を許可するロールが付与されている可能性があります。 そのようなロールとしては、所有者、共同作成者、サービス管理者、共同管理者があります。詳細については、[課金管理者の追加](/azure/devops/organizations/billing/add-backup-billing-managers?view=vsts)に関するページを参照してください。

Visual Studio 月次サブスクリプションについては、サブスクリプションの購入に関するページの[概要](vscloud-overview.md)を参照してください。 Visual Studio 月次サブスクリプションを購入するには、Visual Studio Marketplace ([https://marketplace.visualstudio.com/subscriptions](https://marketplace.visualstudio.com/subscription)) にアクセスしてください。

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
- [最大使用量の確認](maximum-usage.md)



