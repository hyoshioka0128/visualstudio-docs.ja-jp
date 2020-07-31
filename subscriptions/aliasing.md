---
title: 別名を使用した Visual Studio サブスクリプションへのサインインが失敗する場合がある | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 97bf7474-c6c2-49b3-b2c9-f1b2808eed1a
ms.date: 03/02/2020
ms.topic: conceptual
description: 別名またはフレンドリ名の使用でサインインに失敗する場合がある
ms.openlocfilehash: 1b6c465bc3e850d8582abde200ac9e5bd995e431
ms.sourcegitcommit: 9a7fb8556a5f3dbb4459122fefc7e7a8dfda753a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87234641"
---
# <a name="signing-into-visual-studio-subscriptions-may-fail-when-using-aliases"></a>別名を使用すると、Visual Studio サブスクリプションへのサインインが失敗する場合がある
サインインに使用されるアカウントの種類によっては、[https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) にサインインするときに利用可能なサブスクリプションが正しく表示されない場合があります。 考えられる原因の 1 つは、サブスクリプションが割り当てられているサインイン ID の代わりに "別名" または "表示名" を使用していることです。 これは "別名定義" と呼ばれます。

## <a name="what-is-aliasing"></a>別名定義とは
"別名定義" という用語は、Windows (または Active Directory) へのサインインと電子メールへのアクセスに別々の ID を持っているユーザーを指します。

