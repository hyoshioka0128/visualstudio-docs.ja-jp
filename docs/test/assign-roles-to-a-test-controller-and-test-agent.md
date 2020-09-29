---
title: テスト コントローラー ロールとテスト エージェント ロール
ms.custom: SEO-VS-2020
ms.date: 10/20/2016
ms.topic: conceptual
helpviewer_keywords:
- testing, walkthroughs, test controller and test agents
- test agent, walkthrough
- walkthroughs [Visual Studio ALM] testing
- test controller, walkthrough
- walkthroughs, test controller and test agents
ms.assetid: 57ed43ae-4e67-4139-8aec-3e9fceb0a745
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c7f4360772f3962ff60517071dcae4318dc71e56
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809303"
---
# <a name="assign-roles-to-a-test-controller-and-test-agent"></a>ロールをテスト コントローラーとテスト エージェントに割り当てる

この記事では、Visual Studio で、テスト コントローラーとテスト エージェントを使用して、複数のコンピューターにテストを分散するテスト設定を作成および構成する方法について説明します。 また、診断およびデータ アダプターをテスト設定に追加する方法についても説明します。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="prerequisites"></a>前提条件

- テスト設定で実行する単体テストまたはコード化された UI テストを作成する必要があります。

- テスト コントローラーとテスト エージェントをインストールします。 テスト コントローラーとテスト エージェントをインストールする方法の詳細については、[テスト エージェントのインストールと構成](../test/lab-management/install-configure-test-agents.md)に関するページを参照してください。

## <a name="to-create-and-configure-a-test-setting"></a>テスト設定を作成および構成するには

1. **ソリューション エクスプローラー**で、 **[ソリューション項目]** を右クリックし、 **[追加]** をポイントして、 **[新しい項目]** を選択します。

     **[新しい項目の追加]** ダイアログ ボックスが表示されます。

2. **[インストールされたテンプレート]** ペインで、 **[テストの設定]** を選択します。

3. **[名前]** ボックスに、「**TestSettingDistributedTestWalkthrough**」と入力します。

4. **[追加]** をクリックします。

     **ソリューション エクスプローラー**の **[ソリューション項目]** フォルダーに、*TestSettingDistributedTestWalkthrough.testsettings* という新しいテスト ファイルが表示されます。

     **[テストの設定]** ダイアログ ボックスが表示されます。 **[全般]** ページが選択されています。

     このページで、テストの設定値を編集および保存できます。

5. **[名前]** ボックスに、テストの設定の名前を入力します。

6. **[説明]** に、「**分散テスト設定**」と入力します。

7. **[既定の名前付けスキーム]** が選択された状態のままにします。

## <a name="to-assign-roles-to-a-test-controller-and-test-agents"></a>ロールをテスト コントローラーとテスト エージェントに割り当てるには

1. **[ロール]** を選択します。

     **[ロール]** ページが表示されます。

2. テストをリモートで実行するには、 **[テストの実行メソッド]** ドロップダウン リストの **[リモート実行]** をクリックします。

3. **[コントローラー]** ドロップダウン リストに、[テスト コントローラー](../test/lab-management/install-configure-test-agents.md)のコンピューター名を入力します。

    > [!NOTE]
    > 初めてコントローラーを追加する場合、このドロップダウン リストにコントローラーは表示されません。 このリストは、他のテスト設定でそれまでに指定したコントローラーによって設定されます。

4. **[ロール]** の **[追加]** をクリックします。

5. **[名前]** 列の強調表示された行に、「**分散テスト**」と入力します。

## <a name="to-assign-a-diagnostic-and-data-adapter-to-your-test-setting"></a>診断およびデータ アダプターをテスト設定に割り当てるには

1. **[データと診断]** を選択します。

     **[データと診断]** ページが表示されます。

2. **[ロール]** で、**分散テスト** ロールが選択されていることを確認します。

3. **[選択されたロールのデータと診断]** の **[IntelliTrace]** アダプターと **[システム情報]** アダプターを選択します。

     これらのアダプター、およびテストの設定で使用できるその他のアダプターの詳細については、[単体テストの構成](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)に関するページを参照してください。

4. **[ホスト]** を選択します。

5. (省略可能) コンピューターで 64 ビット バージョンの Microsoft Windows を実行しており、**Any CPU** 構成を使用してテストをコンパイルした場合は、 **[32 ビット プロセスまたは 64 ビット プロセスでテストを実行]** ドロップダウン リストの **[64 ビット コンピューター上で 64 ビット プロセスでテストを実行]** をクリックします。

    > [!TIP]
    > 柔軟性を最大限に高めるには、テスト プロジェクトを**任意の CPU** 構成でコンパイルします。 これにより、32 ビット エージェントと 64 ビット エージェントの両方で実行できます。 **64 ビット**構成でテスト プロジェクトをコンパイルしても、特に利点はありません。

6. 新しいテストの設定を保存するには、 **[適用]** をクリックします。

7. **[閉じる]** を選択します。

::: moniker range="vs-2017"

8. **[テスト]** メニューで、 **[テストの設定]** > **[テスト設定ファイルの選択]** を選択し、*TestSettingDistributedTestWalkthrough.testsettings* ファイルを選択します。

::: moniker-end

::: moniker range=">=vs-2019"

8. **[テスト]** メニューで **[設定ファイルの選択]** を選択します。 *TestSettingDistributedTestWalkthrough.testsettings* ファイルを参照し、選択します。

::: moniker-end

9. 通常どおり、テストを実行します。

     テスト コントローラーは、単体テストおよびコード化された UI テストを処理するとき、テストを 100 個単位のグループに分割し、テスト エージェント コンピューターに送信します。 たとえば、250 個の単体テストと 3 つのテスト エージェントがある場合、最初の 100 個の単体テストは agent1 に送信され、次の 100 個の単体テストは agent2 に送信され、残りの 50 個の単体テストは agent3 に送信されます。

## <a name="see-also"></a>参照

- [テスト エージェントをインストールして構成する](../test/lab-management/install-configure-test-agents.md)
