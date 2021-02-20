---
title: 試用版を延長する、またはライセンスを更新する
description: Visual Studio の無料試用期間を延長する方法、オンライン サブスクリプションまたはプロダクト キーを使用して Visual Studio のロックを解除する方法、古いライセンスまたは期限切れのライセンスを更新する方法について説明します。
ms.date: 12/18/2019
ms.topic: conceptual
ms.assetid: ffb580a1-8b5d-48f5-b811-87f8036f50ea
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.openlocfilehash: 3dd2a688ef70064f44caccfd7c64150b7c649769
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99869129"
---
# <a name="extend-a-trial-version-or-update-a-license"></a>試用版を延長する、またはライセンスを更新する

[Visual Studio Professional または Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/compare/) の無料試用版を 30 日間評価できます。 サインインすると、試用期間を 90 日まで延長できます (Visual Studio Community は無料です。試用期間はありません。 ただし、[ライセンスを常に最新の状態に保つ](#update-a-stale-license)ために、定期的に[サインイン](signing-in-to-visual-studio.md)する必要があります)。

試用期間が終了した後も Visual Studio を引き続き使用するには、[オンライン サブスクリプション](#use-an-online-subscription)または[プロダクト キー](#enter-a-product-key)を使用してロックを解除します。

## <a name="use-an-online-subscription"></a>オンライン サブスクリプションを使用する

1. IDE の右上隅にある **[サインイン]** ボタンを選択します (または、 **[ファイル]**  >  **[アカウントの設定]** の順に移動して **[アカウントの設定]** ダイアログを開き、 **[サインイン]** ボタンを選択します)。

1. Microsoft アカウントか、職場または学校のアカウントの資格情報を入力します。 Visual Studio は、アカウントに関連付けられている Visual Studio サブスクリプションまたは Azure DevOps 組織を検索します。

> [!IMPORTANT]
> **チーム エクスプローラー** のツール ウィンドウから Azure DevOps 組織に接続すると、Visual Studio は関連付けられているオンライン サブスクリプションを自動的に検索します。 Azure DevOps 組織に接続した場合は、Microsoft アカウントと、職場または学校アカウントの両方を使用してサインインできます。 そのユーザー アカウントのオンライン サブスクリプションが存在する場合は、Visual Studio は自動的に IDE のロックを解除します。

Visual Studio サブスクリプションとそのしくみの詳細については、[サブスクリプション サポートに関する FAQ](https://visualstudio.microsoft.com/subscriptions/support/) ページを参照してください。

## <a name="enter-a-product-key"></a>プロダクト キーを入力する

1. **[ファイル]**  >  **[アカウントの設定]** の順に選択して **[アカウントの設定]** ダイアログを開き、 **[プロダクト キーを使用してライセンスを取得します]** リンクを選択します。

1. 所定の場所にプロダクト キーを入力します。

> [!TIP]
> Visual Studio のプレリリース版には、プロダクト キーはありません。 プレリリース版を使用するには、IDE にサインインする必要があります。

Visual Studio の Visual Studio プロダクト キーとその入手方法の詳細については、「[Visual Studio サブスクリプションでのプロダクト キーの使用](/visualstudio/subscriptions/product-keys)」ページを参照してください。

## <a name="update-a-stale-license"></a>古いライセンスを更新する

Visual Studio に "ライセンスが古くなったため、更新する必要があります" というメッセージが表示される場合があります。

![Visual Studio の古いライセンスに関するメッセージ](../ide/media/vs2017_stale-license.png)

このメッセージは、サブスクリプションがまだ有効な期間でも、Visual Studio でサブスクリプションを最新の状態に保つために使用されるライセンス トークンが更新されていないことを示します。 Visual Studio では、次のいずれかの理由により、ライセンスが古いと報告されます。

* Visual Studio を使用していないか、長期間インターネットに接続していません。
* Visual Studio からサインアウトした。

ライセンス トークンの有効期限が切れる前に、資格情報の再入力を求めるメッセージが Visual Studio により表示されます。

資格情報を再入力しない場合、トークンの有効期限が近づきます。この場合、 **[アカウントの設定]** ダイアログで、トークンの有効期限が切れるまでの日数が通知されます。 トークンの有効期限が切れた後で Visual Studio を引き続き使用するには、アカウントの資格情報を再入力する必要があります。

> [!Important]
> インターネットへのアクセスが限定的またはアクセスできない環境で長期間にわたって Visual Studio を使用している場合は、Visual Studio の中断を回避するためにプロダクト キーを使用してロックを解除する必要があります。

## <a name="update-an-expired-license"></a>期限切れのライセンスを更新する

サブスクリプションの有効期限が切れ、Visual Studio へのアクセス権がなくなった場合は、サブスクリプションを更新するか、サブスクリプションのある別のアカウントを追加する必要があります。 使用中のライセンスの詳細については、 **[ファイル]**  >  **[アカウントの設定]** の順に移動し、ダイアログの右側にあるライセンス情報を参照してください。 異なるアカウントに関連付けられている別のサブスクリプションがある場合は、 **[アカウントの追加]** リンクを選択して、ダイアログ ボックスの左側にある **[すべてのアカウント]** 一覧にそのアカウントを追加します。

## <a name="get-support"></a>サポートを受ける

問題が発生した場合に備え、 問題が発生した場合は、次のようなサポート オプションを利用できます。

* [問題の報告](how-to-report-a-problem-with-visual-studio.md)ツールを使用して、製品の問題を報告します。
* サブスクリプション、アカウント、および課金に関する質問への回答は、[サブスクリプションのサポートに関する FAQ](https://visualstudio.microsoft.com/subscriptions/support/) を参照してください。

## <a name="see-also"></a>参照

* [Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)
* [Visual Studio の各エディションの比較](https://visualstudio.microsoft.com/vs/compare/)
* [Visual Studio サブスクリプションの詳細情報](/visualstudio/subscriptions/)
