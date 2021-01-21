---
title: ロード テスト API
description: ロード テスト API の使用方法について説明します。ロード テスト プラグインがサポートされていて、ロード テストの制御や拡張を行うことができます。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- code, load tests
- plug-ins, load test
- APIs, load tests
ms.assetid: e15567bc-1f21-4feb-b81d-f17ba35cfde5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fd2064a76777390eb4b708b402578f1d89ca52c7
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328679"
---
# <a name="how-to-use-the-load-test-api"></a>方法: ロード テスト API を使用する

Visual Studio では、ロード テストの制御や拡張を行うことができるロード テスト プラグインがサポートされています。 ロード テスト プラグインは、<xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> 名前空間にある <xref:Microsoft.VisualStudio.TestTools.LoadTesting> インターフェイスを実装するユーザー定義のクラスです。 ロード テスト プラグインを使用すると、カウンターやエラーしきい値に達した場合にロード テストを中止するなど、ロード テストのカスタム制御を行うことができます。 ユーザー定義のコードに対してロード テスト パラメーターの取得や設定を行うには、<xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest> クラスのプロパティを使用します。 ロード テストを実行するときに、通知用のデリゲートを割り当てるには、<xref:Microsoft.VisualStudio.TestTools.LoadTesting.LoadTest> クラスのイベントを使用します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!TIP]
> オブジェクト ブラウザーを使用して、<xref:Microsoft.VisualStudio.TestTools.LoadTesting> 名前空間を調べます。 Visual C# エディターおよび Visual Basic エディターの両方では、この名前空間のクラスを使用したコーディングの IntelliSense サポートを提供しています。

Web パフォーマンス テスト用のプラグインを作成することもできます。 詳細については、「[方法:Web パフォーマンス テスト プラグインを作成する](../test/how-to-create-a-web-performance-test-plug-in.md)」と「[方法:要求レベルのプラグインを作成する](../test/how-to-create-a-request-level-plug-in.md)」を参照してください。

## <a name="to-use-the-loadtesting-namespace"></a>LoadTesting 名前空間を使用するには

1. ロード テストが含まれている、Web パフォーマンスとロード テストのプロジェクトを開きます。

2. Visual C# または Visual Basic のクラス ライブラリ プロジェクトをテスト ソリューションに追加します。

3. Web パフォーマンスとロード テストのプロジェクトの参照をクラス ライブラリ プロジェクトに追加します。

4. クラス ライブラリ プロジェクトの Microsoft.VisualStudio.QualityTools.LoadTestFramework DLL への参照を追加します。

5. クラス ライブラリ プロジェクトのクラス ファイルで、`using` 名前空間の <xref:Microsoft.VisualStudio.TestTools.LoadTesting> ステートメントを追加します。

6. <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> インターフェイスを実装するパブリック クラスを作成します。

7. プロジェクトをビルドします。

8. ロード テスト エディターを使用して新しいロード テスト プラグインを追加します。

    1. ロード テストのルート ノードを右クリックし、**[ロード テスト プラグインの追加]** を選択します。

    2. **[ロード テスト プラグインの追加]** ダイアログ ボックスが表示されます。

    3. **[選択したプラグインのプロパティ]** ペインで、実行時に使用するプラグインの初期値を設定します。

        > [!NOTE]
        > プラグインのプロパティは、必要な数だけ公開できます。それをパブリック、設定可能、および基本型 (整数型、ブール型、文字列型など) として設定します。 ロード テスト プラグインのプロパティは、後で **[プロパティ]** ウィンドウを使用して編集することもできます。

9. ロード テストを実行します。

     <xref:Microsoft.VisualStudio.TestTools.LoadTesting.ILoadTestPlugin> の実装については、「[方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.LoadTesting>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [方法: Web パフォーマンス テスト API を使用する](../test/how-to-use-the-web-performance-test-api.md)
- [方法: ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)
