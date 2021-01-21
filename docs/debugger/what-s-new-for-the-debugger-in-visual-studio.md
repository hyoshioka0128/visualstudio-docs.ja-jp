---
title: Visual Studio 2017 のデバッガーの新機能 | Microsoft Docs
titleSuffix: ''
description: 'デバッガー バージョン 15.5 の新機能を確認します。 含まれるもの: 実稼働アプリ内の選択したコード、Intellitrace のステップ バックのスナップショット。'
ms.custom: SEO-VS-2020
ms.date: 01/22/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, what's new
- what's new [debugger]
- debugging [Visual Studio], what's new
- what's new [Visual Studio], debugging
ms.assetid: 2aed9caa-2384-4e49-8595-82d8b06cf271
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 986ebf20cd49569bfcaf471b9bef994dfe774437
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98149405"
---
# <a name="whats-new-for-the-debugger-in-visual-studio-2017"></a>Visual Studio 2017 のデバッガーの新機能

デバッガーには、次の新機能があります。

- バージョン 15.5 の新機能: **スナップショット デバッガー** では、関心があるコードの実行時に実稼働アプリのスナップショットが取得されます。 スナップショットを取得するようにデバッガーに指示するには、コードでスナップショットとログポイントを設定します。 デバッガーでは、実稼働アプリケーションのトラフィックに影響を与えることなく、問題を正確に確認できます。 スナップショット デバッガーは、実稼働環境で発生する問題の解決にかかる時間を大幅に短縮するのに役立ちます。

    スナップショット コレクションは、Azure App Service で実行されている次の Web アプリで利用できます。

  * .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
  * Windows の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。

    詳細については、「[Debug live ASP.NET apps using the Snapshot Debugger](../debugger/debug-live-azure-applications.md)」(スナップショット デバッガーを使用してライブ ASP.NET アプリをデバッグする) を参照してください。

- Visual Studio Enterprise バージョン 15.5 のみの新機能: **IntelliTrace のステップ バック** では、ブレークポイントとデバッガー ステップ イベントごとにアプリケーションのスナップショットを自動作成します。 記録されたスナップショットにより、前のブレークポイントまたはステップに戻り、過去の時点でのアプリケーションの状態を確認できるようになります。 IntelliTrace ステップ バックでは、以前のアプリケーションの状態を確認したいが、デバッグの再開や必要なアプリ状態の再作成は必要でない場合に時間を節約できます。

    スナップショット間を移動して表示するには、デバッグ ツールバーの **[前に戻る]** ボタンと **[次へ進む]** ボタンを使用します。 これらのボタンを使用して、 **[診断ツール]** ウィンドウの **[イベント]** タブに表示されるイベント間を移動します。

    ![[前に戻る] ボタンと [次へ進む] ボタン](../debugger/media/intellitrace-step-back-icons-description.png  "[前に戻る] ボタンと [次へ進む] ボタン")

    詳細について、[IntelliTrace を使用して以前のアプリの状態を検査する](view-historical-application-state.md)方法に関するページを参照してください。

- **例外ヘルパー** は例外処理アシスタントに代わる機能で、エラーが発生した非モーダル ダイアログ ボックスに表示されます。 **例外ヘルパー** を使用すると、内部例外へのすばやくいクセス、デバッガーによる追加の分析 (利用可能な場合)、例外の **例外設定** へのすばやいアクセスが可能です。 見る必要があるものが例外ヘルパーによってブロックされている場合は、例外ヘルパーをフローティング ビューにドラッグすることもできます。

    たとえば、**NullReferenceException** では、null 参照を行っている変数が表示されるようになりました (追加情報)。

    ![デバッガーの例外ヘルパー](../debugger/media/dbg-exception-helper.png "DbgExceptionHelper")

    詳細については、「[Using the New Exception Helper in Visual Studio](https://devblogs.microsoft.com/devops/using-the-new-exception-helper-in-visual-studio-15-preview/)」 (Visual Studio で新しい例外ヘルパーを使用する) のブログの投稿を参照してください。

- **[ここまで実行します]** の緑色の矢印アイコンを選択することで、デバッガーで一時停止中にコード行を実行できるようになりました (コード行をポイントするとアイコンが表示されます)。 これにより、一時的なブレークポイントを設定する必要がなくなります。

    ![デバッガーのクリックして実行](../debugger/media/dbg-run-to-click.png "DbgRunToClick")

- **[例外設定]** ダイアログ ボックスで例外での条件を設定できます (これは、[例外設定] ダイアログ ボックスの **[条件の編集]** アイコンを使用するか、例外の右クリック メニューを使用して行うことができます)。現在サポートされているのは、例外の条件としてモジュール名を含めるか除外するかです。

    ![例外の条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

- [プロセスにアタッチ] ダイアログ ボックスには、アタッチする必要があるプロセスをより迅速に識別するのに役立つ新しい検索機能が追加されています。

    ![[プロセスにアタッチ] で検索する](../debugger/media/dbg-attach-to-process-search.png "DbgAttachToProcessSearch")

サポートされている機能の詳細については、[[!include[vs_dev15](../misc/includes/vs_dev15_md.md)] のリリース ノート](/visualstudio/releasenotes/vs2017-relnotes)を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)