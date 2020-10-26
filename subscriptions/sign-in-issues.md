---
title: Visual Studio サブスクリプションへのサインインに関する問題 | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 176c7f11-b19d-49e9-a6dd-b2e5da5e8480
ms.date: 03/11/2020
ms.topic: conceptual
description: Visual Studio サブスクリプションにサインインするときに発生する可能性のある問題について説明します
ms.openlocfilehash: 5d8a71115cd1a1aa7d850945806c22a64e7721cc
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801881"
---
# <a name="issues-signing-in-to-visual-studio-subscriptions"></a>Visual Studio サブスクリプションへのサインインに関する問題
Visual Studio サブスクリプションを使用するには、最初にサインインする必要があります。  サブスクリプションによっては、Microsoft アカウント (MSA) または Azure Active Directory (AAD) ID を使用してセットアップされている場合があります。  この記事では、サブスクリプションにサインインするときに発生する可能性がある問題について説明します。

## <a name="microsoft-accounts-msa-cannot-be-created-using-workschool-email-addresses"></a>職場/学校のメール アドレスを使用して Microsoft アカウント (MSA) を作成することはできない
職場/学校のメール アドレスを使って新しい個人用 Microsoft アカウント (MSA) を作成する機能は、メール ドメインが Azure AD で構成されているときは使用できません。 これはどういう意味でしょうか。 Microsoft 365 または Azure AD に依存する他の Microsoft 提供ビジネス サービスが組織で使用されていて、Azure AD テナントにドメイン名を追加している場合、ユーザーはドメインのメール アドレスを使って新しい個人用 Microsoft アカウントを作成できなくなります。

### <a name="why-was-this-change-made"></a>この変更が行われた理由
職場のアドレスをユーザー名として使って個人用 Microsoft アカウントを作成することは、エンド ユーザーにとっても IT 部門にとっても問題があることです。 次に例を示します。
- ユーザーは、自分の個人用 Microsoft アカウントがビジネスに準拠していて、自分の OneDrive にビジネス ドキュメントを保存してもポリシーを遵守していると考える可能性があります
- 組織を離れたユーザーは、通常、職場のメール アドレスにアクセスできなくなります。 そうなったとき、自分のパスワードを忘れた場合、自分の個人用 Microsoft アカウントに戻れなくなる場合があります。 逆に、IT 部門はパスワードをリセットして、退職した従業員の個人用アカウントに入ることができます。
- IT 部門は、アカウントの所有権とセキュリティに関して誤った認識を持っています。 しかし、ユーザーは、職場のメール アドレスにコードを 1 回ラウンドトリップするだけで、後でいつでも自分のアカウント名を変更できます。

そのような状況は、同じメール アドレスで 2 つのアカウント (Azure AD と Microsoft アカウント) を持っているユーザーの場合、特に混乱を招きます。

### <a name="what-does-this-experience-look-like"></a>この場合に表示されるエクスペリエンス
職場または学校のメール アドレスで Microsoft のコンシューマー アプリにサインアップしようとすると、次のようなメッセージが表示されます。

   > [!div class="mx-imgBorder"]
   > ![職場のメールではアカウントを作成できない](_img/sign-in-issues/cannot-use-work-email.png)

一方、個人用アカウントと職場/学校アカウントをサポートする Microsoft アプリにサインアップしようとすると、次のようなメッセージが表示されます。

   > [!div class="mx-imgBorder"]
   > ![職場/学校アカウントがサポートされている](_img/sign-in-issues/existing-account.png)

