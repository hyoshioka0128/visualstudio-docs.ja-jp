---
title: テスト用ツール
description: Visual Studio のテスト ツールを使用することで、チームと共に高水準の優れたコードを開発し、維持する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/16/2018
ms.topic: conceptual
helpviewer_keywords:
- testing tools [Visual Studio]
- unit tests [Visual Studio]
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: f5eff2257988a4210e7f4cd8a8a37c66c57c185d
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328692"
---
# <a name="first-look-at-testing-tools-in-visual-studio"></a>初めて Visual Studio のテスト ツールを検討する

Visual Studio のテスト ツールを使用することで、チームと共に高水準の優れたコードを開発し、維持できます。

> [!NOTE]
> 単体テストは、Visual Studio のすべてのエディションで使用できます。 ライブ単体テスト、IntelliTest、コード化された UI テストなど、その他のテスト ツールは Visual Studio Enterprise エディションでのみ使用できます。 エディションの詳細については、[Visual Studio IDE の比較](https://visualstudio.microsoft.com/vs/compare/)に関するページを参照してください。

## <a name="test-explorer"></a>テスト エクスプローラー

**[テスト エクスプローラー]** ウィンドウは、開発者が単体テストを作成、管理、実行する場合に役立ちます。 Microsoft 単体テスト フレームワークまたは複数のサードパーティ フレームワークやオープン ソース フレームワークの 1 つを使用できます。

::: moniker range="vs-2017"
![Visual Studio テスト エクスプローラー](media/devtest-testexplorer.png)
::: moniker-end

::: moniker range="vs-2019"
![Visual Studio テスト エクスプローラー 16.2](media/vs-2019/test-explorer-16-2.PNG)
::: moniker-end

* [単体テストの概要](unit-test-your-code.md)
* [テスト エクスプローラーを使用して単体テストを実行する](run-unit-tests-with-test-explorer.md)
* [テスト エクスプローラーに関する FAQ](test-explorer-faq.md)
* [サードパーティ製の単体テスト フレームワークをインストールする](install-third-party-unit-test-frameworks.md)

Visual Studio は拡張可能であり、NUnit や xUnit.net などのサード パーティの単体テスト アダプターにも対応します。 さらに、コード クローン機能では、一般的なバグの修正またはリファクタリングの対象になる可能性がある意味的に似たコードのブロックを特定できるようにして、高品質なソフトウェアを提供することもできます。

![サード パーティ テストの統合](media/devtest-thirdparty.png)

## <a name="live-unit-testing"></a>Live Unit Testing

[Live Unit Testing](../test/live-unit-testing.md) は、バックグラウンドで自動的に単体テストを実行し、Visual Studio のコード エディターにコード カバレッジとテスト結果をグラフィカルに表示します。

## <a name="intellitest"></a>IntelliTest

IntelliTest は、マネージド コードの単体テストとテスト データを自動生成します。 IntelliTest によって、対象範囲が増え、新規または既存のコードの単体テストを作成および保守する手間を大幅に削減できます。

![実行中の IntelliTest](media/devtest-intellitest.png)

* [IntelliTest でのコードの単体テストの生成](generate-unit-tests-for-your-code-with-intellitest.md)
* [IntelliTest – 1 回のテストですべてのルールを把握](https://devblogs.microsoft.com/devops/intellitest-one-test-to-rule-them-all/)
* [IntelliTest リファレンス マニュアル](intellitest-manual/index.md)

## <a name="code-coverage"></a>コード カバレッジ

[コード カバレッジ](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)は、プロジェクトのコードの中で、単体テストなどのコード化されたテストによって実際にテストされる割合を判断します。 バグから効果的に保護するには、コードの大部分を "カバー" するようにテストを実行する必要があります。

コード カバレッジ分析は、マネージド コードにもアンマネージド (ネイティブ) コードにも適用できます。

コード カバレッジは、テスト エクスプローラーを使用してテスト メソッドを実行する場合のオプションです。 結果テーブルには、各アセンブリ、クラス、およびメソッドで実行されたコードの割合が表示されます。 また、ソース エディターには、どのコードがテストされたかが表示されます。

* [コード カバレッジを使用した、テストされるコード割合の確認](using-code-coverage-to-determine-how-much-code-is-being-tested.md)
* [Visual Studio での単体テスト、コード カバレッジおよびコード クローン分析 (ラボ)](https://www.boost.org/doc/libs/1_71_0/libs/test/doc/html/index.html)
* [コード カバレッジ分析のカスタマイズ](customizing-code-coverage-analysis.md)

## <a name="microsoft-fakes"></a>Microsoft Fakes

[Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md) では、アプリケーションの別の部分をスタブまたは shim で置き換えることにより、テストするコードを分離できます。

## <a name="user-interface-testing-with-coded-ui-and-selenium"></a>コード化された UI と Selenium によるユーザー インターフェイスのテスト

コード化された UI テストでは、アプリケーションのユーザー インターフェイスの機能と動作を検証するために完全に自動化されたテストを作成できます。 XAML ベースの UWP アプリ、ブラウザー アプリ、および SharePoint アプリなど、さまざまなテクノロジをカバーする UI テストを自動化できます。

コード化された UI テストまたは汎用ブラウザー ベースの UI テストと Selenium の最適な組み合わせを選択したかどうかに関係なく、Visual Studio では必要なツールがすべて提供されます。

![コード化された UI を使用した UI テスト](media/devtest-codeduitest.png)

* [UI オートメーションを使用してコードをテストする](use-ui-automation-to-test-your-code.md)
* [コード化された UI テストの作成、編集、および保守の概要](walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
* [コード化された UI テストを使用して UWP アプリをテストする](test-uwp-app-with-coded-ui-test.md)
* [Visual Studio Enterprise でのコード化された UI テストの概要 (ラボ)](https://www.boost.org/doc/libs/1_71_0/libs/test/doc/html/index.html)

## <a name="load-testing"></a>ロード テスト

[ロード テスト](../test/quickstart-create-a-load-test-project.md)では、単体テストと Web パフォーマンス テストを実行することでサーバー アプリケーションの負荷をシミュレーションします。

## <a name="related-scenarios"></a>関連するシナリオ

* [探索的テストと手動テスト (Azure Test Plans)](/azure/devops/test/index?view=vsts&preserve-view=true)
* [ロード テスト (Azure Test Plans)](/azure/devops/test/load-test/index?view=vsts&preserve-view=true)
* [継続的なテスト (Azure Test Plans)](/azure/devops/pipelines/test/getting-started-with-continuous-testing?view=vsts&preserve-view=true)
* [コード分析ツール](../code-quality/code-analysis-for-managed-code-overview.md)
