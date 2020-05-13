---
title: 接続済み Microsoft アカウントと Azure Active Directory ID を使用する方法 | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: lank
ms.assetid: 50ce0445-ef1a-4e92-b9d0-aebb2155a111
ms.date: 03/11/2020
ms.topic: conceptual
robots: noindex, nofollow
description: 接続済み Microsoft アカウントと Azure Active Directory ID を使用する方法について説明します
ms.openlocfilehash: b88c978f330520af62f51e372db93475b71caa36
ms.sourcegitcommit: eeff6f675e7850e718911647343c5df642063d5e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233175"
---
# <a name="how-to-use-connected-identities-in-visual-studio-subscriptions"></a>Visual Studio サブスクリプションで接続済み ID を使用する方法
職場または学校を介して Visual Studio サブスクリプションを受け取り、Microsoft アカウント (MSA) を使用してサインインする場合は、サブスクリプション管理者が組織の Azure Active Directory (Azure AD) の ID に MSA を接続できます。  これにより、サブスクリプションに含まれる特典の一部にアクセスする方法が変わります。 

## <a name="overview-of-connected-ids"></a>接続済み ID の概要
組織は Azure AD ベースの ID への移行をますます進めており、サブスクリプションの自動管理のセキュリティとサポートを強化しています。  サブスクリプションで @outlook.com やその他の個人用メール アドレスなどの MSA が使用されている場合は、管理者がサインインのメール アドレスを Azure AD ID に変更することがあります。  その結果、サブスクライバー ポータル (https://my.visualstudio.com ) にサインインする方法は変わりますが、すべての特典にアクセスする方法は変わらない可能性があります。  

管理者が MSA と Azure AD ID を接続すると、Visual Studio サブスクリプションへのアクセスに MSA ではなく Azure AD ID を使用するように通知するメールが送信されます。 

## <a name="how-to-access-benefits-using-azure-ad-identities"></a>Azure AD ID を使用して特典にアクセスする方法
管理者が MSA を Azure AD ID に接続した後、Azure AD に依存する特典にアクセスするには、Azure AD ID を使用してサブスクライバー ポータル (https://my.visualstudio.com ) にサインインする必要があります。  次の設定があります。
- Visual Studio IDE
- Azure DevOps
- Azure DevTest の個人クレジット

## <a name="how-to-access-benefits-using-your-msa"></a>MSA を使用して特典にアクセスする方法
Pluralsight、LinkedIn、CloudPilot など、Visual Studio サブスクリプションで提供される多くの特典については、パートナーの Web サイトでユーザー アカウントを実際に作成します。  このようなアカウントの場合、アカウントの作成時に使用した ID を引き続き使用する必要があります。  たとえば、MSA を使用して Pluralsight 特典をアクティブ化した場合、Pluralsight トレーニングを行うときは、サブスクライバー ポータルへのサインインに使用する ID とは関係なく、MSA を引き続き使用する必要があります。  

## <a name="use-an-alternate-identity-to-access-your-subscription"></a>別の ID を使用してサブスクリプションにアクセスする
Visual Studio サブスクリプションに代替アカウントを追加すると、サブスクリプションが割り当てられているものとは異なる ID を利用して、Azure DevOps や Azure などのサブスクリプションの特典にアクセスできます。 以前は、この機能は、Visual Studio (VS) サブスクリプションが Microsoft Account (MSA) に割り当てられた場合にのみ利用できました。 Azure Active Directory (Azure AD) でこの機能が職場や学校のアカウントにも使えるようになりました。  代替アカウントの使用方法の詳細については、[代替 ID](vs-alternate-identity.md) に関するページを参照してください。 

## <a name="frequently-asked-questions"></a>よく寄せられる質問
### <a name="q-how-can-i-contact-my-admin-about-this"></a>Q:管理者にこのことを問い合わせるにはどうすればよいですか?
A: 管理者に問い合わせる方法の詳細については、[サブスクリプション管理者への問い合わせ](contact-my-admin.md)に関するページを参照してください。  

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次の手順
管理者が Azure AD と MSA のアカウントを接続した後は、[サブスクリプション ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)に正常にサインインできることと、Azure DevOps、Visual Studio、Azure DevTest の個人クレジットなどの特典にアクセスできることを確認することをお勧めします。 