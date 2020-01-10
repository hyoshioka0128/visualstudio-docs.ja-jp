---
title: 問題レポートのプライベート データ
ms.date: 06/21/2018
ms.topic: conceptual
helpviewer_keywords:
- developer community privacy
- privacy, developer community
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 09f3e5fed93cac3a251e4b7cdcaa988e63ff8741
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75596269"
---
# <a name="developer-community-data-privacy"></a>開発者コミュニティのデータのプライバシー

既定では、[開発者コミュニティ](https://developercommunity.visualstudio.com/)の問題レポートのすべての情報 (すべてのコメントと返信を含む) は、公開されます。 これには、コミュニティ全体が問題、解決策、および他のユーザーが見つけた回避策を閲覧できるという利点があります。 ただし、自分のデータや ID のプライバシーについて心配がある場合には、オプションがあります。

## <a name="identity-privacy"></a>ID プライバシー

身元を公開することについて心配がある場合は、個人情報を公開しない[新しい Microsoft アカウントを作成](https://signup.live.com/)します。 このアカウントを使用してレポートを作成します。

## <a name="data-privacy"></a>データのプライバシー

データのプライバシーについて心配がある場合は、常に公開される最初のレポートのタイトルや内容に、公開したくないことを含めないでください。 代わりに、レポートを作成して、別のコメントで詳細を非公開で送信することができます。 問題レポートが作成されると、返信と添付ファイルを閲覧できる人を指定することができます。

1. 作成したレポートで、 **[コメントの追加]** を選択して、問題の個人的な詳細を作成します。

2. 返信エディターで、 **[送信]** ボタンと **[キャンセル]** ボタンの下のコントロールを使用して、返信を閲覧できる人を指定します。 閲覧できるのを Microsoft の従業員と自分に制限するには、 **[Viewable by moderators and the original poster]\(モデレーターと元の投稿者が閲覧可能\)** を選択します。

   ![開発者コミュニティでのプライバシー コントロール](media/developer-community-privacy-control.png)

   指定された人だけがコメントと、それに含まれるイメージ、リンク、またはコードを閲覧できます。 コメントの下の返信はすべて、元のコメントと同じ表示設定になります。 これは、応答のプライバシー コントロールに閲覧制限の状態が正しく表示されていない場合でも当てはまります。

3. 説明と、問題の再現に必要なその他の情報、イメージ、および、添付ファイルを追加します。 **[送信]** ボタンを選択して、非公開でこの情報を送信します。

   > [!NOTE]
   > 添付ファイルには 2 GB の制限があり、最大で 10 個のファイルに制限されています。 これより大きいファイルをアップロードする必要がある場合は、新しい問題レポートを送信するか、プライベート コメントで Microsoft の社員にアップロード URL を要求できます。

お客様のプライバシーと機密情報が公開されないようにするため、Microsoft とのすべてのやり取りは、この表示制限付きのコメントの下で返信するように注意してください。 他のコメントに返信すると、機密情報が誤って公開される場合があります。

## <a name="data-we-collect"></a>収集されるデータ

**問題の報告**が Visual Studio インストーラーから開始された場合、最新のセットアップ ログが収集されます。

**問題の報告**が Visual Studio から開始された場合、次の 1 つ以上の種類のデータが収集されます。

- イベント ログからの Watson エントリと .NET エントリ

- Visual Studio のメモリ内アクティビティ ログ ファイル

- PerfWatson ファイル (Watson コレクションが有効になっている場合)

- LiveShare ログ ファイル (存在する場合)

- Xamarin ログ ファイル (存在する場合)

- Nuget ログ ファイル (存在する場合)

- Web デバッガー ログ ファイル (存在する場合)

- Service Hub ログと MEF エラー ログ (存在する場合)

- Python ログ (存在する場合)

- Windows フォーム ログ (存在する場合)

- スクリーン ショット (含めることを選択した場合)

- 記録データ (以下を含む記録を含めるように選択した場合)

  - 問題を再現する手順

  - ETL トレース ファイル

  - ダンプ ファイル

> [!NOTE]
> ログ ファイル、スクリーンショット、および記録データは、それらが含まれている問題レポートを送信してアクセス許可を付与した場合にのみ、Microsoft に送信されます。 [問題の報告] ウィンドウの [サマリー] ステップで、どのファイルが含まれているかを確認できます (このメモのスクリーンショットを参照)。 収集されたログとファイルは %temp% フォルダーに格納され、定期的に、および各アップロードの後で、クリーンアップされます。 問題レポートにログを含めたくない場合は、レポートを送信する前に、%temp% フォルダーからファイルを削除します。
  > ![問題の報告 - 収集されたログのサマリー](media/report-a-problem-logs-collected.png)


## <a name="see-also"></a>関連項目

- [Visual Studio 2017 で問題を報告する方法](how-to-report-a-problem-with-visual-studio.md)
- [C++ の問題レポート データのプライバシー](/cpp/how-to-report-a-problem-with-the-visual-cpp-toolset#reports-and-privacy)
