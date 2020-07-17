---
title: Visual Studio で問題を報告する方法
description: Visual Studio に関する問題を報告する方法を確認します
ms.date: 03/11/2018
ms.topic: how-to
ms.assetid: bee01179-cde5-4419-9095-190ee0ba5902
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 15a1d497b5b4217cd7a404cb591c20bb1196b04b
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387318"
---
# <a name="how-to-report-a-problem-with-visual-studio-or-visual-studio-installer"></a>Visual Studio または Visual Studio Installer に関する問題を報告する方法

> [!NOTE]
> Visual Studio for Mac については、「[Visual Studio for Mac に関する問題を報告する方法](/visualstudio/mac/report-a-problem)」を参照してください。

Visual Studio またはそのインストーラーで発生した問題は、それらに含まれているフィードバック ツールを使用して報告できます。 フィードバック ツールを使用すると、お客様のフィードバック内に診断情報を簡単に含めることができ、Visual Studio チームが問題の診断と修正を非常に効率的に行うのに役立ちます。 問題を報告する手順を次に示します。

1. **Visual Studio で**、右上隅にあるフィードバック アイコンを選択し、[問題の報告] を選択します。 フィードバック ツールには、 **[ヘルプ]** メニュー >  **[フィードバックの送信]**  >  **[問題の報告]** からアクセスすることもできます。
![Visual Studio Developer Community の [問題の報告] ポップアップ](media/vsfeedbackentry.png) Visual Studio をインストールできない場合、または Visual Studio 内のフィードバック ツールにアクセスできない場合は、**Visual Studio Installer** で問題を報告してください。  Installer で、右上隅にあるフィードバック アイコンを選択し、[問題の報告] を選択します。
![Visual Studio Developer Community での問題の報告に関するポップアップ](media/installer.png)

1. サインインしていない場合は、次のスクリーンショットに示されている **[サインイン]** を選択します。 画面に表示される手順に従ってサインインします。

   ![サインインして問題を報告する](../ide/media/sign-in-new-ux.png)

   サインインすると、問題を報告するだけではなく、既存のフィードバックに投票したり、コメントしたりできます。

1. サインイン後に、 **[フォロー項目]** 画面で、**問題**と**活動**を確認できます。

   ![フォロー項目](../ide/media/items-i-follow.png)

1. Visual Studio では、問題を検索したり、その問題が他のユーザーによって報告済みかどうかを確認するためのインターフェイスが提供されます。 報告済みの場合は、"上向きの矢印に投票" してお知らせください。
   > [!NOTE]
   > 検索する場合は、検索ボックスに目的のテキストを入力し、Enter キーを押すか、検索アイコンをクリックします。

   ![類似問題を検索して投票する](../ide/media/search-and-vote.png)

1. 発生した問題が見つからない場合は、画面の下部にある **[新しい問題を報告する]** を選択します。

1. 適切な Visual Studio チームに問題を転送できるように、報告には説明的なタイトルを付けてください。

1. 可能であれば、問題を再現する手順など、さらに詳しい情報を記載します。

   ![新しい問題を報告する](../ide/media/report-new-problem.png)

1. **[次へ]** を選択して、 **[添付ファイル]** タブに移動します。ここで、Microsoft に送信する現在の画面を取り込むことができます。 追加のスクリーンショットやその他のファイルを添付するには、 **[追加ファイルを添付]** を選択します。

   ![Visual Studio の問題レポートにスクリーンショットを添付する](media/report-a-problem-screenshot.png)

