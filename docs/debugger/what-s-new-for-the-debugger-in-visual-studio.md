---
title: Visual Studio 2017 でのデバッガーの新機能 |Microsoft Docs
titleSuffix: ''
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
ms.openlocfilehash: 523867a8f9aa074e9122c74deb8bcd91cddd8bee
ms.sourcegitcommit: 9a66f1c31cc9eba0b5231af72da1d18761a9c56a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75944227"
---
# <a name="whats-new-for-the-debugger-in-visual-studio-2017"></a>Visual Studio 2017 のデバッガーの新機能

デバッガーには、次の新機能があります。

- バージョン15.5 の新動作では、対象となるコードが実行されるときに、**スナップショットデバッガー**は実稼働アプリのスナップショットを取得します。 スナップショットを取得するようにデバッガーに指示するには、コードでスナップショットとログポイントを設定します。 デバッガーでは、実稼働アプリケーションのトラフィックに影響を与えることなく、問題を正確に確認できます。 スナップショット デバッガーは、実稼働環境で発生する問題の解決にかかる時間を大幅に短縮するのに役立ちます。

    スナップショット コレクションは、Azure App Service で実行されている次の Web アプリで利用できます。

  * .NET Framework 4.6.1 以降で実行されている ASP.NET アプリケーション。
  * Windows の .NET Core 2.0 以降で実行されている ASP.NET Core アプリケーション。

    詳細については、「[Debug live ASP.NET apps using the Snapshot Debugger](../debugger/debug-live-azure-applications.md)」(スナップショット デバッガーを使用してライブ ASP.NET アプリをデバッグする) を参照してください。

- Visual Studio Enterprise のみのバージョン15.5 で新しくなった**IntelliTrace ステップバック**では、すべてのブレークポイントとデバッガーステップイベントで、アプリケーションのスナップショットが自動的に取得されます。 記録されたスナップショットにより、前のブレークポイントまたはステップに戻り、過去の時点でのアプリケーションの状態を確認できるようになります。 IntelliTrace ステップ バックでは、以前のアプリケーションの状態を確認したいが、デバッグの再開や必要なアプリ状態の再作成は必要でない場合に時間を節約できます。

    スナップショット間を移動して表示するには、デバッグ ツールバーの **[前に戻る]** ボタンと **[次へ進む]** ボタンを使用します。 これらのボタンを使用して、 **[診断ツール]** ウィンドウの **[イベント]** タブに表示されるイベント間を移動します。

    ![[前に戻る] ボタンと [次へ進む] ボタン](../debugger/media/intellitrace-step-back-icons-description.png  "[前に戻る] ボタンと [次へ進む] ボタン")

    詳細について、[IntelliTrace を使用して以前のアプリの状態を検査する](view-historical-application-state.md)方法に関するページを参照してください。

- 例外**ヘルパー**は、例外処理アシスタントを置き換え、エラーが発生した非モーダルダイアログボックスに表示されます。 **例外ヘルパー**を使用すると、内部例外にすばやくアクセスでき、デバッガーによる追加の分析 (利用可能な場合) が可能になり、例外の**例外設定**にすぐにアクセスできるようになります。 例外ヘルパーは、表示する必要があるものをブロックしている場合に、フローティングビューにドラッグすることもできます。

    たとえば、 **NullReferenceException**は、null 参照 (追加情報) を持つ変数を表示するようになりました。

    ![デバッガーの例外ヘルパー](../debugger/media/dbg-exception-helper.png "DbgExceptionHelper")

    詳細については、「[Using the New Exception Helper in Visual Studio](https://devblogs.microsoft.com/devops/using-the-new-exception-helper-in-visual-studio-15-preview/)」 (Visual Studio で新しい例外ヘルパーを使用する) のブログの投稿を参照してください。

- デバッガーで一時停止中にコード行を実行できるようになりました。**この**緑色の矢印アイコンをクリックすると、コード行の上にカーソルを置くとアイコンが表示されます。 これにより、一時的なブレークポイントを設定する必要がなくなります。

    ![デバッガーの実行をクリックします](../debugger/media/dbg-run-to-click.png "DbgRunToClick")

- 例外 **[設定]** ダイアログボックスで例外の条件を設定できます (これを行うには、例外設定 ダイアログボックスの **[条件の編集]** アイコンを使用するか、例外の右クリックメニューを使用します)。現在サポートされている条件には、例外に含めたり除外したりするモジュール名が含まれます。

    ![例外に関する条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

- [プロセスにアタッチ] ダイアログボックスには、アタッチする必要があるプロセスをより迅速に識別するのに役立つ新しい検索機能が追加されています。

    ![プロセスにアタッチして検索](../debugger/media/dbg-attach-to-process-search.png "DbgAttachToProcessSearch")

これらの新機能の詳細については、 [[!include[vs_dev15](../misc/includes/vs_dev15_md.md)]のリリースノート](/visualstudio/releasenotes/vs2017-relnotes)を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)