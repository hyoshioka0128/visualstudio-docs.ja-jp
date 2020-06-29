---
title: Visual Studio にサインイン
titleSuffix: ''
ms.custom: seodec18
ms.date: 03/10/2020
ms.topic: conceptual
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 85d4be9ffd8d1f5ccc6c6d1a1ba5f83e7f0fccf6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85285297"
---
# <a name="sign-in-to-visual-studio"></a>Visual Studio にサインイン

Visual Studio の開発エクスペリエンスをカスタマイズし、最適化するには、個人アカウントにサインインします。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[Visual Studio for Mac にサインインする](/visualstudio/mac/signing-in)」を参照してください。

::: moniker range="vs-2017"

> [! 警告] Visual Studio 2017 を使用して、条件付きアクセス用に構成されたリソースにアクセスすると、認証エクスペリエンスが低下し、同じ Visual Studio セッション内で再認証が何度も要求されることがあります。 
> 条件付きアクセス用に構成されたリソースを操作するには、Visual Studio 2019 Update 16.6 以降にアップグレードします。 詳細については、「[多要素認証が必要なアカウントで Visual Studio を使用する方法](work-with-multi-factor-authentication.md)」を参照してください。

::: moniker-end

## <a name="why-should-i-sign-in-to-visual-studio"></a>Visual Studio にサインインする必要がある理由

サインインすると、Visual Studio エクスペリエンスが強化されます。 たとえば、数例を挙げると、サインイン後にデバイス全体の[設定を同期](synchronized-settings-in-visual-studio.md)したり、評価期間を延長したり、Azure サービスに自動的に接続したりできます。

期待できる内容とサイン後に行うことができる内容の完全なリストを以下に示します。
- **Visual Studio の評価期間を拡張する** - 30 日の評価期間にとらわれることなく、Visual Studio Professional または Visual Studio Enterprise を 90 日間延長して使用できます。 詳細については、「[試用版を延長する、またはライセンスを更新する](../ide/how-to-unlock-visual-studio.md)」をご覧ください。

- **Visual Studio Community エディションのロックを解除する** - Community エディションのインストール時にライセンスを求めるプロンプトが表示された場合は、IDE にサインインして自分でロックを解除します。

- **Visual Studio サブスクリプションまたは Azure DevOps 組織に関連付けられているアカウントを使用している場合は、Visual Studio をロック解除します**。 詳細な手順については、「[試用版を延長する、またはライセンスを更新する](../ide/how-to-unlock-visual-studio.md)」をご覧ください。

- **Visual Studio Dev Essentials プログラムにアクセスする** - このプログラムには、無料のソフトウェア提供サービス、トレーニング、サポートなどが含まれます。 詳細については、「 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/) 」をご覧ください。

- **Visual Studio の設定を同期する** - どのデバイス上の Visual Studio にサインインしても、ユーザーがカスタマイズした設定 (キー バインド、ウィンドウのレイアウト、配色テーマなど) がすぐに適用されます。 [Visual Studio での設定の同期](../ide/synchronized-settings-in-visual-studio.md)に関する記事をご覧ください。

- IDE で、**Azure や Azure DevOps Services などのサービスに自動的に接続**され、同じアカウントの資格情報を再度要求されることはなくなります。

## <a name="how-to-sign-in-to-visual-studio"></a>Visual Studio にサインインする方法

Visual Studio を初めて開くと、サインインして基本登録情報を入力するように求められます。 

![サインイン プロンプト](../ide/media/vs2019_signinpopup.png)

Microsoft アカウント、またはユーザーを最も的確に表す職場や学校のアカウントを選択してください。 これらのアカウントがない場合は、サインイン ボタンの下にあるリンクをクリックして、Microsoft アカウントを無料で作成できます。 問題が発生した場合は、[Microsoft アカウントにサインアップする方法](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)に関するページをご覧ください。

次に、Visual Studio で使用する UI 設定や配色テーマを選択します。 これらの設定は Visual Studio に保存され、サインインしたすべての Visual Studio 環境間で同期されます。 同期される設定の一覧については、「[Visual Studio での同期された設定](../ide/synchronized-settings-in-visual-studio.md)」を参照してください。 Visual Studio の **[ツール]** 、 **[オプション]** メニューを開けば、これらの設定は後で変更できます。

設定が終わったら、Visual Studio が起動し、サインインして、作業を開始できるようになります。 ログインしているかどうかを確認するには、Visual Studio 環境の右上隅に表示されているプロファイル名を探します。

![VS2019 に現在ログインしているユーザー](../ide/media/vs2019_username.png)

最初に Visual Studio を開いたときにサインインしないように選択した場合、後から簡単にサインインできます。 Visual Studio 環境の右上隅にある **[サインイン]** リンクを探してください。 

![サインインしていないユーザー](../ide/media/vs2019_usernotsignedin.png)

サインアウトしない限り、Visual Studio を起動すると自動的にサインインすることになり、同期された設定への変更が自動的に適用されます。 サインアウトするには、Visual Studio 環境の右上隅にある自分のプロファイル名が表示されたアイコンを選択し、 **[アカウント設定]** コマンドを選択してから **[サインアウト]** リンクを選択します。 再度サインインするには、Visual Studio 環境の右上隅の **[サインイン]** をクリックします。

## <a name="to-change-your-profile-information"></a>ユーザーのプロファイル情報を変更するには

1. **[ファイル]** 、 **[アカウント設定]** の順に進み、 **[Visual Studio プロファイルの管理]** リンクを選択します。

1. ブラウザー ウィンドウで、 **[プロファイルの編集]** を選択し、必要な設定を変更します。

1. 完了したら、 **[変更の保存]** を選択します。

## <a name="troubleshooting"></a>トラブルシューティング

サインイン時に問題が発生した場合は、「[サブスクリプション サポート](https://visualstudio.microsoft.com/subscriptions/support/)」ページを参照してヘルプを表示してください。

## <a name="see-also"></a>関連項目

* [試用版を延長する、またはライセンスを更新する](../ide/how-to-unlock-visual-studio.md)
* [Visual Studio IDE の概要](../get-started/visual-studio-ide.md)
* [サインイン (Visual Studio for Mac)](/visualstudio/mac/signing-in)
* [アクティブ化 (Visual Studio for Mac)](/visualstudio/mac/activation)
