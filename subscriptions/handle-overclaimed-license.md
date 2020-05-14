---
title: ライセンスの割り当て超過への対処 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: a747100c-6f08-41a4-aaad-05099741742b
ms.date: 03/03/2020
ms.topic: conceptual
description: サブスクリプションの割り当て超過を管理者が解決する方法について説明します
ms.openlocfilehash: a4cdab7d4e6e5925bab3d4dc7c800dc33ef6d713
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80232450"
---
# <a name="overallocated-subscriptions"></a>サブスクリプションの割り当て超過
サブスクライバーを追加した後に、注文が変更される場合があります。これにより会社が所有するライセンス数よりも割り当てられたサブスクリプションが多くなる場合があります。 これは "割り当て超過" と呼ばれています。  

ご利用のサブスクリプションの割り当てを表示するには、左上にあるアイコンをクリックして、割り当てウィンドウを開きます。  

> [!NOTE]
> Open License プログラムでは割り当て超過は許可されません。  また、他のプログラムでは、ポータルにこの情報を別の方式で表示できます。
>
> [!div class="mx-imgBorder"]
> ![過剰に要求されたサブスクリプションの通知](_img/over-claimed/over-claimed-alert.png)

表示ではハッシュされたバーを使用して、サブスクリプションの割り当て超過が示されていることに注目してください。  すべてのサブスクリプションの種類全体での割り当て超過の数は、上部の [概要] セクションにあります。また、サブスクリプション レベルごとに、固有の割り当て状態も表示されます。  

## <a name="resolve-overallocated-subscriptions"></a>サブスクリプションの割り当て超過を解決する
割り当て超過を解決するには、次のようにいくつかの方法があります。
- 再販業者に連絡して追加のサブスクリプションを購入します。
- 年次補正期間まで待って、その時点で割り当て超過のサブスクリプションの支払いを行います。 
- 一部のサブスクリプションの割り当てを削除します  (この場合、補正は年度の任意の時点で割り当てられたサブスクリプション最大数に基づいているため、年次補正の時点で支払いが必要になります)。

## <a name="billing-and-true-up"></a>課金とトゥルーアップ
組織に Enterprise Agreement (EA) がある場合、管理者はサブスクリプションを購入せずに割り当てて、後で "トゥルーアップ" と呼ばれる調整プロセスを通して支払うことができます。  割り当て超過が生じると、組織は、"トゥルーアップ" 中にユーザーに割り当てられているサブスクリプションの最大数に対して課金されます。  トゥルーアップの実行時に割り当てられているサブスクリプションが最大数未満になっている場合でも、このことは当てはまります。  最大使用量の監視の詳細については、[最大使用量](maximum-usage.md)に関するトピックを参照してください。

> [!Important]
> Visual Studio Subscriptions with GitHub Enterprise が Visual Studio サブスクリプション管理者によって割り当てられていて、これらのサブスクリプションが一度も購入されていない場合、これらは組織内の GitHub Enterprise 管理者に対して表示されません。 GitHub Enterprise サブスクリプションが表示されるようにするには、最初にサブスクリプションが割り当てられたときに、Visual Studio Professional with GitHub Enterprise または Visual Studio Enterprise with GitHub Enterprise の**少なくとも 1 つの**サブスクリプションを含む購入を行う必要があります。
>
> 割り当てられている GitHub サブスクリプションごとに、このサブスクリプションのライセンス要件への準拠を維持するために、お客様の責任下で、管理ポータルで対応する Visual Studio with GitHub サブスクリプションが割り当てられていることを確認する必要があります。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
- [Visual Studio Subscriptions with GitHub Enterprise](assign-github.md) の管理に関する詳細情報をご覧ください。
- Visual Studio サブスクリプションの販売、サブスクリプション、アカウント、課金のサポートについては、Visual Studio [サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/)にお問い合わせください。