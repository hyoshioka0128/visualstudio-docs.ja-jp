---
title: Visual Studio サブスクリプションをユーザーに割り当てる | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 4e529a43-7aed-4eee-895d-862a631952df
ms.date: 09/21/2020
ms.topic: conceptual
description: 管理者がサブスクライバーにライセンスを割り当てる方法について説明します
ms.openlocfilehash: dd80a14a3ff57100f210fd7ae1b882c0ab7a9faf
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915415"
---
# <a name="assign-licenses-in-the-visual-studio-subscriptions-administration-portal"></a>Visual Studio サブスクリプション管理者ポータルでライセンスを割り当てる
Visual Studio サブスクリプションの管理者は、管理ポータルを使用して、個々のユーザーおよびユーザーのグループにサブスクリプションを割り当てることができます。

ユーザーのグループに対しては、サブスクリプションの割り当て方法を選択できます。  
- サブスクリプションは一度に 1 つずつ割り当てることができます。
- また、[一括追加](assign-license-bulk.md)機能を使用して、サブスクライバーとそのサブスクリプション情報の一覧を迅速かつ簡単にアップロードすることも可能です。
- 組織で Microsoft Azure Active Directory (Azure AD) を使用している場合は、[Azure AD グループを使用して、ユーザーのグループにサブスクリプションを割り当てる](./assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions)ことができます。  


## <a name="add-a-single-subscriber"></a>1 人のサブスクライバーを追加する
新しいユーザーがサブスクリプションの特典にアクセスできるように、そのユーザーに Visual Studio サブスクリプションを割り当てる方法については、動画をご覧になるか、このまま読み進めてください。

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vpPh]


1. [管理ポータル](https://manage.visualstudio.com)にサインインします。
2. 1 人の Visual Studio サブスクライバーにライセンスを割り当てるには、テーブルの上部にある **[追加]** を選択してから、 **[Individual subscriber]\(個々のサブスクライバー\)** を選択します。
   > [!div class="mx-imgBorder"]
   > ![1 人のサブスクライバーを追加する](_img/assign-license-add/add-subscriber-individual.png "[追加] を選択し、個々のサブスクライバーを選択し、単一サブスクリプションを割り当てます。")
3. フォームのフィールドに新しいサブスクライバーの情報を入力します。 組織が Azure Active Directory を使っている場合は、 **[名前]** フィールドを使って現在のディレクトリのユーザーを検索し、検索結果から適切なユーザーを選ぶことができます。 そのユーザーを選ぶと、サインイン メール アドレス、通知メール アドレスが自動的に設定されます。  組織内にサブスクライバーが見つからない場合、通知メールは自動的には設定されませんが、サブスクリプション関連のメールの送信先となる別のメール アドレスを手動で追加することができます。  メール サービスがサインイン メール アドレスへの受信メールをブロックしている場合は、サブスクライバーと管理者が Microsoft から重要なサブスクリプションに関連するメールを受信できるように、別の通知メール アドレスを指定することが重要です。
   > [!div class="mx-imgBorder"]
   > ![サブスクライバーの詳細](_img/assign-license-add/subscriber-details.png "サブスクライバーの名前とその他の詳細を入力するか、テナント メンバーから選択します。")

    > [!NOTE]
    > サブスクライバー名を入力するときに Azure Active Directory テナントのメンバーが表示されるようにするには、管理者がテナントのメンバーである必要があります。 


    このサブスクライバーが [Visual Studio サブスクリプション ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)にサインインするときにソフトウェアのダウンロードにアクセスできるようにする場合は、 **[ダウンロードの設定]** セクションでダウンロードのトグルをオンのままにします。 ダウンロードを無効にした場合、ユーザーはソフトウェアのダウンロードにアクセスできなくなります。  プロダクト キーへのアクセスも無効になります。  サブスクライバーは、サブスクリプションに含まれるその他すべての特典に引き続きアクセスできます。
   > [!div class="mx-imgBorder"]
   > ![ダウンロードにアクセスする](media/access-to-downloads.png "[許可] を選択して、サブスクライバーがソフトウェアのダウンロードにアクセスできるようにします。")

    サブスクリプションに独自の参照メモを追加する場合は、 **[Add reference]\(参照の追加\)** セクションで追加できます。
   > [!div class="mx-imgBorder"]
   > ![サブスクリプションごとに独自の参照メモを追加する](media/add-subscriber-reference-notes.png "このサブスクリプションに関するメモがあれば、[参照] フィールドを使用してそれを記録します。")

    オプションの選択とサブスクライバーのデータの入力が終わったら、 **[Add Subscriber]\(サブスクライバーの追加\)** フライアウトの下部にある **[追加]** を選択します。
   > [!div class="mx-imgBorder"]
   > ![[追加] ボタンを選択する](media/add-button.png "[追加] を選択して情報を保存し、サブスクリプションをサブスクライバーに割り当てます。")

## <a name="why-use-a-different-notification-email-address"></a>別の通知メール アドレスを使用するのはなぜですか?
一部の組織では、他のドメインからの受信メールをブロックするようにメール サービスを設定しています。  受信メールをブロックすると、サブスクライバーと管理者は重要な通信を行うことができなくなります。
- サブスクライバーは、サブスクリプションが割り当てられているという通知を受け取りません。  これにより、含まれているベネフィットの一部をアクティブ化することもできなくなります。  
- GitHub Enterprise で Visual Studio サブスクリプションを割り当てられているサブスクライバーに、GitHub 組織に参加するための招待が届きません。つまり、招待を受け入れることができません。 GitHub 組織にアクセスするには、**メールで送信された招待を受け入れる必要があります**。 
- 管理者は、契約に追加されたときに通知されず、月ごとの管理者のステートメントを受け取るか、またはサブスクリプションの管理方法に影響を与える機能変更の通知を受け取ります。

通知メール アドレスを使用すれば、サインイン メール アドレスの機能を変更することなく、サブスクリプションに関する重要な情報をサブスクライバーが受信できるようにするオプションが提供されます。  

## <a name="resend-assignment-emails"></a>割り当てメールを再送信する
サブスクライバーを追加すると、詳細な説明が記載された割り当てメールがサブスクライバーに自動的に送信されます。 サブスクライバーを選択して、上部メニューの **[再送信]** ボタンを選択することで、いつでも割り当てメールを送信し直すことができます。  複数のユーザーにメールを再送信するには、**Ctrl** キーを押しながら複数のサブスクライバーを選択します。  **[再送信]** ボタンを選択すると、そのサブスクライバーに再送信するかどうかを確認するダイアログが表示されます。  



## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)


## <a name="next-steps"></a>次の手順
- 多数のユーザーを追加する必要がありますか?  [複数のサブスクライバー](assign-license-bulk.md)にサブスクリプションを割り当てる方法について説明します。
- お困りの際は、  [Visual Studio の管理とサブスクリプションのサポート](https://visualstudio.microsoft.com/support/support-overview-vs)にお問い合わせください。