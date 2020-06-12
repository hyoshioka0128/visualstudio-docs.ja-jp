---
title: Visual Studio サブスクリプションにライセンスを割り当てる | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 4e529a43-7aed-4eee-895d-862a631952df
ms.date: 03/02/2020
ms.topic: conceptual
description: 管理者がサブスクライバーにライセンスを割り当てる方法を説明します
ms.openlocfilehash: a90d6f3fec1f619cda397788c130f7514307effd
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183471"
---
# <a name="assign-licenses-in-the-visual-studio-subscriptions-administration-portal"></a>Visual Studio サブスクリプション管理者ポータルでライセンスを割り当てる
Visual Studio サブスクリプションの管理者は、管理者ポータルを使用して、個々のユーザーおよびユーザーのグループにサブスクリプションを割り当てることができます。

ユーザーのグループに対しては、サブスクリプションの割り当て方法を選択できます。  
- サブスクリプションは一度に 1 つずつ割り当てることができます。
- また、[一括追加](assign-license-bulk.md)機能を使用して、サブスクライバーとそのサブスクリプション情報の一覧を迅速かつ簡単にアップロードすることも可能です。
- 組織で Microsoft Azure Active Directory (Azure AD) を使用している場合は、[Azure AD グループを使用して、ユーザーのグループにサブスクリプションを割り当てる](https://docs.microsoft.com/visualstudio/subscriptions/assign-license-bulk#use-azure-active-directory-groups-to-assign-subscriptions)ことができます。  


## <a name="add-a-single-subscriber"></a>1 人のサブスクライバーを追加する
次に、新しいユーザーがサブスクリプションの特典にアクセスできるように、そのユーザーに Visual Studio サブスクリプションを割り当てる方法を示します。

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vpPh]


1. [管理ポータル](https://manage.visualstudio.com)にサインインします。
2. 1 人の Visual Studio サブスクライバーにライセンスを割り当てるには、テーブルの上部にある **[追加]** を選択してから、 **[Individual subscriber]\(個々のサブスクライバー\)** を選択します。
   > [!div class="mx-imgBorder"]
   > ![1 人のサブスクライバーを追加する](_img/assign-license-add/add-subscriber-individual.png)
3. フォームのフィールドに新しいサブスクライバーの情報を入力します。 組織が Azure Active Directory を使っている場合は、 **[名前]** フィールドを使って現在のディレクトリのユーザーを検索し、検索結果から適切なユーザーを選ぶことができます。 そのユーザーを選ぶと、サインイン メール アドレス、通知メール アドレスが自動的に設定されます。
   > [!div class="mx-imgBorder"]
   > ![サブスクライバーの詳細](_img/assign-license-add/subscriber-details.png)

    > [!NOTE]
    > サブスクライバー名を入力するときに Azure Active Directory テナントのメンバーが表示されるようにするには、管理者がテナントのメンバーである必要があります。 


    このサブスクライバーが [Visual Studio サブスクリプション ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)にサインインするときにソフトウェアのダウンロードにアクセスできるようにする場合は、 **[ダウンロードの設定]** セクションでダウンロードのトグルをオンのままにします。 ダウンロードを無効にした場合、ユーザーはソフトウェアのダウンロードにアクセスできなくなります。  プロダクト キーへのアクセスも無効になります。  サブスクライバーは、サブスクリプションに含まれるその他すべての特典に引き続きアクセスできます。
   > [!div class="mx-imgBorder"]
   > ![ダウンロードにアクセスする](media/access-to-downloads.png)

    サブスクリプションに独自の参照メモを追加する場合は、 **[Add reference]\(参照の追加\)** セクションで追加できます。
   > [!div class="mx-imgBorder"]
   > ![サブスクリプションごとに独自の参照メモを追加する](media/add-subscriber-reference-notes.png)

    オプションの選択とサブスクライバーのデータの入力が終わったら、 **[Add Subscriber]\(サブスクライバーの追加\)** フライアウトの下部にある **[追加]** を選択します。
   > [!div class="mx-imgBorder"]
   > ![[追加] ボタンを選択する](media/add-button.png)

## <a name="resend-assignment-emails"></a>割り当てメールを再送信する
サブスクライバーを追加すると、詳細な説明が記載された割り当てメールがサブスクライバーに自動的に送信されます。 サブスクライバーを選択して、上部メニューの **[再送信]** ボタンをクリックすることで、いつでも割り当てメールを送信し直すことができます。  複数のユーザーにメールを再送信するには、**Ctrl** キーを押しながら複数のサブスクライバーを選択します。  **[再送信]** ボタンをクリックすると、そのサブスクライバーに再送信するかどうかを確認するダイアログが表示されます。  

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)


## <a name="next-steps"></a>次の手順
- 多数のユーザーを追加する必要がありますか?  [複数のサブスクライバー](assign-license-bulk.md)にサブスクリプションを割り当てる方法について説明します。
- お困りの際は、  [Visual Studio の管理とサブスクリプションのサポート](https://visualstudio.microsoft.com/support/support-overview-vs)にお問い合わせください。


