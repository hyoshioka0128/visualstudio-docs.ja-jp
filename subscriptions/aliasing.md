---
title: 別名を使用した Visual Studio サブスクリプションへのサインインが失敗する場合がある | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.date: 02/14/2020
ms.topic: conceptual
description: 別名またはフレンドリ名の使用でサインインに失敗する場合がある
ms.openlocfilehash: dff48852e566522ad01ee07bd46cda72b8e1e249
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77276622"
---
# <a name="signing-in-to-visual-studio-subscriptions-may-fail-when-using-aliases"></a>別名を使用した Visual Studio サブスクリプションへのサインインが失敗する場合がある
サインインに使用されるアカウントの種類によっては、[https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) にサインインするときに利用可能なサブスクリプションが正しく表示されない場合があります。 考えられる原因の 1 つは、サブスクリプションが割り当てられているサインイン ID の代わりに "別名" または "表示名" を使用していることです。 これは "別名定義" と呼ばれます。

## <a name="what-is-aliasing"></a>別名定義とは
"別名定義" という用語は、Windows (または Active Directory) へのサインインと電子メールへのアクセスに別々の ID を持っているユーザーを指します。

別名定義は、"olivia@contoso.com" のように、会社が自社のディレクトリのサインイン用に Microsoft オンライン サービスを持っているが、ユーザーは "OliviaG@contoso.com" などの別名や表示名を使用して自分の電子メール アカウントにアクセスしている場合に発生する場合があります。 ユーザーが、 https://manage.visualstudio.com の Visual Studio サブスクリプション管理ポータルに表示されている "サインイン電子メール アドレス" を使用して自分のサブスクリプションにアクセスしていることを確認します。

## <a name="as-an-administrator-what-options-do-i-have"></a>管理者として選択できるオプションとは

サブスクライバーのアカウントの種類に応じて、適用できるソリューションを以下で見つけます。

### <a name="work-or-school-account-upn-mismatch-issue"></a>職場または学校アカウントの UPN 不一致の問題

ユーザー プリンシパル名 (UPN) の不一致は、UPN がプライマリ SMTP アドレスと異なる Active Directory が会社に設定されている場合に、発生する可能性があります。 

#### <a name="how-to-detect-if-a-users-sign-in-address-has-a-upn-mismatch"></a>ユーザーのサインイン アドレスに UPN の不一致があるかどうかを検出する方法

ユーザーに次の手順を完了してもらいます。

1. サブスクリプション割り当ての電子メールに記載されているサインイン アドレスを使用して、 https://my.visualstudio.com にサインインします。  

    > [!NOTE]
    > サブスクリプション割り当ての電子メールがない場合は、管理ポータル内からメールを再送信することができます。  

2. **[サブスクリプション]** タブをクリックします。
3. 右上の [次のアカウントでサインインしています] に表示されている電子メール アドレスが、サブスクリプション割り当ての電子メールに記載されているサインイン電子メール アドレスと同じであることを確認します。  そうでない場合は、サブスクリプションの特典を利用できません。 

   > [!div class="mx-imgBorder"]
   > ![[サブスクリプション] ページ](_img/aliasing/aliasing-subscriptions-page.png)

#### <a name="how-to-correct-the-upn-mismatch"></a>UPN の不一致を修正する方法

1. https://manage.visualstudio.com の Visual Studio 管理ポータルにアクセスします。 

2. UPN 不一致の問題が発生しているユーザーを見つけます。  [フィルター](search-license.md)機能を使用すると、多数のサブスクリプションがある場合に、これを簡単に行うことができます。 

3. サインイン電子メール アドレスをユーザーの UPN に変更します。

4. 変更を保存します 

5. サブスクライバー ポータルからログアウトし、UPN を使用してもう一度サインインするようにユーザーに依頼します。   

### <a name="personal-account-aliasing-issue"></a>個人アカウントの別名の問題

別名の問題も、個人のアカウントに影響を与える可能性があります。 

#### <a name="how-to-detect-if-a-personal-account-has-an-aliasing-issue"></a>個人のアカウントに別名の問題があるかどうかを検出する方法

1. https://my.visualstudio.com にサインインします。

2. **[サブスクリプション]** タブをクリックし、サインインしているアドレスを確認します。 

3. サインインした電子メール アドレスと、Web サイトへのアクセスに使用した電子メール アドレスが異なる場合は、アカウントと別名が競合しています。 

#### <a name="how-to-fix-a-personal-account-aliasing-issue"></a>個人アカウントの別名の問題を修正する方法

Visual Studio サブスクリプション プラットフォームでは、サブスクリプションの詳細を表示するためのプライマリ エイリアスが優先されます。  問題を解決するには、別の電子メール エイリアスをサインイン用のプライマリ エイリアスにする必要があります。 

1. [Microsoft にサインインする方法の管理](https://go.microsoft.com/fwlink/p/?linkid=842796)に移動します。
2. メッセージが表示されたら Microsoft アカウントにサインインします。 
3. [アカウント エイリアス] で、サブスクリプションの割り当てに使用する電子メール アドレスの横にある **[プライマリにする]** を選択します。 
4. [アカウント エイリアス] で、サブスクリプションの割り当てに使用する電子メール アドレスの横にある [プライマリにする] を選択します。 
5. Visual Studio サブスクライバー ポータル (https://my.visualstudio.com) にサインインします。 
6. 新しいプライマリ エイリアスを使用してポータルにもう一度アクセスします。 

### <a name="ensure-a-successful-experience-for-your-users"></a>ユーザーのエクスペリエンスが成功したことを確認する

管理者には、 https://my.visualstudio.com でユーザーのサインインを確実に成功させるために、次の 2 つのオプションがあります。 

- 最初のオプション (推奨) は、 https://manage.visualstudio.com でのサインイン アドレスとしてディレクトリ アカウントを利用することです。
- 2 番目のオプション (より安全性が低い) は、サブスクライバーがディレクトリの電子メール アドレスとは異なる電子メール アドレスを使用してサインインできるようにすることです。

どちらのオプションも、管理ポータルで次の手順を行って構成します。

1. https://manage.visualstudio.com にサインインします。 

2. 1 人のユーザーを変更する場合は、テーブルでそのユーザーを選択し、右クリックして編集します。 これにより、サインインの電子メール アドレスを変更できるパネルが開きます。  

3. サインイン電子メール アドレスのフィールドで必要な更新を行います。 

4. [保存] をクリックすると、変更が有効になります。  
このような変更を大量のユーザーに対して行う必要がある場合は、一括編集機能を利用できます。 その処理の詳細については、「[サブスクリプションの編集](edit-license.md)」の記事にある「**一括編集を使用した複数のサブスクライバーの編集**」セクションを参照してください。  

## <a name="next-steps"></a>次の手順
Visual Studio サブスクリプションの管理に関する詳細情報をご覧ください。
- [個別のサブスクリプションの割り当て](assign-license.md)
- [複数のサブスクリプションを管理する](assign-license-bulk.md)
- [サブスクリプションの編集](edit-license.md)
- [サブスクリプションの削除](delete-license.md)
- [最大使用量の確認](maximum-usage.md)

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)
