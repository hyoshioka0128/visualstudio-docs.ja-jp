---
title: Visual Studio サブスクライバー データの匿名化 | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: ce5fc8a4-484c-4df6-97c3-cb60174fb66b
ms.date: 03/11/2021
ms.topic: conceptual
description: サブスクリプションへのアクセスを喪失したときに、サブスクライバー データがどのように匿名化されるかについて説明します。
ms.openlocfilehash: 69f41232a678a857908b30d63df2ae7f72b79904
ms.sourcegitcommit: 9da787bf5b4281f933dc22083dc0bdeae3bc9461
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2021
ms.locfileid: "103225964"
---
# <a name="anonymization-of-visual-studio-subscriber-information"></a>Visual Studio サブスクライバー情報の匿名化
サブスクライバーのサブスクリプションの使用をブロックするイベント (サブスクリプションの有効期限切れやサブスクライバーのサインイン アカウントの削除など) が発生すると、名前やサインイン アカウントなどのユーザーの個人情報は、基本的にスクランブルされ、使用できなくなります。  これは、サブスクライバーの個人情報を保護するために実行されます。

[!INCLUDE [GDPR-related guidance](includes/gdpr-intro-sentence.md)]

## <a name="when-does-anonymization-occur"></a>匿名化が行われるタイミング
サブスクライバーがサブスクリプションを使用できなくなると、匿名化がトリガーされます。  匿名化が行われるタイミングは、サブスクリプションとトリガー起動イベントの種類によって異なります。 詳細については、以下の表を参照してください。

| サブスクリプションの種類                                                                                                                       | 匿名化をトリガーするイベント                                                                                                     | 匿名化が発生するタイミング |
|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|---------------------------|
| Visual Studio Dev Essentials                                                                                                            | サブスクライバーがプログラムを止めるか、利用規約に同意しない                                    | 30 日               |
| Microsoft Store (リテール) から購入した Visual Studio サブスクリプション                                                                      | サブスクリプションの有効期限が切れている、またはアクティブ化されていない                                                                   | 360 日                  |
| ボリューム ライセンス、Visual Studio Marketplace (クラウド サブスクリプション)、または MPN などのプログラムを通じて取得した Visual Studio サブスクリプション | サブスクリプションの有効期限が切れている、またはユーザーに割り当てられていない                                                          | 180 日                  |
| すべてのサブスクリプション                                                                                                                       | サブスクリプションにサインインするために使用されている Azure Active Directory アカウントまたは Microsoft アカウント (MSA) が終了している | 即時               |
| すべてのサブスクリプション                                                                                                                       | Azure Active Directory アカウントに関連付けられているテナントからサブスクライバーが削除される                                | 即時               |

## <a name="faq"></a>よくあるご質問
### <a name="q--does-the-anonymization-of-the-subscribers-personal-information-cause-them-to-lose-access-to-the-subscription"></a>Q:サブスクライバーの個人情報の匿名化により、サブスクリプションにアクセスできなくなりますか。
A: いいえ。  匿名化は、サブスクリプションへのアクセス権の喪失を引き起こすイベントへの応答で、アクセス権の不足を引き起こすことはありません。

### <a name="q--im-an-admin-for-my-organizations-subscriptions--if-one-of-my-subscribers-information-is-anonymized-can-that-subscription-be-reassigned-to-another-user"></a>Q:私は組織のサブスクリプションの管理者です。  組織内のサブスクライバーのうちの 1 人の情報が匿名化された場合、そのサブスクリプションを別のユーザーに再割り当てすることはできますか。
A: はい。  これらの条件が満たされた場合は、サブスクリプションを再割り当てできます。
- サブスクリプションの有効期限が切れていない
- サブスクリプションがサブスクライバーに最後に割り当てられてから、少なくとも 90 日が経過した。  たとえば、サブスクリプションが 6 月 1 日にサブスクライバーに割り当てられた場合、少なくとも 8 月 30 日までは、サブスクリプションを再割り当てすることはできません。

### <a name="q-how-can-i-prevent-anonymization-caused-by-deleting-a-sign-in-email-address"></a>Q:サインイン電子メール アドレスを削除することによって、匿名化の原因を防ぐ方法はありますか?
A: この問題を回避するには、次の 2 つの方法があります。
- 両方の ID 管理システムではなく、どちらか一方 (MSA または AAD) だけを配置します。  
- テナントを介して、AAD と MSA の ID を関連付けます。 

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次の手順
[MSA と AAD の ID を関連付け](/azure/active-directory/b2b/add-users-administrator)て、匿名化を回避する方法について学習します。