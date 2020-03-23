---
title: 管理ポータルでのスーパー管理者と管理者ロール
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/02/2020
ms.topic: conceptual
description: スーパー管理者と管理者ロール、および管理者を割り当てる方法について説明します。
ms.openlocfilehash: ef0ba479c099bf1e34fe871386984297b130ffd6
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "78234830"
---
# <a name="super-admins-and-administrators-for-visual-studio-subscription-agreements"></a>Visual Studio サブスクリプション契約のスーパー管理者と管理者

新しい Visual Studio サブスクリプションの管理ポータルには、ボリューム ライセンスのお客様用に 2 つの異なるロールが用意されています。 これらのロールは、以前 VLSC にあった主要/通知連絡先ロールとサブスクリプション マネージャー ロールに似ています。

**スーパー管理者:** 最初に組織を設定したとき、主要または通知連絡先が既定でスーパー管理者になります。 主要または通知連絡先は、追加のスーパー管理者または管理者を割り当てることを選択できます。 スーパー管理者では、他の管理者だけでなくサブスクライバーを追加および削除することができます。 システムに 2 人以上のスーパー管理者がいる場合、スーパー管理者はセキュリティのために最後の 2 人を除くすべての管理者を削除できます。

**管理者:** スーパー管理者のみが管理者を割り当てることができます。管理者は、スーパー管理者に割り当てられた契約のサブスクライバーのみを管理できます。

## <a name="assigning-administrators"></a>管理者の割り当て
新しい管理者 (管理者) を割り当てるには:
1. サブスクリプションを購入した契約でスーパー管理者に割り当てられるメール アドレスを使用し、 https://manage.visualstudio.com にサインインします。
2. **[管理者の管理]** というラベルのタブをクリックします。
3. **[追加]** をクリックします。
   > [!div class="mx-imgBorder"]
   > ![管理者の追加](_img/admin-roles/add-admins.png)
4. 新しい管理者の情報でフォームを完成させます。  
   > [!div class="mx-imgBorder"]
   > ![[管理者の追加] フォーム](_img/admin-roles/add-form.png)

   > [!NOTE]
   > この管理者が管理者をさらに割り当てることができるようにするには、 **[スーパー管理者]** チェックボックスをオンにすることを忘れないでください。

5. **[追加]** をクリックすると、新規に割り当てられた管理者は、ポータルにサインインする招待メールを受信します。  

## <a name="resources"></a>リソース
- [Visual Studio の管理とサブスクリプションのサポート](https://visualstudio.microsoft.com/support/support-overview-vs)

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)


## <a name="next-steps"></a>次の手順
- [サブスクリプションを割り当てる](assign-license.md)方法を学ぶ
- さまざまな[サブスクリプションのメリット](https://visualstudio.microsoft.com/vs/benefits/)について学ぶ
- [契約の基本設定を設定する](admin-prefs.md) 


