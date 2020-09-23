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
ms.openlocfilehash: b2deb3f8ff19c2d7805031c0c3ba02bc82b8a3e7
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90810875"
---
# <a name="how-to-report-a-problem-with-visual-studio-or-visual-studio-installer"></a>Visual Studio または Visual Studio Installer に関する問題を報告する方法

> [!NOTE]
> Visual Studio for Mac については、「[Visual Studio for Mac に関する問題を報告する方法](/visualstudio/mac/report-a-problem)」を参照してください。

Visual Studio またはそのインストーラーで発生した問題を報告できます。 組み込みのフィードバック ツールを使用すると、Visual Studio チームが問題を診断して解決するのに役立つ診断情報を簡単に追加できます。 問題を報告する手順を次に示します。

1. **Visual Studio で**、右上隅にあるフィードバック アイコンを選択し、[問題の報告] を選択します。 フィードバック ツールには、 **[ヘルプ]** メニュー >  **[フィードバックの送信]**  >  **[問題の報告]** からアクセスすることもできます。
![Visual Studio Developer Community の [問題の報告] ポップアップ](media/feedback-button.png) Visual Studio をインストールできない場合、または Visual Studio 内のフィードバック ツールにアクセスできない場合は、**Visual Studio Installer** で問題を報告してください。  Installer で、右上隅にあるフィードバック アイコンを選択し、[問題の報告] を選択します。
![Visual Studio Developer Community での問題の報告に関するポップアップ](media/installer.png)

1. **[問題の報告]** をクリックすると、既定のブラウザーが開き、Visual Studio へのサインインで使用するものと同じアカウントでサインインされます。

   ![サインインして問題を報告する](../ide/media/feedback-browser-top.png)

1. まず、バグ レポートのわかりやすいタイトルを入力します。 25 文字以上になるようにしてください。

    ![問題を報告する](../ide/media/feedback-report.png)

1. 入力を開始すると、タイトル フィールドの下に重複の可能性が表示されます。

    ![重複を検索する](../ide/media/feedback-search.png)

1. 重複している可能性のあるバグ レポートを選択して、自分の問題に一致するものがあるかどうかを確認します。 一致するものがある場合、独自のチケットを作成せず、それに投票します。

    ![重複に投票する](../ide/media/feedback-duplicate.png)

2. 重複が見つからなかった場合は、引き続き、問題の説明を入力します。 Microsoft がバグを再現できる可能性を上げるため、可能な限りわかりやすく説明することが重要です。 わかりやすい再現手順を必ず含めてください。

3. バグ レポートに関連する場合、 *[Include Visual Studio screenshot]\(Visual Studio スクリーンショットを含める\)* チェックボックスを選択し、スクリーンショットを作成します。

    ![スクリーンショットを作成する](../ide/media/feedback-screenshot.png) *Microsoft のエンジニアだけがこのスクリーンショットを見ることができます*

    スクリーンショットはブラウザー内で直接トリミングし、機密情報や関係のない部分を削除することもできます。

4. Visual Studio エンジニアリング チームの問題解決を支援する最良の方法の 1 つは、チームが参照するためのトレースとヒープ ダンプのファイルを提供することです。 これは、バグを発生させた手順を記録するだけで簡単に行うことができます。 

    ![手順を記録する](../ide/media/feedback-recording.png) *Microsoft のエンジニアだけがこの記録を見ることができます*

5. 添付ファイルを見直し、問題の診断に役立つと思われる場合は追加のファイルをアップロードします。   

    ![添付ファイル](../ide/media/feedback-attachments.png) *Microsoft のエンジニアだけが添付ファイルを見ることができます*

6. 最後の手順は **[送信]** ボタンをクリックすることです。 レポートを送信すると、トリアージを待機している内部 Visual Studio バグ報告システムにレポートが直接送信されます。

## <a name="when-further-information-is-needed"></a>さらに情報が必要な場合

Microsoft では、イシューに重要な情報が含まれていない場合、"**詳細情報が必要**" 状態を割り当てます。 必要な特定の情報と合わせてイシューについてコメントし、ユーザーは電子メール通知を受け取ります。 7 日以内に情報を受信しない場合は、ユーザーにリマインダーを送信します。 その後、14 日間の非アクティブ状態を経て、チケットを終了します。

1. 電子メールに含まれるリンクをクリックして問題のレポートに進むか、[マイ フィードバック] に進み、"**詳細情報が必要**" 状態のすべてのレポートを確認します。

    ![マイ フィードバック](../ide/media/feedback-my-feedback.png)

1. 問題のレポートで [さらに情報を提供] リンクを選択すると、新しい画面が表示されます。 要求されている情報をそこで確認できます。

   ![マイ フィードバック](../ide/media/feedback-need-more-info.png)

1. コメントや添付ファイルを追加するか、手順を記録することで、さらに情報を提供することができます。 このエクスペリエンスは、新しい問題を報告することや、問題への投票時に追加情報を提供することと似ています。

1. 要求側の Microsoft エンジニアは、提供された追加情報に関する通知を受け取ります。 調査に十分な情報がある場合は、問題の状態が変わります。 それ以外の場合、エンジニアはさらに情報を求めます。

**[マイ フィードバック]** 画面にはそれらの要求と共に他のすべての **[問題]** と **[提案]** を確認できます。

## <a name="search-for-solutions-or-provide-feedback"></a>解決策を検索するかフィードバックを提供する

Visual Studio を使用して問題を報告したくない場合、またはできない場合は、既に問題が報告され、[Visual Studio Developer Community](https://developercommunity.visualstudio.com/) ページに解決策が投稿されている可能性があります。

レポートする問題はないが、機能を提案したい場合は、そのための場所も用意されています。 詳細については、「[Suggest a feature](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)」(機能を提案する) ページをご覧ください。

## <a name="see-also"></a>関連項目

* [開発者コミュニティのガイドライン](./developer-community-guidelines.md)
* [Visual Studio フィードバック オプション](../ide/feedback-options.md)
* [Visual Studio for Mac に関する問題を報告する](/visualstudio/mac/report-a-problem)
* [C++ に関する問題を報告する](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset)
* [Visual Studio 開発者コミュニティ](https://developercommunity.visualstudio.com/)
* [開発者コミュニティのデータのプライバシー](developer-community-privacy.md)