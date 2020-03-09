---
title: Visual Studio サブスクリプション管理ポータルでのサブスクリプション割り当ての削除 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/03/2020
ms.topic: conceptual
description: 管理者がサブスクリプションの割り当てを削除する方法を説明します。
ms.openlocfilehash: 6ed64f5c05f77bea7f157eee9e29bbb05aa8730d
ms.sourcegitcommit: 3ed59ce39692124fe61c484df4348c0b9abee9b9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78263248"
---
# <a name="delete-assignments-in-visual-studio-subscriptions"></a>Visual Studio サブスクリプションで割り当てを削除する
サブスクライバーが会社を退職したり、プロジェクトを完了したり、新しい仕事の役割に切り替わったりして、Visual Studio サブスクリプションが不要になった場合に、それらのサブスクリプションを削除して、他のユーザーに割り当てることができます。 サブスクリプションを再割り当てする場合は、サブスクライバーのすべての特典がリセットされるわけではないことに注意してください。  新しいユーザーは要求されていない任意のキーを要求し、以前に要求されたキーを表示できるようになりますが、要求の上限はリセット**されません**。  エンタープライズ契約 (EA) を締結している組織の場合、Pluralsight トレーニングなど、元のユーザーによって使用されていたすべての特典がリセットされます。 

## <a name="delete-a-subscription-assignment"></a>サブスクリプションの割り当てを削除する
1. 削除するサブスクライバーの名前をクリックします。 削除する複数のサブスクライバーを選択するには、サブスクライバー名の左にある円をクリックして、1 つずつ選択できます。  または、**CTRL** キーを押しながら、削除する各サブスクライバーをクリックすることもできます。  すべてのサブスクライバーを選択して削除するには、**CTRL + A** キーを押します。 
2. 選択したサブスクライバーを削除するには、 **[削除]** をクリックします。
3. 削除の確認を求めるメッセージが表示されたら、 **[OK]** をクリックします。
   > [!div class="mx-imgBorder"]
   > ![サブスクライバーの削除](_img/delete-license/delete-subscribers.png)

   > [!NOTE]
   > テンプレートを利用した一括削除は、使用できません。 Azure Active Directory セキュリティ グループを使用してサブスクリプションの割り当てを管理している組織では、削除の実行方法の詳細については、[こちらの記事](assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions)を参照してください。  

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
- サプスクリプションを削除せずに変更する必要がありますか?  [サブスクリプションの編集](edit-license.md)方法をご確認ください。
- 特定のサブスクリプションを検索する方法については、[サブスクリプションの検索](search-license.md)に関する記事を参照してください。
- すべてのサブスクリプションの一覧を作成する必要がありますか?  [サブスクリプションのエクスポート](exporting-subscriptions.md)に関する記事を参照してください。


