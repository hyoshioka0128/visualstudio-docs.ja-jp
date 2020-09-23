---
title: Visual Studio のビジュアル クラウド サブスクリプションの請求に関する FAQ | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 21e0471d-ad59-4d21-9c6f-13f7147569af
ms.date: 09/08/2020
ms.topic: conceptual
description: クラウド サブスクリプションの請求に関する質問。
ms.openlocfilehash: ae99e6e843636efc6d81a0c4feebfd3e306f6319
ms.sourcegitcommit: 09d1f5cef5360cdc1cdfd4b22a1a426b38079618
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "91006005"
---
# <a name="visual-studio-cloud-subscriptions-billing-faq"></a>Visual Studio クラウド サブスクリプションの請求に関してよくあるご質問
必ず[クラウド サブスクリプションの特典と価格を比較](https://visualstudio.microsoft.com/vs/pricing/)して、各 Visual Studio サブスクリプションの特典、クラウドと標準の Visual Studio サブスクリプションの比較、サブスクライバー特典の詳細などを理解してください。

## <a name="general-purchasing-questions"></a>一般的な購入に関する質問
### <a name="q-can-i-buy-visual-studio-cloud-subscriptions-using-a-purchase-order"></a>Q:発注書を使って Visual Studio クラウド サブスクリプションを購入することはできますか。
A: いいえ。 すべての Visual Studio クラウド サブスクリプションは、Azure サブスクリプションを使って購入する必要があります (Azure 請求先アカウントとお考えください)。

### <a name="q-what-types-of-azure-subscriptions-can-be-used-to-buy-visual-studio-cloud-subscriptions"></a>Q:Visual Studio クラウド サブスクリプションの購入にはどのような種類の Azure サブスクリプションを使うことができますか。
A: ほとんどの Azure サブスクリプションを使うことができます。お使いの [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/) と接続した Azure サブスクリプション、Cloud Solution Providers (CSP) によって設定された Azure サブスクリプション、Microsoft オープン ライセンス リセラーによって設定された Azure サブスクリプション、従量課金制 Azure サブスクリプションがサポートされています。

[Azure 無料試用版](https://azure.microsoft.com/pricing/free-trial/)や Visual Studio サブスクリプションのサブスクライバー特典として含まれているサブスクリプションなど、一部の種類の Azure サブスクリプションは使用できません。

### <a name="q-am-i-required-to-buy-other-azure-services"></a>Q:他の Azure サービスを購入する必要はありますか。
A: まったくありません。 Azure で Visual Studio クラウド サブスクリプションだけを購入したい場合は、そうすることができます。

## <a name="enterprise-agreement-ea-customers"></a>Enterprise Agreement (EA) のお客様
### <a name="q-can-i-use-an-enterprise-agreement-to-buy-visual-studio-cloud-subscriptions"></a>Q:Enterprise Agreement を使って、Visual Studio クラウド サブスクリプションを購入できますか。
A: はい、できます。 お使いの EA 用に作成された Azure サブスクリプションに対して共同作成者以上のロールが与えられている必要があります。 Visual Studio クラウド サブスクリプションの購入は、Visual Studio Marketplace 内で直接行うようにしてください。 発注書を使って Visual Studio クラウド サブスクリプションを購入することはできません。

### <a name="q-how-can-i-tell-whether-i-have-the-necessary-privileges-to-buy-services-in-the-visual-studio-marketplace-through-my-organizations-enterprise-agreement"></a>Q:組織の Enterprise Agreement を使って Visual Studio Marketplace でサービスを購入するために必要な特権があるかどうかは、どうすれば確認できますか。
A: 適切な特権があるかどうかを確認する最も簡単な方法は、Visual Studio Marketplace で提供されているサービスの **[購入]** ボタンを選択してみることです。
お使いのログインに現在リンクされている Azure サブスクリプションの一覧が表示されるので、そこから Azure サブスクリプション (請求先アカウント) を選ぶ必要があります。
Azure サブスクリプションの名前として既定で表示される種類は請求先アカウント ("従量課金制"、"Enterprise Agreement" など) なので、通常、Azure サブスクリプションが Enterprise Agreement の一部かどうかは明白です。

もう 1 つの方法は、[Azure Enterprise Portal](https://ea.azure.com) にアクセスしてみることです。  正常にアクセスできる場合、エンタープライズ管理者ロールまたはアカウント所有者ロールを既に持っています。 Enterprise Agreement で新しい Azure 請求先アカウントを設定できるのは、アカウント所有者だけです。 Azure Enterprise Portal にアクセスできない場合は、組織のエンタープライズ管理者を調べて、その管理者に Azure Enterprise Portal で自分をアカウント所有者として追加するよう依頼してください。  誰に頼めばよいかわからない場合は、[サポート チケットを送信](https://support.microsoft.com/supportrequestform/cf791efa-485b-95a3-6fad-3daf9cd4027c)して、連絡先情報を要求できます。  サポート チケットを送信するときは、組織の名前と、Enterprise Agreement の登録番号が必要です。

### <a name="q-can-i-use-the-azure-monetary-commitment-funds-from-my-enterprise-agreement-to-buy-visual-studio-cloud-subscriptions"></a>Q:Enterprise Agreement の Azure 年額コミットメント資金を使って、Visual Studio クラウド サブスクリプションを購入することはできますか。
A: いいえ、これらの前払い資金では、Visual Studio クラウド サブスクリプションを購入することはできません。 EA 用に作成された Azure サブスクリプションを選んで Visual Studio クラウド サブスクリプションを購入すると、料金は次の "超過分" 請求書に表示されます。 通常これは毎月発生しますが、一部の EA 顧客については、過去のルールにより、超過分請求書が数か月間発行されない可能性があります。 超過分請求書が発生しないで追加購入 (Azure 年額コミットメントの資金の対象ではない購入) できる量を知る必要がある場合は、EA のライセンス スペシャリストに問い合わせてください。

## <a name="how-charges-are-processed"></a>料金の処理方法
### <a name="q-how-are-monthly-cloud-subscription-charges-processed"></a>Q:**月間プラン**のクラウド サブスクリプション料金はどのように処理されますか。
A: 最初の購入時は、現在の月の残りの日数をカバーする日割り計算された数量を請求します。 たとえば、10 個の Visual Studio Professional クラウド サブスクリプション月間プランを 4 月 15 日に購入した場合、月の 50% (30 日の月の 15 日) が残っているため、5 ユニット分を請求します。
5 月 1 日およびそれ以降は毎月、ユーザーがキャンセルするまで、10 ユニット分が請求されます。

後で支払い数量を増やした場合も、現在の月の残りの日数について、増加ユニット分が日割りで請求されます。 したがって、1 個の Visual Studio Professional クラウド サブスクリプション月間プランを 5 月 10 日に追加購入した場合は、約 0.677 ユニット (5 月の 31 日間の残り 21 日分) が請求されます。

### <a name="q-how-are-annual-cloud-subscription-charges-processed"></a>Q:**年間プラン**のクラウド サブスクリプション料金はどのように処理されますか。
A: 購入ごとに、購入された全数量が直ちに請求されます。 料金は 1 年間に分散されず、日割り計算は行われません。 同じ年の異なる時期にクラウド サブスクリプション年間プランを購入した場合、サブスクリプションは異なる月に更新されます。 Microsoft ボリューム ライセンス契約の購入で一般に行われている方法とは異なり、お客様のすべてのクラウド サブスクリプション年間プランを同じ期間にすることはありません。

### <a name="q-how-do-cancelations-work"></a>Q:キャンセルはどのように行われますか。
A: Visual Studio クラウド サブスクリプションをキャンセルすると、自動更新がキャンセルされます。 サブスクリプションは通常の更新日まで継続した後、単に期限切れになります。
期限が切れると、Visual Studio サブスクライバーは、Visual Studio またはサブスクリプションからの他のすべての特典を使用できなくなります。

クラウド サブスクリプション月間プランでは、キャンセルは次の月の最初の日に有効になります。 クラウド サブスクリプション月間プランの一部だけをキャンセルする場合は、次の月の最初の日にユーザーを削除し、適切なユーザーが引き続きアクティブなサブスクリプションを割り当てられるようにしてください。

クラウド サブスクリプション年間プランの場合は、元の購入または最後の年間更新請求から 12 か月が経過した後の月の最初の日に有効になります。 たとえば、2018 年 1 月 3 日に Visual Studio Professional クラウド サブスクリプション年間プランを購入した場合、2019 年 2 月 1 日に次の年に自動的に更新されるまで、サブスクリプションはアクティブです。 2019 年 2 月 1 日から 2020 年 2 月 1 日までの間にキャンセルした場合、サブスクリプションは 2020 年 2 月 1 日に期限切れになります。 クラウド サブスクリプション年間プランのサブスクリプション年の途中でキャンセルした場合の払い戻しはありません。

### <a name="q-what-kind-of-volume-discounts-are-available-for-visual-studio-subscriptions"></a>Q:Visual Studio サブスクリプションに対してはどのようなボリューム ディスカウントを利用できますか。
A: サブスクリプションの*各タイプ内*で 6 番目以降のすべてのサブスクリプションについて、5% の割引を得られます。

* Visual Studio Professional - 月間プラン
* Visual Studio Professional - 年間プラン
* Visual Studio Enterprise - 月間プラン
* Visual Studio Enterprise - 年間プラン

たとえば、6 個の Visual Studio Professional サブスクリプション月間プランと 5 個の Visual Studio Enterprise サブスクリプション月間プランを購入した場合、5 個の Professional サブスクリプションは通常料金、6 番目の Professional サブスクリプションは 5% のディスカウント料金、5 個の Enterprise サブスクリプションはすべて通常料金になります。

また、割引は、特定の月単位の請求期間内の料金に対してのみ適用されます。 したがって、ある月に 5 個の Visual Studio Professional サブスクリプション年間プランを購入し、次の月にさらに 5 個追加購入した場合、10 個のサブスクリプションすべてについて通常料金を支払います。

> [!NOTE]
> Microsoft では、クラウド サブスクリプションの Visual Studio Professional 年間サブスクリプションおよび Visual Studio Enterprise 年間サブスクリプションが提供されなくなりました。 サブスクリプションの更新、増減、キャンセルに関する既存のお客様のエクスペリエンスと機能については変更はありません。 新規のお客様は、[https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/) に移動し、Visual Studio のさまざまな購入オプションを調べることをお勧めします。

## <a name="other-questions"></a>その他の質問
### <a name="q-can-i-use-the-monthly-azure-devtest-individual-credit-as-a-visual-studio-subscriber-to-buy-more-visual-studio-cloud-subscriptions"></a>Q:Visual Studio サブスクライバーとして毎月の Azure DevTest の個人クレジットを使って、さらに Visual Studio クラウド サブスクリプションを購入できますか。
A: いいえ、Visual Studio サブスクライバーとして[月単位の Azure DevTest の個人クレジット](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)を使って、Visual Studio Marketplace での購入を支払うことはできません。 Visual Studio クラウド サブスクリプションのすべての購入は、クレジット カードに課金されます。
購入を行う前に、[使用制限を解除する](https://azure.microsoft.com/pricing/spending-limits/)必要があります。

### <a name="q-whats-the-difference-between-annual-and-monthly-cloud-subscriptions"></a>Q:クラウド サブスクリプションの年間プランと月間プランは何が違うのですか。
A: クラウド サブスクリプション月間プランには、Visual Studio に加えて Azure DevOps Services と TFS の使用が含まれます。 クラウド サブスクリプション年間プランにもこれらは含まれますが、それだけでなく、開発とテストを目的とするインストールと実行のための Windows および他の Microsoft ソフトウェアの使用、Azure サービスでの実験およびクラウドでの開発とテストのために使用できる月単位の Azure DevTest の個人クレジット、トレーニング、サポート、その他のサブスクライバー特典が含まれます。
[クラウド サブスクリプションの特典と価格を比較する](https://visualstudio.microsoft.com/vs/pricing/)

### <a name="q-do-i-get-new-versions-of-visual-studio-if-i-buy-a-visual-studio-cloud-subscription"></a>Q:Visual Studio クラウド サブスクリプションを購入した場合、新しいバージョンの Visual Studio を入手できますか。
A: はい。 新しいバージョンがリリースされたら、ダウンロードして実行できます。 さらに、以前のバージョンを引き続き実行することもできます。

### <a name="q-can-i-buy-visual-studio-cloud-subscriptions-from-my-software-reseller"></a>Q:ソフトウェア リセラーから Visual Studio クラウド サブスクリプションを購入することはできますか。
A: はい、リセラーがクラウド ソリューション プロバイダー (CSP) プログラムに加入している場合はできます。 リセラーにお問い合わせください。

## <a name="related-resources"></a>関連資料
- [Visual Studio サブスクリプション管理ポータル](https://manage.visualstudio.com/)
- [Visual Studio サブスクリプションのサポート](https://visualstudio.microsoft.com/vs/support/)
- [CSP 向けの Visual Studio クラウド サブスクリプションの購入](vscloud-csp.md)

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次の手順
クラウド サブスクリプションを今すぐ購入する
- [Visual Studio Professional - 月間プラン](https://marketplace.visualstudio.com/items?itemName=ms.vs-professional-monthly)
- [Visual Studio Enterprise - 月間プラン](https://marketplace.visualstudio.com/items?itemName=ms.vs-enterprise-monthly)