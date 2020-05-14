---
title: コード化された UI テストでのさまざまな Web ブラウザーの使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: a859595f-6517-43f2-9d61-c706cb55a388
caps.latest.revision: 25
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5234dddad13ccb52cc653a68ad1c35370a4eae18
ms.sourcegitcommit: da5ebc29544fdbdf625ab4922c9777faf2bcae4a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82586336"
---
# <a name="using-different-web-browsers-with-coded-ui-tests"></a>コード化された UI テストでのさまざまな Web ブラウザーの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード化された UI テストでは、Internet Explorer を使用してテストを記録することによって、Web アプリケーションのテストを自動化できます。 その後、テストをカスタマイズし、Internet Explorer や Web アプリケーションに対応している他の種類のブラウザーを使用して再生できます。

 **必要条件**

- Visual Studio Enterprise

- オペレーティング システム:

  - Microsoft Windows 7

  - Microsoft Windows 8

  - Microsoft Windows Server 2008 R2 SP1

- Web ブラウザーのバージョン:

  - Windows Internet Explorer 9

  - Windows Internet Explorer 10

  - Mozilla Firefox と Google Chrome のサポートされているバージョンについては、[こちら](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)を参照してください。

- [コード化された UI のクロス ブラウザー テスト用に Selenium コンポーネント](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)をインストールします。

  **すべての web ブラウザーでサポートされているもの**

