---
title: VLSC に表示される個人メール
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 3f4b0528-03f0-4a02-b3c3-a39292a9bbe1
ms.date: 09/22/2020
ms.topic: conceptual
description: 'Visual Studio のサブスクリプション: サブスクライバーに Hotmail や Gmail のアドレスが表示される理由'
ms.openlocfilehash: dc2de6c852f39f789fb07358384ad490d13f137c
ms.sourcegitcommit: d3bca34f82de03fa34ecdd72233676c17fb3cb14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "91022660"
---
# <a name="visual-studio-subscriptions--why-do-i-see-personal-accounts-for-my-subscribers"></a>Visual Studio のサブスクリプション: サブスクライバーに個人用アカウントが表示される理由
ボリューム ライセンス サービス センター (VLSC) から Visual Studio の新しい[サブスクリプション管理ポータル](https://manage.visualstudio.com)に移行した後、一部のサブスクライバーの "サインイン用のメール アドレス" として、Hotmail や Outlook などの個人用メール アドレスが表示され、管理者が驚くことがありました。  

## <a name="cause"></a>原因
このシナリオは、従来の MSDN サブスクライバー エクスペリエンスにサインイン プロセスが関連付けられていることによって発生します。 ユーザーはボリューム ライセンス サービス センター (VLSC) から Visual Studio のサブスクリプション管理ポータルに、変更なく移行されました。 管理者は、ユーザーが個人アカウントを使用して、サブスクリプションの特典にアクセスしていたことを知らなかった可能性があります。 2016 年で完了した Visual Studio のサブスクライバーの移行以前は、Visual Studio のサブスクリプションを使用には、2 回アクションを実行する必要がありました。
1. 管理者が、個々のサブスクライバーに、職場または学校のメール アドレスを使用してサブスクリプションを “割り当て” ます。
2. そのサブスクリプションをサブスクライバーが “アクティブ化” します。

サブスクライバーのアクティブ化処理中には、次が発生します。サインインに Microsoft アカウント (MSA) が求められます。 サブスクライバーが職場または学校のアカウント (例: tasha@contoso.com) を MSA にしない場合、新しい MSA を作成するか、既存のものが利用されます。 これにより、“サインイン電子メール アドレス” が “割り当てられたメール アドレス” と異なってしまいます。

> [!NOTE]
> [https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) の最新のサブスクライバー エクスペリエンスでは、職場または学校と、Microsoft アカウント (MSA) の両種類の ID がサポートされています。

## <a name="solution"></a>ソリューション
この問題を解決するには、 **[Connect Emails]\(電子メールに接続\)** ボタンを選択するればよいだけです。後はシステムによって、MSA を含むアカウントを組織の Azure Active Directory (Azure AD) 内の既存のユーザーと一致させる試みが姓と名の照合に基づいて行われます。 エラーが発生した場合は、一致の右側にある **[X]** をクリックして一致を削除できます。  

この修正方法を学習するには、この動画を見るか、読み続けてください。 

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4th6B]

> [!div class="mx-imgBorder"]
> ![[Connect Emails]\(電子メールに接続\) ボタン](_img/connect-emails/connect-emails-button.png "[Connect Emails]\(電子メールに接続\) をクリックし、Microsoft アカウントを持つユーザーを Azure Active Directory で照合する")

**[ディレクトリの検索]** を使用して、エラーを修正したり、不足している情報をご利用の Azure AD から入力したりすることもできます。 すべての一致が正しく表示されている場合は、一度に 1 つずつ選択するのでなく、 **[Current identity]\(現在の ID)\** ボタンを選択し、一致するすべてのエントリを選択できます。  

> [!div class="mx-imgBorder"]
> ![[Connect Emails]\(電子メールに接続\) のフライアウト](_img/connect-emails/connect-emails-flyout.png "Azure AD の ID と照合するサブスクライバーを選択し、[続行] をクリックします。")

次に **[続行]** をクリックします。これにより、行われる変更の一覧が表示されます。 同意する場合は、 **[保存]** をクリックします。変更が行われます。 また、サブスクライバーが次回自分のサブスクリプションにサインインしたとき、変更を通知するメッセージも表示されます。  Azure Active Directory で一致した 2 つのサブスクライバーだけがこの一覧に表示されることに注意してください。  今回の例では、Azure AD ではそれに対応するアドレスが Frederick に与えられていないため、彼の Microsoft account (MSA) は仕事用アカウントに一致しませんでした。 

> [!div class="mx-imgBorder"]
> ![電子メールへの接続の確認](_img/connect-emails/connect-emails-confirm.png "[続行] をクリックし、提案された変更を実行し、[保存] をクリックします。") 

> [!NOTE]
> サインイン電子メール アドレスを編集した場合、これによって更新されるのは、サブスクライバーが https://my.visualstudio.com 上で自分のサブスクリプションにサインインするときに使用する電子メールのみとなります。 他の電子メール アドレスを使用して Azure や Pluralsight などのベネフィットを既にアクティブ化しているサブスクライバーは、該当する電子メール アドレスを引き続き使用してそれらにアクセスする必要があります。 彼らが新しいベネフィットにアクセスする場合は、新しい電子メール アドレスを使用する必要があります。 

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

##  <a name="next-steps"></a>次の手順
- サブスクライバーのメール アドレスを更新したら、サインイン情報が変更されたことをサブスクライバーに通知することもできます。  更新された情報が含まれる電子メールも送信されます。
- 組織内の[サブスクライバーの一覧をフィルター処理](search-license.md)して、変更が必要な可能性のあるサインイン用メールアドレスを検索すると便利な場合があります。