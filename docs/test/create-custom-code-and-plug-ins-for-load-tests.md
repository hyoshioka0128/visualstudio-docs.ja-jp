---
title: ロード テスト用のカスタム コードおよびカスタム プラグインの作成
description: ロード テスト API および Web パフォーマンス テスト API を使用してテスト用のカスタム プラグインを作成し、組み込みの機能に拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
f1_keywords:
- vs.test.dialog.recorderplugin
helpviewer_keywords:
- Web performance tests, plug-ins
- load tests, plug-ins
ms.assetid: 0c0fcc99-673b-4ea0-a268-0475f66e5cb6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: db91f8f5ccf86d67d01bb56a3a42b66757320500
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95442665"
---
# <a name="create-custom-code-and-plug-ins-for-load-tests"></a>ロード テスト用のカスタム コードおよびカスタム プラグインの作成

カスタム プラグインでは、ユーザーが作成してロード テストや Web パフォーマンス テストにアタッチしたコードが使用されます。 ロード テスト API または Web パフォーマンス テスト API を使用してテスト用のカスタム プラグインを作成し、組み込みの機能に拡張できます。 ロード テストには複数のプラグインを追加することができます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="tasks"></a>タスク

|タスク|関連するトピック|
|-|-----------------------|
|**ロード テスト用のカスタム プラグインを作成する**: ロード テスト API を使用してカスタム プラグインを作成し、ロード テストのテスト機能を拡張できます。|-   [方法: ロード テスト API を使用する](../test/how-to-use-the-load-test-api.md)<br />-   [方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)|
|**Web パフォーマンス テスト用のカスタム プラグインを作成する:** Web パフォーマンス テスト API を使用してカスタム プラグインを作成し、Web パフォーマンス テスト (要求レベルのテストを含む) のテスト機能を拡張できます。 Web サービス テストを作成することもできます。<br /><br /> さらに、Web パフォーマンス テストの記録後、Web パフォーマンス テスト結果ビューアーに表示する前にこのパフォーマンス テストを変更できる Web レコーダー プラグインを作成できます。|-   [方法: Web パフォーマンス テスト API を使用する](../test/how-to-use-the-web-performance-test-api.md)<br />-   [方法: Web パフォーマンス テスト プラグインを作成する](../test/how-to-create-a-web-performance-test-plug-in.md)<br />-   [方法: 要求レベルのプラグインを作成する](../test/how-to-create-a-request-level-plug-in.md)<br />-   [方法: Web サービス テストを作成する](../test/how-to-create-a-web-service-test.md)<br />-   [方法: レコーダー プラグインを作成する](../test/how-to-create-a-recorder-plug-in.md)|
|**UI 機能を Web パフォーマンス テスト結果ビューアーに追加する:** Visual Studio アドインを使用すると、Web パフォーマンス テスト結果ビューアーにさらに UI 機能を追加できます。|-   [方法: Web パフォーマンス テスト結果ビューアー用に Visual Studio アドインを作成する](../test/how-to-create-an-add-in-for-the-web-performance-test-results-viewer.md)|
|**カスタム HTTP ボディ エディターを作成する:** Web サービスからのバイナリまたは文字列 http XML 形式の応答を編集するためのカスタム エディターを作成できます。|-   [方法: Web パフォーマンス テスト エディターのカスタム HTTP ボディ エディターを作成する](../test/how-to-create-a-custom-http-body-editor-for-the-web-performance-test-editor.md)|

## <a name="reference"></a>関連項目

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin>

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin>

<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin>

<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRecorderPlugin>

<xref:Microsoft.VisualStudio.TestTools.LoadTesting>

## <a name="see-also"></a>関連項目

- [ロード テストの結果の分析](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [コード化された Web パフォーマンス テストの生成と実行](../test/generate-and-run-a-coded-web-performance-test.md)