- プロパティ、検索、再生待機処理などの[機能を制御するためのカスタム コードを追加](https://devblogs.microsoft.com/devops/coded-ui-test-configuring-search-properties-while-recording-on-internet-explorer/)します。

- ポップアップとダイアログ ボックス

- [戻り値の型を持たない基本 JavaScript を実行します](https://devblogs.microsoft.com/devops/introducing-javascript-execution-on-internetexplorer-and-crossbrowser-in-coded-ui-test/)

- 検索の回復機能 (スマート一致を使用) と[パフォーマンスの向上](https://devblogs.microsoft.com/devops/guidelines-on-improving-performance-of-coded-ui-test-playback/)

## <a name="why-should-i-use-coded-ui-tests-across-multiple-web-browser-types"></a>コード化された UI テストを複数の Web ブラウザーの種類で使用する理由
 さまざまな種類の Web ブラウザーを使用して Web アプリケーションをテストすることにより、さまざまなブラウザーを実行するユーザーの UI 操作をより適切にエミュレートできます。 たとえば、他の Web ブラウザーとの互換性がない、Internet Explorer のコントロールまたはコードが、アプリケーションに含まれていることがあります。 コード化された UI テストを他のブラウザーでも実行することにより、ユーザーへの影響が生じる前に問題を検出して修正できます。

## <a name="how-do-i-record-and-play-back-coded-ui-tests-on-web-applications-using-the-supported-web-browsers"></a>サポートされている Web ブラウザーを使用して、Web アプリケーションでコード化された UI テストを記録および再生する方法
 **記録:** Internet Explorer を使用する Web アプリケーション テストを記録するには、コード化された UI テスト ビルダーを使用する必要があります。 コード化された UI テストで通常行うように、定義済みプロパティ セットを使用して、テストされるコントロールの検証コードとカスタム コードを必要に応じて追加できます。 詳細については、「[UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)」を参照してください。

> [!NOTE]
> Google Chrome や Mozilla Firefox ブラウザーを使用して、コード化された UI テストを記録することはできません。

 **Internet Explorer での再生:** ブラウザーが明示的に指定されていない場合、テストは既定では Internet Explorer で実行されます。 使用されるブラウザーを明示的に指定するには、テスト コードで **BrowserWindow.CurrentBrowser** プロパティを設定します。 Internet Explorer の場合は、このプロパティを **IE** または **Internet Explorer** に設定する必要があります。

 **Internet Explorer 以外の Web ブラウザーでの再生:** Internet Explorer 以外の Web ブラウザーで再生する場合は、テスト コードで BrowserWindow.CurrentBrowser プロパティを **Firefox** または **Chrome** に変更します。

 IE 以外の Web ブラウザーでテストを再生するには、**コード化された UI のクロス ブラウザー テスト用に Selenium コンポーネント**をインストールする必要があります。

#### <a name="installing-selenium-components"></a>Selenium コンポーネントをインストールする

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. [拡張機能と更新プログラム] ダイアログ ボックスで、`Selenium components for Cross Browser Testing` を検索します。

3. 拡張機能を強調表示し、**[ダウンロード]** を選択します。

   > [!TIP]
   > コード化された UI のクロス ブラウザー テスト用 Selenium コンポーネントは、[こちら](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)からもダウンロードできます。

   コード化された UI テストの作成方法と使用方法の詳細については、「[コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)」を参照してください。

### <a name="enable-debugging"></a>デバッグの有効化
 Web アプリケーションのデバッグを有効にするには、以下の構成オプションを設定する必要があります。

1. マイ コードのみを有効にする:

    1. **[ツール]** メニューの **[オプション]** を選択し、**[デバッグ]** を選択します。

    2. **[マイ コードのみを有効にする]** を選択します。

2. CLR 例外を無効にする:

    1. **[デバッグ]** メニューの **[例外]** を選択します。

    2. **[共通言語ランタイム例外]** で、**[ユーザーにハンドルされていないとき]** をオフにします。

## <a name="i-dont-see-the-option-to-change-browserwindowcurrentbrowser-in-the-coded-ui-test"></a><a name="generate"></a> *コード化された UI テストで、BrowserWindow.CurrentBrowser を変更するオプションが表示されません。*
 さまざまな Web ブラウザーを使用するコード化された UI テストをサポートしないバージョンの [!INCLUDE[vs2011_first](../includes/vs2011-first-md.md)] を使用している可能性があります。 そのようなコード化された UI テストを使用するには、Visual Studio Enterprise を使用する必要があります。

 *その他に知っておく必要があること*
 **メモ**

- ![Prerequsite](../test/media/prereq.png "前提条件")Apple Safari web ブラウザーはサポートされていません。

- ![Prerequsite](../test/media/prereq.png "前提条件")Web ブラウザーを起動するアクションは、コード化された UI テストの一部である必要があります。

   既に Web ブラウザーが開かれていて、そこで手順を実行すると、Internet Explorer を使用していない場合は再生が失敗します。 そのため、コード化された UI テストの一部として Web ブラウザーの起動を含めることをお勧めします。

- ![Prerequsite](../test/media/prereq.png "前提条件")最大化、最小化、復元など、ブラウザー固有の UI 操作の自動化はサポートされていません。

  **ヒント**

- ![ヒント](../test/media/tip.png "ヒント")出力を構成して、コード化された UI ログにスクリーンショットを含めることができます。 そのためには、QTAgent32.exe.config ファイルの一部の構成設定を設定する必要があります。 既定では、このファイルは次の場所にインストールされます。

   **C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE**

   次の値を設定します。

  - `EqtTraceLevel` セクションの `system.diagnostics`。

  - `<add name="EqtTraceLevel" value="4" />`

     値を 3 以上に設定すると、操作ごとにスクリーン ショットが取得されます。 値を 1 または 2 に設定すると、エラー操作のみでスクリーンショットが取得されます。

    詳細については、「[コード化された UI テスト ログを使用したコード化された UI テストの分析](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)」をご覧ください。

## <a name="external-resources"></a>外部リソース

### <a name="videos"></a>ビデオ
 [IE で記録し、任意の場所で再生する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!183&authkey=!ANqaLtCZbtJrImU)

 [コード化された UI テスト ビルダーでクロス ブラウザー テストを作成する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!184&authkey=!AKG8CSow_qmeTq8)

 [UI マップを使わずに手作業のコーディングでクロス ブラウザー テストを作成する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!186&authkey=!AJaEvxJnsefyAT4)

 [複数のブラウザー上で順番にクロス ブラウザー テストを実行する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!187&authkey=!ADI8eCQkxHnpOR8)

 [クロス ブラウザー テストのエラーのトラブルシューティング](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!182&authkey=!AEpS48i295B49FI)

### <a name="guidance"></a>ガイダンス
 [Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 2 章: 単体テスト: 内部のテスト](https://msdn.microsoft.com/library/jj159340.aspx)

 [Visual Studio 2012 を使用した継続的デリバリーのためのテスト–第5章: システムテストの自動化](https://msdn.microsoft.com/library/jj159335.aspx)

### <a name="faq"></a>よく寄せられる質問
 [Coded UI Tests FAQ - 1 (コード化された UI テストの FAQ - 1)](https://docs.microsoft.com/archive/blogs/mathew_aniyan/content-index-for-coded-ui-test)

 [Coded UI Tests FAQ - 2 (コード化された UI テストの FAQ - 2)](https://social.msdn.microsoft.com/Forums/en-US/vsautotest/thread/3a74dd2c-cef8-4923-abbf-7a91f489e6c4)

### <a name="forum"></a>フォーラム
 [Visual Studio の UI オートメーションのテスト (コード化された UI を含む)](https://social.msdn.microsoft.com/Forums/en-US/vsautotest)

## <a name="see-also"></a>参照
 [Ui オートメーションを使用して、コード](../test/use-ui-automation-to-test-your-code.md)化された ui テスト[と操作の記録に対してサポートされている構成とプラットフォームの](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)テストコード化された ui テストの[ログ](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)
