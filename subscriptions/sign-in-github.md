---
title: GitHub アカウントを使用して Visual Studio サブスクリプションにサインインする | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 1bdcb3c9-bba1-4e25-a609-9d7e539d78e0
ms.date: 12/02/2020
ms.topic: conceptual
description: GitHub アカウントを使用して Visual Studio サブスクリプションにサインインする方法について説明します。
ms.openlocfilehash: 52f67afdf8a4056063cdefef618be5b895dbb960
ms.sourcegitcommit: 29099741fcf94a5aef2655ee16605728b8b9a0ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2020
ms.locfileid: "96537995"
---
# <a name="signing-in-to-visual-studio-subscriptions-with-your-github-account"></a>GitHub アカウントで Visual Studio サブスクリプションにサインインする 

Visual Studio サブスクリプションにサインインする手順は、ご使用のアカウントの種類に応じて変わります。 たとえば、Microsoft アカウント (MSA) または勤務先または学校で指定された電子メール アドレスを使用する場合があります。 2019 年 1 月から GitHub アカウントでも一部のサブスクリプションにサインインできるようになりました。 

この記事では、GitHub アカウントを使用してサインインするための手順について説明します。

## <a name="signing-in-with-your-github-account"></a>GitHub アカウントでサインインする

GitHub ID のサポートにより GitHub アカウントと Microsoft アカウントが関連付けられ、新規または既存の Microsoft アカウントの資格情報として既存の GitHub アカウントを使用できます。 

GitHub でサインインすると、Microsoft は GitHub アカウントに関連付けられているメール アドレスが既存の個人または企業 Microsoft アカウントに一致するかどうかを確認します。 アドレスが企業アカウントに一致した場合、代わりにそのアカウントにサインインするように求められます。 アドレスが個人アカウントに一致した場合、その個人アカウントに GitHub アカウントがサインイン方法として追加されます。

GitHub と Microsoft アカウントの資格情報が関連付けられると、Azure サイト、Office アプリ、Xbox など、個人 Microsoft アカウントが使用できるあらゆる場所でそのシングル サインインを使用できます。 これらのアカウントは、メール アドレスが招待状のものと一致する場合、Microsoft アカウントとして Microsoft Azure Active Directory ゲスト サインインに使用することもできます。

> [!NOTE]
> GitHub ID と Microsoft アカウントを関連付けても Microsoft にコード アクセスが与えられることはありません。 Azure DevOps や Visual Studio のようなアプリでコード リポジトリへのアクセスが必要になるとき、このアクセスに対する特定の同意を与えるように求められます。 

### <a name="frequently-asked-questions"></a>よく寄せられる質問
次のよく寄せられる質問では、GitHub アカウントの資格情報を使用して Visual Studio サブスクリプションにサインインするときに直面する疑問に答えています。

