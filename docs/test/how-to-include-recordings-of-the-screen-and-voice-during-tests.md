---
title: テスト中の画面と音声を記録する
ms.date: 10/03/2016
ms.topic: how-to
helpviewer_keywords:
- test settings, recording desktop video
ms.assetid: 2cefe8c2-430a-4cb4-bbe0-f3edb2e5bc03
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4fb186c97126d843cc47c16fa16a836914ed2e9b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85287767"
---
# <a name="how-to-include-recordings-of-the-screen-and-voice-during-tests-using-test-settings"></a>方法: テスト設定を使用してテスト中に画面と音声の記録を含める

Visual Studio の構成エディターから、テストを実行しているユーザーの画面と音声を記録する診断データ アダプターを構成できます。 この診断データ アダプターは、テスト中にデスクトップ セッションの画面と音声の記録を保存します。 この記録は、テスト結果と共に保存するか、またはバグに添付できます。 他のチーム メンバーがこの記録を使用して、再現するのが困難なアプリケーションの欠陥を特定できます。

> [!WARNING]
> 画面と音声の記録では、複数のモニター構成はサポートされていません。

画面と音声のレコーダーは、手動テストまたは自動テストで使用できます。 たとえば、コード化された UI テストをリモートで実行する場合、コード化された UI テストを実行するときにそのテストを確認するためにデスクトップを記録できます。 画面と音声の記録をリモートでキャプチャする方法の詳細については、「[方法:テスト エージェントを設定して、デスクトップと対話するテストを実行する](../test/how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop.md)」を参照してください。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-configure-screen-and-voice-recording-for-your-test-settings"></a>テストの設定に対して画面と音声の記録を構成するには

1. 画面と音声を記録するために構成するテストの設定を開きます。 詳細については、「[Collect diagnostic data while testing (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)」(テスト中の診断データの収集 (Azure Test Plans)) または「[テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)」を参照してください。

2. テストの設定で、画面と音声の記録に使用する **[ロール]** をクリックします。

    > [!NOTE]
    > 手動テストおよび自動テストの場合、ロールはテストを実行するコンピューターとなります。

3. **[画面と音声のレコーダー]** をクリックし、 **[構成]** をクリックします。

     **[診断データ アダプターの構成 - 画面と音声のレコーダー]** ダイアログ ボックスが表示されます。

     ![ビデオの構成](../test/media/testsettingvideoconfiggdr.png)

4. (省略可能) **[音声記録を有効にする]** をクリックして、オーディオ コンテンツをキャプチャして記録します。

5. (省略可能) **[テスト ケースに成功した場合に記録を保存する]** の横のチェック ボックスをオンにして、テストに失敗した場合も成功した場合も画面と音声の記録が保存されるように指定します。

    > [!WARNING]
    > **[テスト ケースに成功した場合に記録を保存する]** をクリックすると、この記録はテスト結果と共に、サーバーのストレージ領域を使用して保存されます。 これらの添付ファイルをクリーンアップするには、**Test Attachment Cleaner** ツールを使用できます。

6. **[画面記録の品質]** で、以下のボックス オプションを構成します。

    1. **[フレーム レート]:** 画面と音声の記録で使用する 1 秒あたりのフレーム数を指定します。 既定値は 1 秒あたり 4 フレームです。 指定できる値は 2 ～ 20 です。

    2. **[ビット レート]:** 画面と音声の記録で使用する 1 秒あたりのキロバイト数を指定します。 既定値は 512 です。 指定できる値は 512 ～ 10,000 です。

    3. **[品質 (1-100)]:** 画面と音声の記録の品質を 1 から 100 の範囲の値を選択して指定します。 既定値は 50 (中間) です。

7. **[OK]** をクリックします。 これで、テストの設定を対象として診断トレース コレクターの設定が構成および保存されました。

    ::: moniker range="vs-2017"
    > [!TIP]
    > この診断データ アダプターの構成をリセットするには、Visual Studio の場合は **[既定の構成にリセット]** をクリックし、Microsoft Test Manager の場合は **[既定値にリセット]** をクリックします。
    ::: moniker-end
    ::: moniker range=">=vs-2019"
    > [!TIP]
    > この診断データ アダプターの構成をリセットするには、Visual Studio で **[既定の構成にリセット]** をクリックします。
    ::: moniker-end

## <a name="see-also"></a>関連項目

- [テスト中の診断データの収集 (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [手動テストでの診断データの収集 (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [テスト設定を使用して診断情報を収集する](../test/collect-diagnostic-information-using-test-settings.md)
- [手動テストの実行 (Azure Test Plans)](/azure/devops/test/run-manual-tests?view=vsts)
