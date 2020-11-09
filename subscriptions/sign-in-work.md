---
title: 職場または学校アカウントで Visual Studio サブスクリプションにサインインする | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: f39a2672-c283-4755-93d3-31c7c7a032d0
ms.date: 10/28/2020
ms.topic: how-to
description: 職場または学校アカウントを使用して Visual Studio サブスクリプションにサインインする方法について説明します。
ms.openlocfilehash: 3ac4e9fedae66656d4dee2155c8a8dcbe9325970
ms.sourcegitcommit: f1d47655974a2f08e69704a9a0c46cb007e51589
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2020
ms.locfileid: "92903390"
---
# <a name="signing-in-to-visual-studio-subscriptions-with-your-work-or-school-account"></a>職場または学校アカウントを使用して Visual Studio サブスクリプションにサインインする 

Visual Studio サブスクリプションにサインインする手順は、ご使用のアカウントの種類に応じて変わります。  たとえば、Microsoft アカウント (MSA) または勤務先または学校で指定された電子メール アドレスを使用する場合があります。  2019 年 1 月から GitHub アカウントでも一部のサブスクリプションにサインインできるようになりました。 

この記事では、職場または学校から提供された電子メール アドレスを使用してサインインする手順について説明します。

## <a name="signing-in-with-your-work-or-school-account"></a>職場または学校アカウントでサインインする

1. [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) を参照してください。
2. 新しい Visual Studio サブスクリプションを割り当てたメール アドレスを入力します。

   > [!NOTE]
   > このアドレスは、受信したサブスクライバー宛てのウェルカム メールにも示されています。 ウェルカム メールが見つからない場合は、迷惑メール フォルダーを確認してください。

3. **[続行]** をクリックします。
4. 会社のサインイン ページにリダイレクトされます。
5. パスワードを入力します。
6. **[サインイン]** をクリックします
7. この時点で、"特典" ページが表示されます。

ポータルの上部の青いバーに、使用しているサブスクリプションの種類が表示されます。

右上のユーザー名の下で、現在選択されているサブスクリプションも確認できます。  "表示中:" の後にサブスクリプションが表示されます。  複数のサブスクリプションがある場合は、ドロップダウン矢印をクリックして、使用するサブスクリプションを選択できます。

## <a name="using-your-microsoft-account-msa-to-sign-in-to-a-work-or-school-account"></a>Microsoft アカウント (MSA) を使用して職場または学校アカウントにサインインする

1. [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) に移動します。
2. 新しい Visual Studio サブスクリプションを割り当てたメール アドレスを入力します。

   > [!NOTE]
   > このアドレスは、サブスクライバー宛てのウェルカム レターにも示されています。 ウェルカム レターを受け取っていない場合は、迷惑メール フォルダーを確認してください。

3. **[続行]** をクリックします。
4. 決定ページにリダイレクトされます。
    - Azure Active Directory (AAD) テナントに関連付けられた "職場または学校" アカウントにサブスクリプションが割り当てられている場合は、 **[Work or school account]\(職場または学校アカウント\)** を選びます。
    - サブスクリプションが "会社" のメール アドレスに関連付けられている場合でも、"個人" の Microsoft アカウント (MSA) にも変換されている場合は、 **[Personal]\(個人\)** を選択します。

        > [!NOTE]
        > 過去に Visual Studio サブスクリプション (旧 MSDN) を使用していた多くのサブスクライバーがこれに当てはまります。

    - 1 つの経路に失敗した場合は、別の経路を試します。  サブスクリプション管理者によってサブスクリプションが変更されている場合があります。

5. パスワードを入力します。
6. **[サインイン]** をクリックします。
7. この時点で、"特典" ページが表示されます。

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q--im-unable-to-sign-in-using-my-work-or-school-email-address"></a>Q:職場または学校のメール アドレスを使用してサインインできません。  
A: サインインの問題の最も一般的な原因は、サブスクリプションに関連付けられているアカウントとは異なるアカウントを使用してサインインしようとしている場合です。  複数の異なるメール アドレスを使っている場合、間違ったメール アドレスを使ってサインインしようとしている可能性があります。  別のアドレスでサインインしてみてください。  それでもうまくいかない場合は、[サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/) チームまでお問い合わせください。  

### <a name="q--i-cant-see-my-subscription-where-is-it"></a>Q:サブスクリプションを表示できません。 場所はどこなのか。
A: 多くのユーザーが、複数のサブスクリプションを持っています。  [https://my.visualstudio.com](https://my.visualstudio.com ) でサブスクリプション ポータルにサインインできても、サブスクリプションが表示されない場合は、次の 2 つの一般的な原因があります。
1. 異なる Microsoft アカウントでログインしています。  複数のサブスクリプションをお持ちで (Professional または Enterprise サブスクリプションと、Visual Studio Dev Essentials メンバーシップなど)、それらが異なるメール アドレスに関連付けられている可能性があります。 他のサブスクリプションを表示するには、いったんサインアウトし、他の MSA を使ってもう一度サインインしてください。
2. 同じメール アドレスに複数のサブスクリプションが関連付けられています。  メール アドレスに関連付けられているすべてのサブスクリプションを表示するには、 https://my.visualstudio.com/subscriptions にアクセスして、使用するサブスクリプションを選択します。 

それでも問題が解消しない場合は、[サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/) チームまでお問い合わせください。  

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次の手順
サブスクリプション ポータルに正常にサインインしたら、特典ページ (https://my.visualstudio.com/benefits ) にアクセスし、お客様が利用できる優れたツール、サービス、オファーを調査することをお勧めします。