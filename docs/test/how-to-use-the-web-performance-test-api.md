---
title: Web パフォーマンス テスト API
description: コード化された Web パフォーマンス テスト、テスト プラグイン、要求プラグイン、要求、抽出と検証の規則をサポートする Web パフォーマンス テスト API について説明します。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- Web performance tests, using the API
- APIs, Web performance tests
ms.assetid: 93a6a1dd-663b-4ab5-8760-7d6b081561d3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.openlocfilehash: f2afc1ab325fab8da6bdaba5650ae06d9cfcce14
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969231"
---
# <a name="how-to-use-the-web-performance-test-api"></a>方法: Web パフォーマンス テスト API を使用する

Web パフォーマンス テストのコードを記述できます。 Web パフォーマンス テスト API は、コード化された Web パフォーマンス テスト、Web パフォーマンス テスト プラグイン、要求プラグイン、要求、抽出規則、検証規則を作成するために使用します。 これらの種類を構成するクラスは、この API のコア クラスです。 この API の他の種類は、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTest> オブジェクト、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> オブジェクト、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequestPlugin> オブジェクト、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestRequest> オブジェクト、<xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule> オブジェクト、および <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule> オブジェクトの作成をサポートするために使用されます。 カスタマイズされた Web パフォーマンス テストを作成するには、<xref:Microsoft.VisualStudio.TestTools.WebTesting> 名前空間を使用します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

また、Web パフォーマンス テスト API を使用して、プログラムにより宣言 Web パフォーマンス テストを作成および保存することもできます。 それを行うには、<xref:Microsoft.VisualStudio.TestTools.WebTesting.DeclarativeWebTest> クラスと <xref:Microsoft.VisualStudio.TestTools.WebTesting.DeclarativeWebTestSerializer> クラスを使用します。

> [!TIP]
> オブジェクト ブラウザーを使用して、<xref:Microsoft.VisualStudio.TestTools.WebTesting> 名前空間を調べます。 Visual C# エディターおよび Visual Basic エディターの両方では、この名前空間のクラスを使用したコーディングの IntelliSense サポートを提供しています。

ロード テスト用のプラグインを作成することもできます。 詳細については、「[方法:ロード テスト API を使用する](../test/how-to-use-the-load-test-api.md)と[方法:ロード テスト プラグインを作成する](../test/how-to-create-a-load-test-plug-in.md)。

## <a name="to-use-the-webtesting-namespace"></a>WebTesting 名前空間を使用するには

1. Web パフォーマンス テストが含まれている、Web パフォーマンスとロード テストのプロジェクトを開きます。

2. Visual C# または Visual Basic のクラス ライブラリ プロジェクトをテスト ソリューションに追加します。

3. Web パフォーマンスとロード テストのプロジェクトの参照をクラス ライブラリ プロジェクトに追加します。

4. Microsoft.VisualStudio.QualityTools.WebTestFramework DLL への参照をクラス ライブラリ プロジェクトに追加します。

5. クラス ライブラリ プロジェクトのクラス ファイルで、`using` 名前空間の <xref:Microsoft.VisualStudio.TestTools.WebTesting> ステートメントを追加します。

6. <xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> インターフェイスを実装するクラスを作成します。

7. プロジェクトをビルドします。

8. Web パフォーマンス テスト エディターを使用して、新しい Web パフォーマンス テスト プラグインを追加します。

    1. ツール バーの **[Web テスト プラグインの追加]** を選択します。

         **[Web テスト プラグインの追加]** ダイアログ ボックスが表示されます。

    2. **[プラグインの選択]** で、Web パフォーマンス テスト プラグイン クラスを選択します。

    3. **[選択したプラグインのプロパティ]** ペインで、実行時に使用するプラグインの初期値を設定します。

        > [!NOTE]
        > プラグインのプロパティをパブリック、設定可能、および基本型 (整数型、ブール型、文字列型など) として設定して、任意の数だけ公開できます。 Web パフォーマンス テスト プラグインのプロパティは、後で [プロパティ] ウィンドウを使用して編集することもできます。

    4. **[OK]** をクリックします。

9. Web パフォーマンス テストを実行します。

     たとえば、<xref:Microsoft.VisualStudio.TestTools.WebTesting.WebTestPlugin> の実装については、「[方法:Web パフォーマンス テスト プラグインを作成する](../test/how-to-create-a-web-performance-test-plug-in.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.TestTools.WebTesting>
- [ロード テスト用のカスタム コードおよびカスタム プラグインの作成](../test/create-custom-code-and-plug-ins-for-load-tests.md)
- [方法: ロード テスト API を使用する](../test/how-to-use-the-load-test-api.md)
- [方法: Web パフォーマンス テスト プラグインを作成する](../test/how-to-create-a-web-performance-test-plug-in.md)
