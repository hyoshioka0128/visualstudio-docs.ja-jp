---
title: ロード テストへの実行設定の追加
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- load tests, run settings, adding
- load tests, run settings
ms.assetid: 257d2a24-d582-4cfe-8b2b-51f51ba9cc84
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a2f62b3e9797e411138590fc15b0fe872920d203
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85288456"
---
# <a name="how-to-add-additional-run-settings-to-a-load-test"></a>方法: ロード テストに追加の実行設定を追加する

ロード テストの実行設定で、その他のさまざまな設定を行います。 こうした設定には、テストの継続時間、結果収集の詳細レベル、テストの実行時に収集されるカウンター セットなどがあります。 それぞれのロード テストに対して複数の実行設定を作成して保存しておき、テストの実行時には使用する特定の設定を選択できます。 **新しいロード テスト ウィザード**を使用してロード テストを作成するときに、初期の実行設定をロード テストに追加します。

さまざまな条件でロード テストを実行できるように、別のプロパティ設定のロード テストにそれ以外の実行設定を追加できます。 たとえば、新しいテストの設定を追加して、異なるサンプリング レートを使用したり、より長い実行時間を指定することができます。 一度に使用できる実行設定は 1 つのみです。使用する実行設定を指定するには、その設定をアクティブにする必要があります。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-add-another-run-setting"></a>実行設定を追加するには

1. ロード テストを開きます。

2. (省略可能) **[実行設定]** フォルダーを展開します。

3. **[実行設定]** フォルダーを右クリックして、 **[実行設定の追加]** をクリックします。

     **[実行設定]** フォルダーに新しい実行設定が追加されます。

4. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

     **[プロパティ]** ウィンドウが開き、選択した実行設定のプロパティが表示されます。

5. **[プロパティ]** ウィンドウで、 **[名前]** プロパティのテキスト ボックスに新しい実行設定の名前を入力します。名前は実行設定の内容を説明するものにします (たとえば、「**実行設定: 実行時間 5 分**」など)。

6. **[プロパティ ]** ウィンドウを使用して、実行設定を変更します。 たとえば、テストを 5 分間実行するには、実行の継続時間を **00:05:00** に変更します。

    > [!NOTE]
    > 実行設定の各プロパティとその説明の一覧については、「[ロード テストの実行設定のプロパテ](../test/load-test-run-settings-properties.md)」を参照してください。

     追加した実行設定をアクティブに設定すると、これを使用することができます。 詳細については、「[方法: ロード テストのアクティブな実行設定を選択する](../test/how-to-select-the-active-run-setting-for-a-load-test.md)」を参照してください。

## <a name="see-also"></a>参照

- [ロード テストの実行設定の構成](../test/configure-load-test-run-settings.md)
- [ロード テストでのコンピューターのカウンター セットとしきい値規則の指定](../test/specify-counter-sets-and-threshold-rules-for-load-testing.md)
