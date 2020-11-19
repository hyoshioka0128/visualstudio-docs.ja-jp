---
title: 新しい月単位のサブスクリプションをサブスクリプション管理ポータルに追加する | Microsoft Docs
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: 36f0d9f1-fe28-469f-a54c-dc46638270a8
ms.date: 09/03/2020
ms.topic: how-to
description: 新しく購入した月単位の Visual Studio サブスクリプションをサブスクリプション管理ポータルに追加する方法について説明します
ms.openlocfilehash: f6b835969fff3a8316a2b46c6e15217ebe3e33b1
ms.sourcegitcommit: a731a9454f1fa6bd9a18746d8d62fe2e85e5ddb1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/01/2020
ms.locfileid: "92467597"
---
# <a name="add-new-monthly-visual-studio-subscriptions-to-the-subscriptions-administration-portal"></a>新しい月単位の Visual Studio サブスクリプションをサブスクリプション管理ポータルに追加する
Azure サブスクリプションを使用して新しい月単位の Visual Studio サブスクリプションを購入するときに、それらをユーザーに割り当てるにはサブスクリプション管理ポータルへの追加が必要な場合があります。  

## <a name="how-do-i-know-if-i-need-to-add-my-subscriptions"></a>サブスクリプションを追加する必要があるかどうかを知る方法
月単位のサブスクリプションを追加する手順は、組織で既に使用されているサブスクリプションの種類と、お客様が新しい管理者であるかどうかによって異なります。
- お客様が新しい管理者である場合は、サブスクリプション管理ポータルに初めてサインインするときに、お客様がユーザー アクセス管理者権限を持っている Azure サブスクリプションがチェックされます。  月単位のサブスクリプションがある場合は、それらが自動的に追加されます。 
- 月単位のサブスクリプションの追加または管理を既に実行している場合は、サインインするたびに新しい月単位のサブスクリプションの有無が確認されます。 
- 既にボリューム ライセンスによって取得されたサブスクリプションの管理者であるが、以前に月単位のサブスクリプションの追加または管理を実行したことがない場合は、以下の手順を使用してそれらを追加する必要があります。

## <a name="how-to-add-monthly-subscriptions"></a>月単位のサブスクリプションを追加する方法
1. サブスクリプション管理ポータル (<https://manage.visualstudio.com>) にサインインします。
1. **[サブスクライバーの管理]** タブで、 **[Add agreement]\(契約の追加\)** ドロップダウンを選択します。 
1. ドロップダウンで **[新しい月単位のサブスクリプション]** を選択します。
   > [!div class="mx-imgBorder"]
   > ![新しい月単位のサブスクリプションを追加するドロップダウン](_img/add-monthly-subs/add-subs-drop-down.png "[Add agreement]\(契約の追加\) を選択し、[New monthly subscriptions]\(新しい月額サブスクリプション\) を選択する。")
1. ユーザー アクセス管理者権限があるすべての Azure サブスクリプションがシステムによって検索され、それらの Azure サブスクリプションで購入されたすべての Visual Studio サブスクリプションがインポートされます。
1. ユーザー アクセス管理者権限のある Azure サブスクリプションが見つからない場合、または該当する Azure サブスクリプションはあるが Visual Studio サブスクリプションが見つからない場合は、次のメッセージが表示されます。
   > [!div class="mx-imgBorder"]
   > ![新しい月単位のサブスクリプションが見つかりません](_img/add-monthly-subs/no-subs-found.png "使用できる Azure サブスクリプションまたは Visual Studio サブスクリプションがないことを示すエラー メッセージ。")
1. 新しい月単位のサブスクリプションが見つかった場合は、確認メッセージが表示されます。
   > [!div class="mx-imgBorder"]
   > ![サブスクリプション追加の確認メッセージ](_img/add-monthly-subs/subs-added-confirmation.png "追加したサブスクリプションが確認メッセージに表示される。")

## <a name="things-to-keep-in-mind"></a>留意事項
- 新しい月単位のサブスクリプションを追加するオプションは、初回の購入時にのみ使用できます。  月単位のサブスクリプションを追加している場合は、ポータルにサインインするたびに、新しいサブスクリプションの有無が確認されます。 
- 新しいサブスクリプションが見つかった場合は、それらが既にサブスクライバーに割り当てられていることを確認できます。  これは、Azure サブスクリプションへのアクセス権を持つ他の管理者が存在し、その管理者によって既に新しい Visual Studio サブスクリプションがユーザーに割り当てられているためです。  これで自分のポータルにも追加したので、それらのサブスクリプションを管理できます。 

## <a name="next-steps"></a>次の手順
サブスクリプションを追加したので、それらをユーザーに割り当てることができます。  それはさまざまな方法で実行できます。
- [サブスクリプションを個別に割り当てる](assign-license.md)
- [サブスクリプションを複数のユーザーに割り当てる](assign-license-bulk.md)
- [特定のサブスクリプションを特定のユーザーに割り当てる](assign-guid.md)

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)