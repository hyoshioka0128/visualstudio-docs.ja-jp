---
title: 管理ポータルの最大使用量機能を使用する
author: evanwindom
ms.author: lank
manager: lank
ms.date: 03/24/2019
ms.topic: conceptual
description: 割り当てられているサブスクリプションの最大数を管理ポータルで表示する方法について説明します
ms.openlocfilehash: 76360c9843d82350a2b9929b8debfdb4aa4cde82
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852339"
---
# <a name="use-the-maximum-usage-feature-to-track-the-number-of-assigned-subscriptions"></a>最大使用量機能を使用して割り当てられているサブスクリプション数を追跡する
Visual Studio のサブスクリプション管理ポータルの新機能を使用すると、購入して割り当てたサブスクリプション数を追跡し、過去 1 年間と全契約期間の割り当てた各レベルのサブスクリプションのピーク数を特定できます。 

## <a name="view-your-maximum-usage"></a>最大使用量を表示する
任意の契約およびサブスクリプション レベルに割り当てられているサブスクリプションのピーク数を確認するには、次の手順を行います。
1. ポータルの左上のドロップダウンで、表示する契約を選択します (契約が 1 つしかない場合は、最初から選択されています)。
2. **[Maximum Usage]\(最大使用量\)** タブをクリックします。  
    > [!div class="mx-imgBorder"]
    > ![[Maximum Usage]\(最大使用量\) メニュー](_img/maximum-usage/maximum-usage-menu.png)
3. [Maximum Usage Summary]\(最大使用量の概要\) が表示され、過去 1 年間に各レベルに割り当てたサブスクリプションの最大数とそのピークに達した日付が表示されます。  複数回ピークに達した場合は、最初に達したときが表示されます。 
    > [!div class="mx-imgBorder"]
    > ![[Maximum Usage Summary]\(最大使用量の概要\) メニュー](_img/maximum-usage/maximum-usage-summary.png)
4. 契約期間中に割り当てられた最大サブスクリプション数を確認するには、 **[Full-Term]\(全期間\)** タブをクリックします。

## <a name="view-your-assignment-history"></a>割り当て履歴を表示する
各サブスクリプション レベルのピークの割り当てを確認するだけでなく、 **[Export full report]\(完全なレポートのエクスポート\)** ボタンをクリックして、購入や割り当てを含む契約上のアクティビティの現在のアカウントを確認できます。  

> [!div class="mx-imgBorder"]
> ![最大使用量の完全なレポート](_img/maximum-usage/maximum-usage-full-report.png)

サブスクリプション レベルごとに、レポートには、新しい最大割り当てレベルに達した日付と、その日の時点で購入済みのサブスクリプション数が表示されるので、超過割り当てがあった日付を簡単に確認できます。  

たとえば、上の表では、2018 年 12 月 13 日の契約には 123 個の Visual Studio Enterprise サブスクリプションがあり、120 個が割り当てられていることがわかります。  2019 年 1 月 8 日には、もう 1 つのサブスクリプションが割り当てられ、合計が 121 個になりました。  翌日、さらに 6 個のサブスクリプションが割り当てられ、新しい割り当てに対応するためにさらに 4 個のサブスクリプションが契約に追加されました。  

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q-how-is-the-information-in-the-maximum-usage-different-from-the-assignment-information-available-in-the-overview-section-on-the-left-side-of-the-portal"></a>Q:最大使用量の情報は、ポータルの左側の [概要] セクションに表示される割り当て情報とどのように異なりますか。
A: 概要の情報には、*現在*の割り当てと、各契約レベルで使用できるサブスクリプションが表示されます。  これは、現在の年度または契約期間中に契約に割り当てられた最大サブスクリプション数とは大きく異なる場合があります。  最大使用量機能を使用すると、最大割り当てレベルに達した時期とそのレベルを確認できます。  この点は重要な違いです。調整中のサブスクリプションに対する請求は、1 年間の任意の時点で割り当てられた最大サブスクリプション数に基づいているためです。 

## <a name="resources"></a>リソース
- [Visual Studio ライセンスのホワイト ペーパー](https://visualstudio.microsoft.com/wp-content/uploads/2019/06/Visual-Studio-Licensing-Whitepaper-May-2019.pdf)
- [Visual Studio の管理とサブスクリプションのサポート](https://visualstudio.microsoft.com/support/support-overview-vs)
- [ボリューム ライセンスの契約条件](https://www.microsoft.com/licensing/product-licensing/products.aspx)

## <a name="next-steps"></a>次の手順
- サブスクリプションの割り当てや管理ポータルのその他の側面について不明な点がある場合は、 https://visualstudio.microsoft.com/subscriptions/support/ にお問い合わせください。 
- 購入した数よりも多くのサブスクリプションを割り当てた場合の対処方法の詳細については、[割り当て超過](handle-overclaimed-license.md)に関するページを参照してください。