別名定義は、"JohnD@contoso.com" のように、会社が自社のディレクトリのサインイン用に Microsoft オンライン サービスを持っているが、ユーザーは "John.Doe@contoso.com" などの別名や表示名を使用して自分の電子メール アカウントにアクセスしている場合に発生する場合があります。 ユーザーが管理ポータル (https://manage.visualstudio.com ) に表示されている "サインイン電子メール アドレス" を使用してサブスクリプションにアクセスしていることを確認します。 

## <a name="what-are-the-potential-issues"></a>潜在的な問題は何か

サブスクライバーのアカウントの種類に応じて、次の 2 つの問題のいずれかが発生する可能性があります。 

### <a name="work-or-school-account-upn-mismatch-issue"></a>職場または学校アカウントの UPN 不一致の問題 
社内で UserPrincipalName (UPN) がプライマリ SMTP アドレスとは異なる Active Directory 設定が行われている場合、UPN の不一致が発生する可能性があります。 

#### <a name="how-to-detect-if-your-sign-in-address-is-impacted-by-a-upn-mismatch"></a>サインイン アドレスが UPN の不一致による影響を受けているかどうかを検出する方法 

1. サブスクリプション割り当ての電子メールに記載されているサインイン アドレスを使用して、 https://my.visualstudio.com/subscriptions にサインインします。

2. ページの右上に示されているサインイン電子メール アドレスが、サインインに使用したアドレスと一致していることを確認します。  そうでない場合は、UPN が不一致になっており、サブスクリプションを表示することはできません。 

> [!div class="mx-imgBorder"]
> ![電子メール アドレスへのサインイン](_img//aliasing/sign-in-email.png "右上に表示されるメール アドレスをサインインに使用するアドレスに必ず一致させます。")

#### <a name="how-to-fix-a-upn-mismatch"></a>UPN の不一致を修正する方法

1. Visual Studio 管理ポータル ([https://manage.visualstudio.com](https://manage.visualstudio.com)) にアクセスします。 

2. UPN の不一致の問題が発生しているサブスクライバーを見つけます ([フィルター](search-license.md)機能を使用すると、サブスクライバーを簡単に見つけることができます)。

3. サインイン電子メール アドレスをサブスクライバーの UPN に変更します 

0. 変更を保存します 

0. サブスクリプション ポータルからサインアウトし、UPN を使用して再度アクセスするように、サブスクライバーに通知します 

### <a name="personal-account-aliasing-issue"></a>個人アカウントの別名の問題

Visual Studio サブスクリプション ポータルへのサインインに使用された電子メール アドレスが、サブスクリプションに関連付けられている電子メール アドレスと一致しない場合、個人のサブスクリプション アカウントで問題が発生する可能性もあります。 

#### <a name="how-to-detect-if-your-personal-subscription-account-is-impacted-by-an-aliasing-issue"></a>個人のサブスクリプション アカウントが別名の問題による影響を受けているかどうかを検出する方法

1. [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions) にサインインします。

0. ページの右上に示されているサインイン電子メール アドレスが、サインインに使用したアドレスと一致していることを確認します。  サインインした電子メール アドレスと、Web サイトへのアクセスに使用した電子メール アドレスが異なる場合は、アカウントと別名が競合しています。

#### <a name="how-to-fix-an-alias-issue"></a>別名の問題を修正する方法

Visual Studio プラットフォームでは、サブスクリプションの詳細を表示するためのプライマリ エイリアスが優先されます。 

1. **Microsoft にサインインする方法の管理**に移動します。 メッセージが表示されたら Microsoft アカウントにサインインします。 

2. [アカウント エイリアス] で、サブスクリプションの割り当てに使用する電子メール アドレスの横にある **[プライマリにする]** を選択します。 

> [!div class="mx-imgBorder"]
> ![プライマリ電子メール アドレスの設定](_img//aliasing/account-aliases.png "[プライマリにする] リンクを使用し、サブスクリプションのプライマリ エイリアスを選択します。")

3. Visual Studio サブスクリプション ポータル (https://my.visualstudio.com) ) からサインアウトします 

4. サブスクリプションの割り当てに使用したアカウントを使ってもう一度サインインすると、プライマリ エイリアスとして構成されています。 

## <a name="preventing-aliasing-issues"></a>別名の問題の防止

管理者には、[https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) でユーザーのサインインを確実に成功させるために、次の 2 つのオプションがあります。
- 最初のオプション (推奨) では、Visual Studio サブスクリプション ポータル (https://my.visualstudio.com ) のサインインとして、ディレクトリ アカウントを利用します。  
- 2 番目のオプション (より安全性が低い) では、サブスクライバーはディレクトリの電子メール アドレスとは異なる電子メール アドレスを使用してサインインできます。

これらのどちらのオプションも、管理ポータル上で、次の手順を実行して構成します。  
1. [https://manage.visualstudio.com](https://manage.visualstudio.com) にサインインします。 

0. 1 人のユーザーを変更する場合は、テーブルでそのユーザーを選択し、右クリックして編集します。 これにより、サインインの電子メール アドレスを変更できるパネルが開きます。 サインイン電子メール アドレスのフィールドで必要な更新を行います。 [保存] をクリックすると、変更が有効になります。  

0. このような変更を大量のユーザーに対して行う必要がある場合は、一括編集機能を利用できます。 詳細については、「[一括編集を使用して複数のサブスクライバーを編集する](https://docs.microsoft.com/visualstudio/subscriptions/edit-license#edit-multiple-subscribers-using-bulk-edit)」を参照してください。

> [!NOTE]
> 個別変更および一括変更のどちらの場合も、サブスクライバーは、サインイン電子メール アドレスが変更されており、更新された電子メール アドレスを使用してサインインする必要があることを示した電子メールを受け取ります。 また、サブスクライバーが以前に他のサインイン アドレス下で特典を有効にした場合は、該当の他のサインイン アドレスを引き続き使用してアクセスする必要があることにも、注意してください。  

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)


## <a name="next-steps"></a>次の手順
Visual Studio サブスクリプションの管理に関する詳細情報をご覧ください。
- [個別のサブスクリプションの割り当て](assign-license.md)
- [複数のサブスクリプションを管理する](assign-license-bulk.md)
- [サブスクリプションの編集](edit-license.md)
- [最大使用量の確認](maximum-usage.md)


