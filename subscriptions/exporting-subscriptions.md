---
title: サブスクリプション情報のエクスポート | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 02/20/2020
ms.topic: conceptual
description: サブスクライバーの一覧とサブスクリプションの割り当ての詳細をエクスポートする方法について説明します。
ms.openlocfilehash: ddf466e314190b8c91d35aad522da14f4c4af69f
ms.sourcegitcommit: 3c105990656cd509062ce60e52e776c794f6305d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77520853"
---
# <a name="export-subscription-information"></a>サブスクリプション情報のエクスポート
Visual Studio サブスクリプションの[管理ポータル](https://manage.visualstudio.com)では、サブスクライバーの一覧とその割り当てに関する詳細情報をエクスポートできます。 この情報には、名前、メール アドレス、連絡用メール アドレス、サブスクリプション レベル、割り当て日、ライセンス認証の状態、有効期限、参照フィールド、ダウンロードが有効であるかどうか、国、言語、サブスクリプションの状態、サブスクリプション GUID が含まれます。  一覧は CSV ファイルとしてエクスポートされ、Microsoft Excel で簡単に開いて、グラフやピボットなどの成果物を作成することができます。

すべてのサブスクライバー情報を 1 か所にまとめておくと、次のようなことができます。
- 組織内のチームや場所で使用されているサブスクリプションを全体的に把握する。
- 将来のサブスクリプション購入のための計画と予算を開発する。 
- サブスクリプションを割り当てられているユーザーにアクティブ化を促す。
- サブスクリプションの有効期限が切れる前に事前アクションを実行する。  
- サブスクリプションの割り当て超過の可能性がある部分を特定する。 

## <a name="export-your-subscriptions"></a>サブスクリプションをエクスポートする
エクスポートを実行するには、次の手順に従います。
1. [管理ポータル](https://manage.visualstudio.com)にサインインします。
2. **[エクスポート]** タブを選択します。ファイルがローカル コンピューターにダウンロードされます。 このファイルには、ユーザー サブスクリプションを含む割り当ての名前と、エクスポートの日付が含まれます。
> [!div class="mx-imgBorder"]
> ![サブスクライバーのエクスポート](_img/exporting-subscriptions/exporting-subscriptions.png)

## <a name="next-steps"></a>次の手順
- サブスクリプションの管理の詳細な情報については、次の詳細なトピックをご覧ください。
    - [有効期限が切れたサブスクリプションに対応する](handle-expired-license.md)
    - [超過](handle-overclaimed-license.md)
    - [最大使用量](maximum-usage.md)
- サブスクリプションの管理に関するさまざまな側面についてサポートが必要ですか?  [Visual Studio の管理とサブスクリプションのサポート](https://visualstudio.microsoft.com/support/support-overview-vs)にお問い合わせください。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)