#### <a name="q-i-forgot-my-github-password--how-can-i-access-my-account-now"></a>Q:GitHub パスワードを忘れました。  どうすれば今、自分のアカウントにアクセスできますか?
A: [[パスワードのリセット]](https://github.com/password_reset) に進むと、GitHub アカウントを回復できます。 あるいは、[[アカウントの回復]](https://account.live.com/password/reset) で GitHub アカウントのメール アドレスを入力すると、GitHub にリンクされている Microsoft アカウントを回復できます。

#### <a name="q-i-deleted-my-github-account--how-can-i-access-my-microsoft-account-msa-now"></a>Q:GitHub アカウントを削除しました。  どうすれば今、自分の Microsoft アカウント (MSA) にアクセスできますか?
A: MSA に他の資格情報 (パスワード、認証アプリ、セキュリティ キーなど) がない場合、Microsoft アカウントに関連付けられているメール アドレスを使用して Microsoft アカウントを回復できます。 開始するには、[[アカウントの回復]](https://account.live.com/password/reset) に移動します。 Microsoft が後であなたをサインインする方法を知るために、アカウントにパスワードを追加する必要があります。 

#### <a name="q-theres-no-sign-in-with-github-option-on-the-sign-in-page--how-can-i-use-my-github-credentials-to-sign-in"></a>Q:サインイン ページに "GitHub アカウントでサインイン" オプションがありません。  GitHub 資格情報を使用してサインインするにはどうすればよいですか?
A: GitHub とリンクする Microsoft アカウントの作成時に選択した GitHub アカウントのメール アドレスを入力します。 アドレスが確認されると、サインインのために GitHub に移動します。 あるいは、サインイン ページに [サインイン] オプション リンクがある場合、そのリンクのクリック後に表示される **[GitHub アカウントでサインイン]** ボタンを使用します。 

#### <a name="q-i-cant-sign-in-to-some-of-my-apps-and-products-with-github--why"></a>Q:GitHub では一部のアプリと製品にサインインできません。  なぜでしょうか。
A: Xbox コンソールなど、一部の Microsoft 製品では、そのサインイン ページから GitHub.com にアクセスできません。 代わりに、リンクされている GitHub アカウントからメール アドレスを入力すると、身元確認できるよう、そのアドレスにコードが送信されます。 別のサインイン方法によって同じアカウントにサインインすることになります。 

#### <a name="q--ive-added-a-password-to-the-microsoft-account-i-have-linked-to-my-github-account--will-that-cause-a-problem"></a>Q:自分の GitHub アカウントに関連付けた Microsoft アカウントにパスワードを追加しました。  それによって問題が発生しますか?
A: まったくありません。 GitHub パスワードが変更されることはありません。Microsoft アカウントにサインインする別の方法が与えられるだけです。 メール アドレスを使用してサインインするときは常に、Microsoft アカウントのパスワードでサインインするか、GitHub に移動してサインインするという選択肢が与えられます。 パスワードを追加する必要がある場合、GitHub アカウントのパスワードとは異なるパスワードにすることを強くお勧めします。

#### <a name="q-i-want-to-add-the-authenticator-app-to-the-account-i-created-using-github--can-i-do-that"></a>Q:GitHub を使用して作成したアカウントに認証アプリを追加することを検討しています。  それは可能ですか?
A: 問題はありません。アプリをダウンロードし、自分のメール アドレスでサインインしてください。 メール アドレスでサインインすると、[認証アプリ](https://www.microsoft.com/p/microsoft-authenticator/9nblgggzmcj6)か GitHub を資格情報として選択するように求められます。

#### <a name="q-ive-enabled-two-factor-authentication-on-both-my-github-and-microsoft-accounts-msa-but-when-i-sign-in-to-my-msa-im-still-asked-to-authenticate-twice--why"></a>Q:GitHub と Microsoft アカウント (MSA) の両方で 2 要素認証を有効にしたが、MSA にサインインすると、依然として 2 回の認証が求められます。  なぜでしょうか。
A: セキュリティ上の制約により、Microsoft は GitHub によるサインインを 1 要素認証として数えます。このことは、2 要素認証を有効にしている場合でも同じです。 そのため、Microsoft アカウントのためにもう一度認証する必要があります。 

#### <a name="q--how-can-i-tell-if-my-microsoft-account-and-github-accounts-are-linked"></a>Q:自分の Microsoft アカウントと GitHub アカウントが関連付けられていることはどうすれば確認できますか?
A: アカウント エイリアス (メール アドレス、電話番号、Skype 名) でサインインするときは常に、アカウントに対するあらゆるサインイン方法が提示されます。 そこに GitHub が表示されない場合、それがまだ設定されていません。

#### <a name="q--how-can-i-unlink-my-microsoft-and-github-accounts"></a>Q:Microsoft アカウントと GitHub アカウントの関連付けを解除する方法はありますか? 
A: account.microsoft.com の [[セキュリティ]](https://account.microsoft.com/security) タブに移動し、 **[More security options]\(その他のセキュリティ オプション\)** をクリックして GitHub アカウントの関連付けを解除します。 GitHub アカウントの関連付けを解除すると、サインイン方法としてそのアカウントが削除され、Visual Studio のあらゆる GitHub リポジトリへのアクセスが取り消されます。 他の Microsoft 製品で GitHub アカウントへのアクセスが別途要求されていることがあります。そのため、ここでアクセスを取り消しても全製品においてアクセスが取り消されることはありません。 GitHub プロファイルの [[アプリケーションのアクセス許可]](https://github.com/settings/applications) ページに進み、そこに一覧表示されているアプリから同意を取り消します。

#### <a name="q--i-try-to-use-my-github-account-to-sign-in-but-im-prompted-that-i-already-have-a-microsoft-identity-that-i-should-use-instead--whats-happening"></a>Q:GitHub アカウントでサインインを試していますが、Microsoft ID が既に登録されているので代わりにそれを使用するように促されます。  どうしてでしょうか。
A: GitHub アカウントに Azure Active Directory のメール アドレスを登録している場合、Azure にアクセスし、GitHub コードで CI パイプラインを実行できる Microsoft ID が既に与えられています。 そのアカウントを使用することで、Azure のリソースとビルド パイプラインが組織の境界内に留まります。 しかしながら、個人的な作業をしている場合、常にそれにアクセスできるよう、GitHub アカウントに個人のメール アドレスを登録することをお勧めしています。 登録後、もう一度サインインを試し、職場または学校のアカウントにサインインするように求められたら、 **[別のメール アドレスを使用]** を選択します。 これで、その個人メール アドレスを使用して新しい Microsoft アカウントを作成できます。

## <a name="see-also"></a>関連項目
- [Visual Studio ドキュメント](/visualstudio/)
- [Azure DevOps ドキュメント](/azure/devops/)
- [Azure ドキュメント](/azure/)
- [Microsoft 365 ドキュメント](/microsoft-365/)

## <a name="next-steps"></a>次の手順
サブスクリプション ポータルに正常にサインインしたら、特典のページ https://my.visualstudio.com/benefits にアクセスし、お客様が利用できる優れたツール、サービス、およびオファーを確認することをお勧めします。