---
title: コード化された UI テストでのさまざまな Web ブラウザーの使用
description: テストをカスタマイズし、Web アプリケーションに対応するさまざまなブラウザーを使用して再生する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 199b8a3852850e1bb3239ad3b70ee5a438d4bcbe
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99850049"
---
# <a name="use-different-web-browsers-with-coded-ui-tests"></a>コード化された UI テストでさまざまな Web ブラウザーを使用する

コード化された UI テストでは、Internet Explorer を使用してテストを記録することによって、Web アプリケーションのテストを自動化できます。 その後、テストをカスタマイズし、Internet Explorer や Web アプリケーションに対応している他の種類のブラウザーを使用して再生できます。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

まず、[コード化された UI のクロス ブラウザー テスト用に Selenium コンポーネント](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)をインストールします。

## <a name="whats-supported-across-all-web-browsers"></a>すべての Web ブラウザーでサポートされている機能

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

IE 以外の Web ブラウザーでテストを再生するには、**コード化された UI のクロス ブラウザー テスト用に Selenium コンポーネント** をインストールする必要があります。

### <a name="install-selenium-components"></a>Selenium コンポーネントをインストールする

::: moniker range="vs-2017"

1. **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

2. **[拡張機能と更新プログラム]** ダイアログ ボックスで、`Selenium components for Cross Browser Testing` を検索します。

::: moniker-end

::: moniker range=">=vs-2019"

1. **[拡張機能]** メニューの **[拡張機能の管理]** を選択します。

2. **[拡張機能の管理]** ダイアログ ボックスで、`Selenium components for Cross Browser Testing` を検索します。

::: moniker-end

3. 拡張機能を強調表示し、**[ダウンロード]** を選択します。

    > [!TIP]
    > コード化された UI のクロス ブラウザー テスト用 Selenium コンポーネントは、[こちら](https://marketplace.visualstudio.com/items?itemName=AtinBansal.SeleniumcomponentsforCodedUICrossBrowserTesting)からもダウンロードできます。

コード化された UI テストの作成方法と使用方法の詳細については、「[コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)」を参照してください。

### <a name="enable-debugging"></a>デバッグの有効化

Web アプリケーションのデバッグを有効にするには、以下の構成オプションを設定する必要があります。

1. マイ コードのみを有効にする:

    1. **[ツール]** メニューの **[オプション]** を選択し、**[デバッグ]** を選択します。

    2. **[マイ コードのみを有効にする]** を選択します。

2. CLR 例外を無効にする:

    1. **[デバッグ]** メニューの **[例外]** を選択します。

    2. **[共通言語ランタイム例外]** で、**[ユーザーにハンドルされていないとき]** をオフにします。

コード化された UI テストの `BrowserWindow.CurrentBrowser` を変更するオプションが表示されない場合、さまざまな Web ブラウザーを使用したコード化された UI テストをサポートしていないバージョンの Visual Studio を使用している可能性があります。 そのようなコード化された UI テストを使用するには、Visual Studio Enterprise Edition を使用する必要があります。

他の注意事項:

- Apple Safari Web ブラウザーはサポートされていません。

- Web ブラウザーを起動する操作は、コード化された UI テストの一部である必要があります。

   既に Web ブラウザーが開かれていて、そこで手順を実行すると、Internet Explorer を使用していない場合は再生が失敗します。 そのため、コード化された UI テストの一部として Web ブラウザーの起動を含めることをお勧めします。

- 最大化、最小化、復元など、ブラウザー固有の UI 操作の自動化はサポートされていません。

## <a name="tips"></a>ヒント

コード化された UI のログにスクリーン ショットを含めるように、出力を構成できます。 そのためには、*QTAgent32.exe.config* ファイルの一部の構成設定を設定する必要があります。 既定では、このファイルは次の場所にインストールされます。

*%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE*

次の値を設定します。

- `EqtTraceLevel` セクションの `system.diagnostics`。

- `<add name="EqtTraceLevel" value="4" />`

   値を 3 以上に設定すると、操作ごとにスクリーン ショットが取得されます。 値を 1 または 2 に設定すると、エラー操作のみでスクリーンショットが取得されます。

詳細については、「[コード化された UI テスト ログを使用したコード化された UI テストの分析](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)」をご覧ください。

## <a name="video-resources"></a>動画リソース

[IE で記録し、任意の場所で再生する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!183&authkey=!ANqaLtCZbtJrImU)

[コード化された UI テスト ビルダーでクロス ブラウザー テストを作成する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!184&authkey=!AKG8CSow_qmeTq8)

[UI マップを使わずに手作業のコーディングでクロス ブラウザー テストを作成する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!186&authkey=!AJaEvxJnsefyAT4)

[複数のブラウザー上で順番にクロス ブラウザー テストを実行する](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!187&authkey=!ADI8eCQkxHnpOR8)

[クロス ブラウザー テストのエラーのトラブルシューティング](https://skydrive.live.com/redir?resid=AE5CD7309CCCC43C!182&authkey=!AEpS48i295B49FI)

## <a name="see-also"></a>関連項目

- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストと操作の記録でサポートされている構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
- [コード化された UI テスト ログを使用してコード化された UI テストを分析する](../test/analyzing-coded-ui-tests-using-coded-ui-test-logs.md)
