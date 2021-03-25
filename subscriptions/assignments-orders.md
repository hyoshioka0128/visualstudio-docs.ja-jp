---
title: Visual Studio サブスクリプションで割り当てを追跡し、注文を処理する | Visual Studio Marketplace
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 83a9162a-b9e7-43a4-b07f-6c1fd8580f78
ms.date: 03/21/2021
ms.topic: conceptual
description: ユーザーの割り当てを追跡して注文を処理する管理者の責任について説明します。
ms.openlocfilehash: 9ba54d13f4481f68d13e43a2e21f62036d23cab3
ms.sourcegitcommit: d7d9fb79448b3534923cc95071d1f91eabde88e8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2021
ms.locfileid: "104776988"
---
# <a name="track-user-assignment-and-process-orders"></a>ユーザーの割り当てを追跡し、注文を処理する
Visual Studio サブスクリプションの管理者は、Visual Studio の使用状況を追跡し、ボリューム ライセンス契約またはマイクロソフト製品/サービス契約に記載されているスケジュールに従って、使用率の増加に応じて注文を処理する必要があります。 新しい Visual Studio サブスクリプション管理ポータルは、使用可能なライセンスと使用済みのライセンスを示す便利なトラッカーにより、これを簡略化します。

## <a name="maximum-usage"></a>最大使用量
**次の場合には、会社が Visual Studio サブスクリプションをすぐに購入する義務が生じます。**
- ユーザーにライセンスが割り当てられた場合、**または**
- ユーザーが Visual Studio ソフトウェアと対話する場合

完全な購入義務は、ユーザーに割り当てられたサブスクリプションの最大数によって決まります。 このレベルのサブスクリプションの割り当ては、日割りユーザーあたりと、Visual Studio ソフトウェアを使用している個人を比べたときの、いずれか高い方のポイントになります。

- Visual Studio サブスクリプションを割り当てるユーザーを増やすと、最大使用レベルが上がります。  
- Visual Studio サブスクリプション管理者は、個人に割り当てられたサブスクリプション レベルを変更できます。これは 1 つの割り当てを減らして別の割り当てを増やすことになります。 あるサブスクライバーの割り当てられたサブスクリプション レベルを下げた場合は、そのサブスクライバーは直ちに使用を停止し、上位レベルのサブスクリプションでのみ許可されているすべてのものをアンインストールする必要があります。 
- Visual Studio サブスクリプション管理者は、元の割り当て時から 90 日間が経過している場合は、あるサブスクライバーから別のサブスクライバーにサブスクリプションを再割り当てすることができます。 
    > [!NOTE]
    > 人為的な高い最大使用レベルを回避するため、これを行う場合は常に既存のサブスクリプションをまず削除してから新しいサブスクリプションを追加します。 
- 組織の最大使用量の監視を支援するため、Visual Studio の[サブスクリプション管理ポータル](https://manage.visualstudio.com)には[最大使用量レポート](maximum-usage.md)があります。 

## <a name="monthly-subscriptions-open-license-or-open-value"></a>月間サブスクリプション、Open License、Open Value
サブスクリプションは、Open License や Open Value のようなプログラムから、あるいは Visual Studio Marketplace から月単位で割り当てることがあります。 その場合は、ユーザー (従業員または外部請負業者) が Visual Studio のライセンス付与されたソフトウェアと対話を開始する月の間に、注文を処理しなければならないユーザーが増えます。

## <a name="enterprise-mpsa-and-select-agreements"></a>Enterprise、MPSA、Select 契約
Microsoft Enterprise Agreements (EA)、MPSA および Select Plus 契約では、長期にわたる Visual Studio ソフトウェアの使用とライセンスの柔軟性が得られます。 Visual Studio 管理者は、ソフトウェア ライセンスが契約期間中に定められた最大使用率になるように年間の調整注文を行う必要があります。

## <a name="resources"></a>リソース
- ヘルプが必要ですか?  [サブスクリプション サポート](https://aka.ms/vsadminhelp)にお問い合わせください。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次のステップ
管理者の責任について詳しくは、以下をご覧ください。
- [管理者の責任](admin-responsibilities.md)
- [運用前環境のインベントリ](admin-inventory.md)
- [大規模なチームと外部請負業者を管理する](manage-teams.md)
- [最大使用量](maximum-usage.md)を使用して購入コミットメントを追跡する