### <a name="are-existing-accounts-affected"></a>既存のアカウントへの影響
ここで説明したサインアップのブロックでは、新しいアカウントの作成だけが禁止されます。 職場/学校のメール アドレスで既に Microsoft アカウントを持っているユーザーには影響ありません。 既にそのような状況になっている場合、個人用 Microsoft アカウントの名前を簡単に変更できるようになっています。 簡単なステップ バイ ステップ ガイダンスが、こちらの[サポート記事](https://windows.microsoft.com/en-US/Windows/rename-personal-microsoft-account)で提供されています。 個人用 Microsoft アカウントの名前の変更とはユーザー名を変更することを意味し、職場のメールや、Microsoft 365 などのビジネス サービスへのサインイン方法には影響ありません。 また、個人情報にも影響しません。サインイン方法が変わるだけです。 別の (個人用) メール アドレスを使用したり、新しい @outlook.com メール アドレスを Microsoft から取得したり、自分の電話番号を新しいユーザー名として使用したりすることができます。

> [!NOTE]
> たとえば Premier サポートなどの Microsoft ビジネス サービスにアクセスするために、IT 部門から職場/学校のメール アドレスで個人用 Microsoft アカウントを作成するよう要求された場合は、アカウントの名前を変更する前に管理チームに連絡します。

## <a name="deleting-a-sign-in-address-may-prevent-access-to-a-subscription"></a>サインイン アドレスを削除するとサブスクリプションにアクセスできなくなる可能性がある
サブスクリプションに関連付けられている ID (MSA または AAD) を削除した場合、ユーザー名とサインイン ID を含むサブスクライバー情報が匿名になり、サブスクリプションにアクセスできなくなる可能性があります。

サブスクリプションへのアクセスが影響を受けないようにするには、次のいずれかの方法を使用します。
- 両方の ID 管理システムではなく、どちらか一方 (MSA または AAD) だけを配置します。
- テナントを介して、AAD と MSA の ID を関連付けます。

## <a name="signing-in-may-fail-when-using-aliases"></a>エイリアスを使用するとサインインに失敗することがある
サインインに使用されるアカウントの種類によっては、[https://my.visualstudio.com](https://my.visualstudio.com?wt.mc_id=o~msft~docs) にサインインするときに利用可能なサブスクリプションが正しく表示されない場合があります。 考えられる原因の 1 つは、サブスクリプションが割り当てられているサインイン ID の代わりに "別名" または "表示名" を使用していることです。 これは "別名定義" と呼ばれます。

### <a name="what-is-aliasing"></a>別名定義とは
"別名定義" という用語は、Windows (または Active Directory) へのサインインと電子メールへのアクセスに別々の ID を持っているユーザーを指します。

別名定義は、JohnD@contoso.com のように、会社が自社のディレクトリのサインイン用に Microsoft オンライン サービスを持っているが、ユーザーは John.Doe@contoso.com などの別名や表示名を使用して自分の電子メール アカウントにアクセスしている場合に発生する場合があります。 ボリューム ライセンス サービス センター (VLSC) を介してサブスクリプションを管理している多くのユーザーにとって、これがサインインが失敗する原因となる場合があります。指定したメール アドレス (John.Doe@contoso.com) が、"職場または学校アカウント" オプションを通じて正常に認証するために必要なディレクトリ アドレス (JohnD@contoso.com) と一致していないからです。

### <a name="what-options-do-i-have"></a>どのようなオプションがありますか
サブスクライバーの観点からは、まず、管理者に問い合わせて、会社の ID の構成を理解することが重要です。 必要に応じて、管理者が管理ポータルから、サブスクライバーのアカウント設定を更新する必要がある場合や、サブスクライバーが自分の会社のメール アドレスを使用して Microsoft アカウント (MSA) を作成する必要がある場合があります。 MSA を作成する手順を実行する前に、この実行に関するポリシーまたは問題について管理者と話します。 

## <a name="see-also"></a>参照
- [Visual Studio ドキュメント](https://docs.microsoft.com/visualstudio/)
- [Azure DevOps ドキュメント](https://docs.microsoft.com/azure/devops/)
- [Azure ドキュメント](https://docs.microsoft.com/azure/)
- [Microsoft 365 ドキュメント](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>次のステップ
- AAD 内で [MSA アカウントと AAD アカウントをリンクする](/azure/active-directory/b2b/add-users-administrator)方法を学習します。
- [匿名化](anonymization.md)について詳しく学習します。
