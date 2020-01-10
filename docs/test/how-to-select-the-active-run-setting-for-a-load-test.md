---
title: ロード テストの実行設定を選択する
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, run settings, active
ms.assetid: ed6ff546-acfa-4dd8-b3a2-6e7455930ca4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 91ac811c1f55fdb9a662db679ebd2d038ecdd5dd
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588981"
---
# <a name="how-to-select-the-active-run-setting-for-a-load-test"></a>方法: ロード テストのアクティブな実行設定を選択する

**新しいロード テスト** ウィザードでロード テストを作成した後で、**ロード テスト エディター**を使用して、テストのニーズや目標に合わせてシナリオのプロパティを変更できます。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

ロード テストには、1 つ以上の*実行設定*を含めることができます。実行設定は、ロード テストの実行方法に影響を与えるプロパティのセットです。 実行設定は、 **[プロパティ]** ウィンドウでカテゴリ別に整理されています。 ロード テストの実行時には、現在アクティブとして設定されている実行設定が使用されます。

> [!NOTE]
> 実行設定の各プロパティとその説明の一覧については、「[ロード テストの実行設定のプロパティ](../test/load-test-run-settings-properties.md)」を参照してください。

ロード テストに含まれている実行設定ノードが、 **[実行設定]** フォルダー下に 1 つだけの場合は、そのノードが常にアクティブ ノードになります。 ロード テストに複数の実行設定ノードが含まれている場合は、ロード テストを実行する際に使用するノードを 1 つ選択します。 「[方法:ロード テストに追加の実行設定を追加する](../test/how-to-add-additional-run-settings-to-a-load-test.md)」を参照してください。

**ロード テスト エディター**で、アクティブな実行設定は "[Active]" というサフィックスで識別されます。

## <a name="select-the-active-run-setting"></a>アクティブな実行設定の選択

1. ロード テストを開きます。

2. **[実行設定]** フォルダーを展開します。

3. アクティブ ノードにする実行設定ノードを右クリックし、 **[アクティブとして設定]** を選択します。

     **ロード テスト エディター**で、対象となった実行設定ノードが "[Active]" というサフィックスで更新されます。

     選択した実行設定がアクティブになり、別の実行設定を選択してアクティブにするまでアクティブのままになります。

> [!NOTE]
> アクティブな実行設定は、`Test.UseRunSetting=<run setting name>` という名前の環境変数を設定することでオーバーライドできます。 これは、ロード テストをコマンド ラインまたはバッチ ファイルから実行する場合に便利です。 これを使用すると、ロード テストを開くことなく異なる実行設定を選択できます。

## <a name="specify-the-run-setting-to-use-from-the-command-line"></a>使用する実行設定のコマンド ラインからの指定

コマンド ラインから次の環境変数を設定することで、ロード テストの既定の実行設定をオーバーライドできます。

**Set Test.UseRunSetting=PreProdEnvironment**

そして、次のテストを実行します。

**mstest /testcontainer:loadtest1.loadtest**

## <a name="see-also"></a>関連項目

- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
- [方法: ロード テストに追加の実行設定を追加する](../test/how-to-add-additional-run-settings-to-a-load-test.md)
