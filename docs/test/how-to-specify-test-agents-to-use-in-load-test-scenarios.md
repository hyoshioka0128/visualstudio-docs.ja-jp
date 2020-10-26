---
title: ロード テスト シナリオで使用するテスト エージェントを指定する
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- test agents, load tests
- load tests, scenarios
- load tests, specifying for load tests
- tests agents, load tests, specifying
- load tests, test agents
ms.assetid: e86806dd-5897-4e4c-bfd4-8d687fb72a6e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5d9e22200a63544b4539f7bf78c48d5711974776
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85287494"
---
# <a name="how-to-specify-test-agents-to-use-in-load-test-scenarios"></a>方法: ロード テスト シナリオで使用するテスト エージェントを指定する

**新しいロード テスト ウィザード**でロード テストを作成した後、**ロード テスト エディター**を使用して、テストのニーズや目標に合わせてシナリオのプロパティを変更できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

> [!NOTE]
> ロード テスト シナリオの各プロパティとその説明の一覧については、「[ロード テスト シナリオのプロパティ](../test/load-test-scenario-properties.md)」を参照してください。

エージェントは、**ロード テスト エディター**の **[プロパティ]** ウィンドウで **[使用するエージェント]** プロパティを変更することによって指定されます。

コントローラーおよびエージェントを使用してリモートでロード テストを実行する場合は、シナリオに使用するエージェントを指定できます。 たとえば、特定のエージェントのセットを指定することで、パフォーマンスの傾向を分析する際の一貫性を維持することができます。 エージェントを地理的に分散して、実行するスクリプトとエージェントの場所の間に親和性を持たせることもできます。

> [!TIP]
> エージェントをリモート サイトに物理的に配置するのではなく、ネットワーク エミュレーションを使用して低速なネットワークをエミュレートする方法もあります。 詳細については、[仮想ネットワークの種類の指定](../test/specify-virtual-network-types-in-a-load-test-scenario.md)に関するページを参照してください。

詳細については、[テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)に関するページを参照してください。

もう 1 つの理由は、特定のシナリオに必要なソフトウェアが、(すべてではなく) 一部のエージェントにインストールされている場合があるということです。

テストの設定でロールを使用すると、特定のリストの実行に対するエージェントの選択を制御できます。 詳細については、「[テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)」を参照してください。

テスト エージェント コンピューターによる CPU 使用率が 75% を超える場合、または使用可能な物理メモリが 10% を下回る場合は、ロード テストにエージェントを追加して、エージェント コンピューターがロード テストのボトルネックにならないようにしてください。

## <a name="to-specify-the-agents-to-use-for-a-scenario"></a>シナリオに使用するエージェントを指定するには

1. ロード テストを開きます。

     **ロード テスト エディター**が表示されます。 ロード テスト ツリーが表示されます。

2. ロード テスト ツリーの **[シナリオ]** フォルダーで、使用するエージェントを指定するシナリオのノードを選択します。

3. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

     **[プロパティ]** ウィンドウに、シナリオのカテゴリおよびプロパティが表示されます。

4. **[使用するエージェント]** プロパティのテキスト ボックスに、シナリオを実行するエージェントの一覧を入力します。

     エージェントは、"**Agent1, Agent2, Agent3**" のように、コンマで区切る必要があります。 プロパティが空白の場合、シナリオでは、使用できるすべてのエージェントが使用されます。

    > [!NOTE]
    > ローカルの実行では、 **[使用するエージェント]** プロパティは無視されます。 リモート実行では、 **[使用するエージェント]** で指定されているエージェントが存在しない場合、シナリオのテストは実行されません。

5. プロパティを変更した後で、 **[ファイル]** メニューの **[保存]** を指定します。 その後で、新しい **[使用するエージェント]** の値を使用して、ロード テストを実行できます。

## <a name="see-also"></a>参照

- [ロード テスト シナリオの編集](../test/edit-load-test-scenarios.md)
- [チュートリアル: ロード テストの作成と実行](../test/walkthrough-create-and-run-a-load-test.md)
- [テスト コントローラーとテスト エージェント](configure-test-agents-and-controllers-for-load-tests.md)
- [ロード テスト シナリオのプロパティ](../test/load-test-scenario-properties.md)
