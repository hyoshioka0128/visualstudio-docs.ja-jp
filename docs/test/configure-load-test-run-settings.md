---
title: ロード テストの実行設定の構成
ms.date: 10/03/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, configuring run settings
ms.assetid: 0c86918b-cd63-4468-8f49-6d547a1276dc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a485b3648f69276c0d1cc472dda70524a00d9c1c
ms.sourcegitcommit: 9c57730000d5ced37d3887f3928b17076f49d0f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92099415"
---
# <a name="configure-load-test-run-settings"></a>ロード テストの実行設定の構成

*実行設定*とは、ロード テストの実行方法に影響を与えるプロパティのセットです。 実行設定は、 **[プロパティ]** ウィンドウでカテゴリ別に整理されています。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

ロード テストでは複数の実行設定を使用できますが、1 回の実行でアクティブにできる実行設定は 1 つのみです。 その他の実行設定は、後続のテスト実行で使用するための代替設定をすばやく選択するために使用できます。

**新しいロード テスト ウィザード**を使用して新しいロード テストを作成するときに、初期の実行設定が作成されます。

![ロード テストの実行設定](../test/media/loadtestrunsettings.png)

## <a name="tasks"></a>タスク

|タスク|関連するトピック|
|-|-|
|**ロード テストに実行設定を追加する:** さまざまな条件でテストを実行できるように、**新しいロード テスト ウィザード**を実行して作成された実行設定に加えて、それ以外の実行設定をロード テストに追加できます。|-   [方法: ロード テストに追加の実行設定を追加する](../test/how-to-add-additional-run-settings-to-a-load-test.md)|
|**ロード テストで使用するアクティブな実行設定を指定する:** ロード テスト エディターを使用してロード テストで使用する実行設定を選択できます。 アクティブな実行設定は "[Active]" というサフィックスで識別されます。|-   [方法: ロード テストのアクティブな実行設定を選択する](../test/how-to-select-the-active-run-setting-for-a-load-test.md)|
|**実行設定プロパティを編集する:** ログ オプション (以下を参照) などの実行設定プロパティを編集して、テストの長さ、ウォームアップ期間、報告されるエラー詳細の最大数、サンプル速度、接続モデル (Web パフォーマンス テストのみ)、結果ストレージの種類、検証レベル、SQL トレースを決定できます。 実行設定は、ロード テストの目的を反映している必要があります。|-   [ロード テストの実行設定のプロパティ](../test/load-test-run-settings-properties.md)<br />-   [実行設定プロパティの変更](../test/load-test-run-settings-properties.md#change-run-setting-properties)|
|**ロード テストの実行設定でテストの反復回数を指定する:** **[テスト イテレーション]** プロパティを構成して、ロード テストのすべてのシナリオですべての Web パフォーマンス テストと単体テストを実行する回数を指定できます。|-   [方法: テスト イテレーションの数を実行設定に指定する](../test/how-to-specify-the-number-of-test-iterations-in-a-load-test.md)|
|**ロード テストの実行設定にサンプル速度を指定する:** **[サンプル速度]** プロパティを構成して、ロード テスト中にパフォーマンス カウンター データを収集する頻度を指定できます。|-   [方法: サンプル速度を指定する](../test/how-to-specify-the-sample-rate-for-a-load-test.md)|
|**タイミングの詳細ストレージ オプションを指定する:** **[タイミングの詳細ストレージ]** プロパティを構成して、ロード テストの詳細を保存する方法を指定できます。|-   [方法: [タイミングの詳細ストレージ] プロパティを指定する](../test/how-to-specify-the-timing-details-storage-property-for-a-load-test.md)|
|**テスト リソースの保持時間を指定する:** **[リソース保持時間]** プロパティを設定して指定した期間、テスト リソースを保持することにより、テスト > 修正 > 再テストのサイクルを高速化することができます。|-   [ロード テストを高速化するためにリソースを保持する](/azure/devops/test/load-test/getting-started-with-performance-testing?view=vsts&preserve-view=true)|
|**コンテキスト パラメーターを使用する:** 文字列のパラメーター化にコンテキスト パラメーターを使用できます。 たとえば、ロード テストにパラメーター化された Web サーバーを使用する Web パフォーマンス テストを含めると、別のサーバーにマップするコンテキスト パラメーターを実行設定に追加できます。|-   [方法: 実行設定にコンテキスト パラメーターを追加する](../test/how-to-add-context-parameters-to-a-load-test-run-setting.md)|
|**テスト ログ プロパティを構成する:** ロード テストの実行設定に関連付けられているログにデータを書き込む頻度を構成できます。 大規模で複雑なロード テストを実行するとログのサイズが数ギガバイトに達する場合があるので、この設定は重要です。<br /><br /> また、アプリケーションのデバッグと分析でロード テストが失敗したときにログ ファイルが自動的に保存されるように構成できます。|-   [ロード テストのログ設定の変更](../test/modify-load-test-logging-settings.md)|