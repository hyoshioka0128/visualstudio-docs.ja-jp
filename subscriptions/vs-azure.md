---
title: Microsoft Azure 特典 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 872c5746-5357-4764-949b-aa525a0adf1a
ms.date: 04/28/2020
ms.topic: conceptual
description: Visual Studio サブスクリプションに含まれる Azure DevTest の個人クレジットの特典をアクティブ化する方法を説明します。
ms.openlocfilehash: 50e784a60dc50232bc390233e2ad80dc91d0f4ab
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183614"
---
# <a name="use-microsoft-azure-in-visual-studio-subscriptions"></a>Visual Studio サブスクリプションで Microsoft Azure を使用する
Visual Studio サブスクライバーは、追加料金なしで Microsoft Azure を使うことができます。  [月単位の Azure DevTest の個人クレジット](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)で、Azure が開発/テストのための個人用サンドボックスになります。  仮想マシン、クラウド サービス、その他の Azure リソースをプロビジョニングできます。  クレジットの額はサブスクリプションのレベルによって異なります。

## <a name="activation-steps"></a>アクティブ化の手順
1. [https://my.visualstudio.com/benefits](https://my.visualstudio.com/benefits?wt.mc_id=o~msft~docs) にサインインします。

2. [特典] ページの [ツール] セクションで、Azure のタイルを見つけて、特典タイルの下部にある **[ライセンス認証]** リンクをクリックします。
   > [!div class="mx-imgBorder"]
   > ![Azure タイル](_img/vs-azure/vs-azure-tile.png)

3. 既存の Azure サブスクリプションがない場合は、必要な情報を入力して Azure サブスクリプションを作成するように求められます。  最初の手順は、ご自分の個人情報を入力してから、 **[次へ]** をクリックすることです。
   > [!div class="mx-imgBorder"]
   > ![Azure のサインアップ](_img/vs-azure/vs-azure-about-you.png)

4. 次に、簡単な確認コードを使用して本人確認を行う必要があります。 電話番号を入力し、コードをテキストで受け取るか、または電話で受け取るかを選択します。  受け取ったコードを入力して、 **[コードの確認]** をクリックします。   
   > [!div class="mx-imgBorder"]
   > ![Azure 準備作業](_img/vs-azure/vs-azure-identity.png)

5. 最後の手順として、チェックボックスをオンにして使用条件に同意した後、 **[サインアップ]** をクリックします。  必要な作業は以上です。
   > [!div class="mx-imgBorder"]
   > ![Azure 準備作業](_img/vs-azure/vs-azure-agreement.png)

0. Azure ダッシュボードのクイック スタート センターが読み込まれます。  
   > [!div class="mx-imgBorder"]
   > ![Azure ダッシュボード](_img/vs-azure/vs-azure-quick-start.png) 

0. 後で簡単にアクセスできるように、[Azure portal](https://portal.azure.com) をブックマークします。

## <a name="maintain-a-subscription-to-use-monthly-credits"></a>月単位のクレジットを使用するサブスクリプションを保守する
Visual Studio サブスクリプションの有効期限が切れた場合、または削除された場合、毎月の Azure  Dev/Test の個別クレジットを含め、すべてのサブスクリプション特典が利用できなくなります。 毎月のクレジットで Azure の使用を続けるには、サブスクリプションを更新するか、新しいサブスクリプションを購入するか、Azure の Dev/Test の個別クレジットが含まれる有効なサブスクリプションに Azure 特典を移す必要があります。  

> [!IMPORTANT]
> 現在の Azure サブスクリプションが無効になるか、データにアクセスできなくなる前に、リソースを別の Azure サブスクリプションに移す必要があります。  

Azure の毎月のクレジットは、いくつかの方法で引き続きご利用いただけます。  Azure リソースを保存するには、下で選択したアクションに関係なく、別の Azure サブスクリプションに[リソースを移す](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription)必要があります。 

- **Visual Studio サブスクリプションを直接購入する場合**、Microsoft Store で新しいサブスクリプションを購入するか、サブスクリプションを更新します。  
    - [Visual Studio Enterprise](https://www.microsoft.com/p/visual-studio-enterprise-subscription/dg7gmgf0dst4?activetab=pivot%3aoverviewtab)
    - [Visual Studio Professional](https://www.microsoft.com/p/visual-studio-professional-subscription/dg7gmgf0dst3?activetab=pivot%3aoverviewtab)
    - [Visual Studio Test Professional](https://www.microsoft.com/p/visual-studio-test-professional-subscription/dg7gmgf0dst6?activetab=pivot%3aoverviewtab)
- **組織の誰かが代表してサブスクリプションを購入する場合**、[Visual Studio サブスクリプションの管理者に問い合わせ](https://docs.microsoft.com/visualstudio/subscriptions/contact-my-admin)、必要な毎月のクレジットが与えられるサブスクリプションを要求してください。  
- 別の Microsoft アカウントに関連付けられている同じサブスクリプション レベルで**別の Visual Studio サブスクリプションがアクティブになっている**場合、Visual Studio [サブスクリプション ポータル](https://my.visualstudio.com/subscriptions)で[代替アカウントを追加する](https://docs.microsoft.com/visualstudio/subscriptions/manage-vs-subscriptions#managing-my-profile)ことで、別の有効な Visual Studio サブスクリプションに Azure 特典を移すことができます。  

以下の適格性テーブルを使用して、各サブスクリプションの種類に含まれるクレジットの数を確認してください。  


## <a name="convert-your-azure-subscription-to-pay-as-you-go"></a>Azure サブスクリプションを従量課金制に変換する

Visual Studio のサブスクリプションまたはクレジットは不要になったものの、Azure リソースを引き続きご利用になる場合は、別の Azure サブスクリプションに[リソースを移して](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription)ください。あるいは[使用制限をなくし](https://docs.microsoft.com/azure/cost-management-billing/manage/spending-limit#remove-the-spending-limit-in-azure-portal)、Azure サブスクリプションを従量課金制に変更してください。 

いずれの措置も行わない場合、電子メールの通知を受信してから 30 日後にご利用の Azure サブスクリプションが無効になり、削除されます。  

## <a name="have-a-question"></a>質問はございますか?
リソースの移動、使用制限の削除、あるいは Azure に関するその他のトピックに関して質問がございましたら、Azure portal で [Azure サポート要求を提出](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)することができます。 

## <a name="eligibility"></a>特典を受ける条件
|                 サブスクリプション レベル/プログラム                 |           特長           |                         更新可能かどうか                          |
|--------------------------------------------------------------|-----------------------------|-------------------------------------------------------------|
|              Visual Studio Enterprise Standard               |     150 ドルのクレジット/月     |                             はい                             |
|              Visual Studio Enterprise with GitHub Enterprise               |     150 ドルのクレジット/月     |                             はい                             |
|               Visual Studio Enterprise - 月間プラン               |        使用できません        |                                                             |
|             Visual Studio Professional Standard              |     50 ドルのクレジット/月      |                             はい
|              Visual Studio Professional with GitHub Enterprise              |     150 ドルのクレジット/月     |                             はい                             |
|              Visual Studio Professional - 月間プラン              |        使用できません        |                                                             |
|                    Visual Studio Test Pro                    |     50 ドルのクレジット/月      |                             はい                             |
|                        MSDN Platforms                        |     100 ドルのクレジット/月     |                             はい                             |
|               Visual Studio Enterprise - NFR\*               |     150 ドルのクレジット/月     |                             はい                             |
|                Visual Studio Enterprise - FTE                |     150 ドルのクレジット/月     |                             はい                             |
|     Visual Studio Enterprise - Microsoft Partner Network     |     150 ドルのクレジット/月     |                             はい                             |
|    Visual Studio Professional - Microsoft Partner Network    |        使用できません        |                                                             |
|        Visual Studio Enterprise – Imagine (Standard)         |        使用できません        |                                                             |
|         Visual Studio Enterprise – Imagine (Premium)         |        使用できません        |                                                             |
|             Visual Studio Enterprise – BizSpark              |     150 ドルのクレジット/月     |                             はい                             |
|      Visual Studio Enterprise – MCT Software & Services      |     100 ドルのクレジット/月     |                             はい                             |
| Visual Studio Enterprise – MCT Software & Services Developer |     150 ドルのクレジット/月     |                             はい                             |

\* Not for Resale (NFR)、Most Valuable Professional (MVP)、Regional Director (RD)、Visual Studio Industry Partner (VSIP) が含まれます。

> [!NOTE]
> Microsoft では、クラウド サブスクリプションの Visual Studio Professional 年間サブスクリプションおよび Visual Studio Enterprise 年間サブスクリプションが提供されなくなりました。 サブスクリプションの更新、増減、キャンセルに関する既存のお客様のエクスペリエンスと機能については変更はありません。 新規のお客様は、[https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/) に移動し、Visual Studio のさまざまな購入オプションを調べることをお勧めします。

どのサブスクリプション使用しているかわからない場合は次の手順を実行してください。  [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions?wt.mc_id=o~msft~docs) に接続し、お使いのメール アドレスに割り当てられているすべてのサブスクリプションを確認します。 すべてのサブスクリプションが表示されない場合は、1 つ以上のサブスクリプションが別のメール アドレスに割り当てられている可能性があります。  それらのサブスクリプションを表示するには、そのメール アドレスを使用してサインインする必要があります。

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q-how-do-i-submit-a-technical-support-incident-from-within-the-azure-portal"></a>Q:Azure ポータル内からテクニカル サポート インシデントを送信するにはどうすればよいですか。
A: Azure ポータルからサポート インシデントを送信するには、3 段階の手順を行います。
1. テクニカル サポートの特典をアクティブ化し、契約 ID アクセス ID を取得します。
2. サポート契約を Azure サブスクリプションにリンクします。
3. サポート インシデントを送信します。

詳細については、[テクニカル サポート](vs-tech-support.md)のドキュメントを参照してください。

### <a name="q-how-owns-the-intellectual-property-i-create-using-my-azure-devtest-individual-credit"></a>Q:自分の Azure DevTest の個人クレジットを使用して作成した知的財産は、だれのものになりますか。
A: 従業員が生成した知的財産で、その会社が提供するリソースに対して作成されたものは、そのリソースを提供する会社の知的財産となります。 したがって、お客様がご自分の雇用主から Visual Studio サブスクリプションを受け取った場合は、その知的財産のポリシーが適用されます。 

## <a name="support-resources"></a>サポート リソース
- Azure に関するヘルプが必要ですか。  以下のリソースを確認してください。
  - テクニカル サポート: [https://azure.microsoft.com/support/options/](https://azure.microsoft.com/support/options/)
  - [Azure のヒントとコツ](https://microsoft.github.io/AzureTipsAndTricks/ "Azure のヒントとコツ") 
- Visual Studio サブスクリプションの販売、サブスクリプション、アカウント、課金のサポートについては、Visual Studio [サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/)にお問い合わせください。
- Visual Studio IDE、Azure DevOps Services、またはその他の Visual Studio の製品やサービスに関する質問がありますか。  [Visual Studio のサポート](https://visualstudio.microsoft.com/support/)にアクセスしてください。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
Microsoft のツールとサービスの詳細については、次のドキュメントを参照してください。
- [Azure](/azure/)
- [Azure DevOps](/azure/devops/)
- [Visual Studio IDE](/visualstudio/)
