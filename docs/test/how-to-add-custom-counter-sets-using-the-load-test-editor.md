---
title: ロード テスト用にカスタム カウンター セットを追加する
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- counters, counter sets
- counter sets
- load tests, counter sets
ms.assetid: 499aca80-1069-408d-ac68-326da6a50645
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e2b78cb68f1e7a7e1f47c6cc3e771353d7e46ca9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85288430"
---
# <a name="how-to-add-custom-counter-sets-using-the-load-test-editor"></a>方法: ロード テスト エディターを使用してカスタム カウンター セットを追加する

**新しいロード テスト ウィザード**でロード テストを作成するときに、初期カウンター セットを追加します。 これらによって、定義済みのカウンター セットがロード テスト用に提供されます。

> [!NOTE]
> ロード テストを複数のリモート コンピューターに分散する場合、コントローラーとエージェント カウンターが、コントローラーとエージェント カウンター セットに割り当てられます。 ロード テストでのリモート コンピューターの使用方法の詳細については、[テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)に関するページを参照してください。

カウンターは、**ロード テスト エディター**で管理します。 テストに既に追加されているカウンター セットは、ロード テストの **[カウンター セット]** ノードに表示されます。 ロード テストを作成すると、そこに新しいカスタム カウンター セットを追加できます。

![カスタムのカウンター セット](../test/media/loadtestcustomcounter.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-a-custom-counter-set-to-a-load-test"></a>カスタム カウンター セットをロード テストに追加するには

1. ロード テストを開きます。

2. **[カウンター セット]** ノードを展開します。 ロード テストに追加されているすべてのカウンター セットが表示されます。

3. **[カウンター セット]** ノードを右クリックし、 **[カスタム カウンター セットの追加]** を選択します。

    > [!NOTE]
    > カウンター セットには、**Custom1** のような既定の名前が付けられます。 名前は **[プロパティ]** ウィンドウを使用して変更できます。 **F4** キーを押して **[プロパティ]** ウィンドウを表示します。

4. カウンターをカスタム カウンター セットに追加するには、新しいカウンター セットを右クリックし、 **[カウンターの追加]** を選択します。 カウンターを追加する方法の詳細については、「[方法: カウンターをカウンター セットに追加する](../test/how-to-add-counters-to-counter-sets-using-the-load-test-editor.md)」を参照してください。

    > [!NOTE]
    > カスタム カウンター セットも追加できます。追加するには、既存のカウンター セットを右クリックし、[コピー] を選択して、カウンター セット ノードに貼り付けます。 コピーされた追加のカウンターで不要になったものは削除できます。 新しいカウンター セットの名前は、 **[プロパティ]** ウィンドウを使用して変更できます。

## <a name="see-also"></a>参照

- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
