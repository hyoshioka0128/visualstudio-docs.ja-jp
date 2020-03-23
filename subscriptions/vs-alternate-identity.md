---
title: Visual Studio サブスクライバー向けの ID
author: evanwindom
ms.author: lank
manager: lank
ms.date: 07/19/2019
ms.topic: conceptual
description: Azure DevOps と Azure で使用するために Visual Studio サブスクリプションに代替 ID を追加する方法
ms.openlocfilehash: e19774f2314280b2e5a995a7d83336f1403682a4
ms.sourcegitcommit: f8e3715c64255b476520bfa9267ceaf766bde3b0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "72816560"
---
# <a name="identities-for-visual-studio-subscribers"></a>Visual Studio サブスクライバー向けの ID
Visual Studio サブスクリプションをアクティブ化すると、アクティベーション中に使用した ID (またはログイン) が Visual Studio サブスクリプションとリンクされます。 これにより、Microsoft は [Visual Studio サブスクライバー ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)、Azure DevOps、および Azure でユーザーを認識することができます。

Azure DevOps では、ユーザーがログインするたびに Visual Studio サブスクリプションの状態を確認し、登録している各組織内で自動的に機能を付与します。
これらの機能はサブスクライバーの特典に含まれているため、Visual Studio サブスクリプションにリンクされている ID を使用すれば、ユーザーは無料で任意の Azure DevOps 組織のメンバーとして追加されます。

Azure では、サブスクライバーの特典である[月単位の Azure DevTest の個人クレジット](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)をアクティブ化すると、Visual Studio サブスクリプションの状態が確認されます。

[Visual Studio サブスクライバー ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)内で、アクティベーション中に使用した ID に加えて、**代替 ID** を追加できる可能性があります。 サブスクリプションをアクティブ化するために Microsoft アカウントを使用した場合、代替 ID を追加することが許可されています。 このように、(Visual Studio、Office 365、または会社や学校のネットワークのログインに使用する) 職場または学校のアカウントを追加することもできます。これにより、個人用アカウントと職場または学校のアカウントの両方を使用して Azure DevOps にアクセスできるようになります。

## <a name="add-an-alternate-account-to-your-subscription"></a>サブスクリプションに代替アカウントを追加する
Visual Studio サブスクリプションに代替アカウントを追加すると、サブスクリプションが割り当てられているものとは異なる ID を利用して、Azure DevOps や Azure などのサブスクリプションの特典にアクセスできます。 以前は、この機能は、Visual Studio (VS) サブスクリプションが Microsoft Account (MSA) に割り当てられた場合にのみ利用できました。 Azure Active Directory (Azure AD) でこの機能が職場や学校のアカウントにも使えるようになりました。

サブスクリプションのコピーが他のアカウントに与えられるわけではなく、代替アカウントを利用して 2 つの特典にアクセスする機能のみが与えられます。

すべてのサブスクリプションに対して "職場または学校のアカウント" を追加できます。これにより、ログインを必要とする特典 (VS IDE、Azure DevOps、Azure) と共にそのアカウントを使用できます。

### <a name="add-the-alternate-account"></a>代替アカウントを追加する
1. Microsoft アカウント (https://my.visualstudio.com) で Visual Studio サブスクライバー ポータルにサインインします。
2. **[サブスクリプション]** タブをクリックします。
3. **[代替アカウントを追加する]** を選択します。
4. 職場または学校アカウントを追加します。
    > [!div class="mx-imgBorder"]
    > ![職場または学校アカウントを追加する](_img/vs-alternate-identity/enter-alternate-account-my-visual-studio-com-portal.png)

5. 職場または学校のアカウントを使用して Azure DevOps にサインインします (https://{自分のアカウント}.visualstudio.com)。
    > [!div class="mx-imgBorder"]
    > ![職場または学校アカウントを使用する](_img/vs-alternate-identity/sign-in-with-alternate-account.png)

代替アカウントが Visual Studio サブスクリプションに追加されました。これで、両方の ID で代替アカウントでのサインインを要求するサブスクリプション特典 (IDE、Azure DevOps、Azure) を活用できます。

## <a name="faq"></a>よく寄せられる質問

### <a name="q--why-doesnt-azure-devops-recognize-me-as-a-visual-studio-subscriber"></a>Q: Azure DevOps で Visual Studio サブスクライバーとして認識されないのはなぜですか?

A: プライマリ ID または代替 ID を使用してサインインすると、Azure DevOps で自動的にサブスクリプションが認識されます。 認識されない場合は、次のいくつかのことを試すことができます。

* 特典として [Azure DevOps](vs-azure-devops.md#eligibility) を含むアクティブな Visual Studio サブスクリプションがあることを確認します。

* Visual Studio サブスクリプション用のプライマリ ID または代替 ID のいずれかであるログインまたは ID を使用していることを確認します。

* Azure DevOps にサインインする前に、少なくとも 1 回は [Visual Studio サブスクライバー ポータル](https://my.visualstudio.com?wt.mc_id=o~msft~docs)にアクセスします。

それでもまだ Azure DevOps でサブスクリプションが認識されない場合は、[Azure DevOps のサポート](https://azure.microsoft.com/support/devops/)にお問い合わせください。