1. スクリーンショットを添付しない場合や、[再現手順を記録](#record-a-repro)しない場合は、 **[次へ]** を選択して **[概要]** タブに移動します。

1. **[送信]** を選択して、イメージおよびトレースまたはダンプ ファイルと共に、レポートを送信します。 ( **[送信]** ボタンが灰色表示の場合、レポートのタイトルと説明が記載されていることを確認します)。

   収集されるデータについては、「[Data we collect](developer-community-privacy.md#data-we-collect)」(収集するデータ) を参照してください。

## <a name="record-a-repro"></a>再現手順を記録する

トレースとヒープ ダンプのファイルは、問題を診断するうえで役立ちます。 **[問題の報告]** ツールで再現する手順を記録し Microsoft にデータを送信してくだされば、大変助かります。 これを行う方法を次に示します。

1. 問題のタイトルと説明を入力したら、 **[次へ]** を選択して **[添付ファイル]** タブに移動します。

1. **[記録]** タブを選択します。

1. 問題をそこで再現できる場合は、 **[操作の記録]** で Visual Studio の現在のインスタンスを選択します。 再現できない (たとえば、Visual Studio が応答していない) 場合は、 **\<Create a new instance>** を選択して、Visual Studio の新しいインスタンスの操作を記録します。

1. **[記録の開始]** を選択します。 ツールの実行を許可します。

   ![[記録の開始] を選択して、Visual Studio の問題レポートでトレースとヒープ ダンプ ファイルを提供する](../ide/media/record-dialog-box.png)

1. **[ステップ記録ツール]** ツールが表示されたら、問題を再現する手順を実行します。

1. 終了したら、 **[記録の停止]** ボタンを選択します。

1. 記録された情報が Visual Studio により収集され、パッケージ化されるまでしばらく待ちます。

   収集されるデータについては、「[Data we collect](developer-community-privacy.md#data-we-collect)」(収集するデータ) を参照してください。

## <a name="when-further-information-is-needed-need-more-info"></a>さらに情報が必要な場合 ([さらに情報が必要です])

Visual Studio 2017 バージョン 15.5 以降には、新しいワークフローがあり、ユーザーが問題レポートに関する追加情報を提供するのに役立ちます。

1. Microsoft のエンジニアが [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) の問題を **[さらに情報が必要です]** の状態に設定した場合、その問題について、投稿、投票、フォロー、コメントしたすべてのユーザーに対して、Visual Studio の **[問題の報告]** ツールに通知が表示されます。

   ![Visual Studio の [さらに情報が必要です] 通知](../ide/media/nmi-notification.png)

1. **[問題の表示]** リンクをクリックし、注意が必要な問題のビューをフィルター処理して並べ替えます。 これらの問題の横には、一般検索で区別するためのインジケーターもあります。

1. 問題をクリックして、問題の詳細ビューを表示します。

   ![[さらに情報が必要です] 通知](../ide/media/nmi-details-view.png)

1. **[さらに情報が必要です]** 要求を表示するには、問題の詳細ビューで **[要求と応答を表示]** リンクをクリックします。 ダイアログ ボックスに要求が表示されます。

   ![[さらに情報が必要です] 通知](../ide/media/nmi-request.png)

1. コメントや添付ファイルを追加するか、手順を記録することで、さらに情報を提供することができます。 このエクスペリエンスは、新しい問題を報告することや、問題への投票時に追加情報を提供することと似ています。

1. 要求側の Microsoft エンジニアは、提供された追加情報に関する通知を受け取ります。 調査に十分な情報がある場合は、問題の状態が変わります。 それ以外の場合、エンジニアはさらに情報を求めます。

   > [!NOTE]
   > * 返信すると、通知は表示されなくなります。 その代わりに、感謝を表すバナーが示され、追加情報を容易に提供できる方法が表示されます。
   > * 問題の状態が変わると、その問題をフォローしているすべてのユーザーに対する通知は表示されなくなります。
   > * 複数のユーザーが同じ **[さらに情報が必要です]** 要求で返信することができます。
   > * Web ブラウザーから直接アクセスした場合は、[Developer Community](https://developercommunity.visualstudio.com/) に **[さらに情報が必要です]** ワークフローはありませんが、そこでコメントや添付ファイルを提供することもできます。

## <a name="search-for-solutions-or-provide-feedback"></a>解決策を検索するかフィードバックを提供する

Visual Studio を使用して問題を報告したくない場合、またはできない場合は、既に問題が報告され、[Visual Studio Developer Community](https://developercommunity.visualstudio.com/) ページに解決策が投稿されている可能性があります。

レポートする問題はないが、機能を提案したい場合は、そのための場所も用意されています。 詳細については、「[Suggest a feature](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)」(機能を提案する) ページをご覧ください。

## <a name="see-also"></a>関連項目

* [Visual Studio フィードバック オプション](../ide/feedback-options.md)
* [Visual Studio for Mac に関する問題を報告する](/visualstudio/mac/report-a-problem)
* [C++ に関する問題を報告する](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 開発者コミュニティ](https://developercommunity.visualstudio.com/)
* [開発者コミュニティのデータのプライバシー](developer-community-privacy.md)
