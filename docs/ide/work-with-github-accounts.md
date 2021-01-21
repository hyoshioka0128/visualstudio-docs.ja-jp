---
title: Visual Studio の GitHub アカウントを使って作業する
ms.date: 11/16/2020
ms.custom: ''
ms.topic: conceptual
description: GitHub アカウントと共に Visual Studio を使用する方法について説明します。
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 845b663a3a0828806766fa0609e45efafabec50a
ms.sourcegitcommit: e8a13978131f257d91ce37c5a2e0d153a4c400ef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94704036"
---
# <a name="work-with-github-accounts-in-visual-studio"></a>Visual Studio の GitHub アカウントを使って作業する

パブリックな GitHub または GitHub Enterprise のアカウントをお持ちの場合は、Visual Studio キーチェーンに追加できます。 アカウントを追加すると、Visual Studio から直接 GitHub リポジトリにアクセスしたり、リポジトリを作成したりすることで、プラットフォーム統合を活用できるようになります。

## <a name="adding-public-github-accounts"></a>パブリック GitHub アカウントの追加

Microsoft アカウントか職場または学校アカウントを使用して Visual Studio に既にサインインしている場合は、パブリック GitHub アカウントを追加できます。

1. Visual Studio 環境の右上隅にある、ご自分のイニシャルが表示されたアイコンを選択します。 次に、 **[アカウント設定...]** を選択してアカウントを管理します。 **[ファイル]**  >  **[アカウント設定]** にアクセスして [アカウント設定] ダイアログを開くこともできます。

    :::image type="content" source="../ide/media/account-picker.png" alt-text="アカウント設定":::

2. **[すべてのアカウント]** サブメニューで、アカウントを追加するプラス記号を選択して、 **[GitHub]** を選択します。

    :::image type="content" source="../ide/media/sign-in-add-github.png" alt-text="GitHub アカウントの追加を選択する":::

3. ブラウザーにリダイレクトされます。ここで GitHub の資格情報を使用してサインインできます。 サインインすると、ブラウザーに成功のウィンドウが表示され、Visual Studio に戻ることができます。

    :::image type="content" source="../ide/media/github-success-signin.png" alt-text="ブラウザーでの成功ウィンドウ":::

4. **[すべてのアカウント]** サブメニューに両方のアカウントが表示されます。

    :::image type="content" source="../ide/media/show-both-accounts.png" alt-text="両方のアカウントが表示される":::

別のアカウントを使用して Visual Studio にまだサインインしていない場合は、Visual Studio 環境の右上隅にある **[サインイン]** リンクを選択します。 **[ファイル]**  >  **[アカウント設定]** にアクセスして [アカウント設定] ダイアログを開くこともできます。 次に、上記の手順に従って、GitHub アカウントを追加します。

![サインインしていないユーザー](../ide/media/vs2019_usernotsignedin.png)

## <a name="adding-github-enterprise-accounts"></a>GitHub Enterprise アカウントの追加

既定では、Visual Studio では、パブリック GitHub アカウントのみが有効になっています。

1. GitHub Enterprise アカウントを有効にするには、 **[ツール]**  >  **[オプション]** にアクセスし、 **[アカウント]** オプションを検索します。

    :::image type="content" source="../ide/media/accounts-options.png" alt-text="[アカウント] オプション メニュー":::

2. 次に、 **[GitHub Enterprise Server アカウントを含める]** チェックボックスをオンにします。 次に **[アカウント設定]** にアクセスして GitHub アカウントを追加しようとすると、GitHub と GitHub Enterprise 両方のオプションが表示されます。

    :::image type="content" source="../ide/media/github-enterprise-endpoint-signin.png" alt-text="GitHub Enterprise を使用したサインイン":::

3. GitHub Enterprise サーバーのアドレスを入力したら、 **[ブラウザーでサインインします]** を選択します。 そこで、GitHub Enterprise の資格情報を使用してサインインできます。

## <a name="see-also"></a>関連項目

- [複数のユーザー アカウントを使って作業する](work-with-multiple-user-accounts.md)
- [Visual Studio へのサインイン](signing-in-to-visual-studio.md)
