---
title: ロード テストのカウンター セット
ms.date: 10/19/2016
ms.topic: how-to
f1_keywords:
- vs.test.load.dialog.countersetmapping
helpviewer_keywords:
- counters, counter sets
- performance counters
- counter sets
- load tests, counter sets
ms.assetid: 64315c2f-a0b2-4378-be16-0774b99beef5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1eeb99d58a9fc0547d118c529878d8b02cc83dda
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85287689"
---
# <a name="how-to-manage-counter-sets-using-the-load-test-editor"></a>方法: ロード テスト エディターを使用してカウンター セットを管理する

**新しいロード テスト ウィザード**でロード テストを作成するときに、初期カウンター セットを追加します。 これらによって、定義済みのカウンター セットがロード テスト用に提供されます。

> [!NOTE]
> ロード テストを複数のリモート コンピューターに分散する場合、コントローラーとエージェント カウンターが、コントローラーとエージェント カウンター セットに割り当てられます。 ロード テストでリモート コンピューターを使用する方法の詳細については、[テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)に関するページを参照してください。

カウンター セットの管理では、パフォーマンス データの収集元となるコンピューター セットの選択や、個々のコンピューターから収集するカウンター セットの割り当てなどを行います。 カウンターは、**ロード テスト エディター**で管理します。

![カウンター セットの管理](../test/media/loadtestmanagecountersets.png)

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-manage-counter-sets"></a>カウンター セットを管理するには

1. ロード テストを開きます。

2. **[カウンター セットの管理]** ボタンを選択します。

     または

     ロード テスト ツリーで **[カウンター セット]** フォルダーを右クリックし、 **[カウンター セットの管理]** を選択します。

     **[カウンター セットの管理]** ダイアログ ボックスが表示されます。

3. (省略可能) **[選択されたコンピューターおよびカウンター セットは、次の実行設定で追加されます]** リスト ボックスで、別の実行設定を選択します。

    > [!NOTE]
    > この手順は、ロード テストに複数の実行設定がある場合にのみ適用されます。

4. (省略可能) **[コンピューターの追加]** を選択して、監視する新しいコンピューターを追加します。 名前の入力を要求されます。 コンピューターの名前を入力すると、新しいエントリの下にノードが表示されます。 たとえば、**ASP.NET**、**IIS**、**SQL** などです。 選択するノードの横にあるチェック ボックスをオンにします。 新しいカウンターが **[選択のプレビュー]** ウィンドウに表示されます。

5. (省略可能) **[コンピューター タグ]** テキスト ボックスに、コンピューターに関連付けるタグを入力します。 たとえば、「ラボ 3 の TestMachine12」のように入力します。

     コンピューター タグを使用すると、わかりやすい名前でコンピューターを識別できます。

     このタグは、ロード テスト エディターのツリーの **[カウンター セットの割り当て]** ノードに表示されます。 また、このタグは Excel のレポートにも表示されるため、関係者がロード テストでコンピューターのロールを確認する際に役立ちます。 たとえば、"ラボ 2 の Web サーバー 1" や "Phoenix オフィスの SQL Server 2" のようなタグを使用できます。 詳細については、「[テストの比較または傾向分析に備えたロード テストの結果レポートの作成](../test/compare-load-test-results.md)」を参照してください。

6. **[OK]** をクリックします。

## <a name="see-also"></a>参照

- [テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)
- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
