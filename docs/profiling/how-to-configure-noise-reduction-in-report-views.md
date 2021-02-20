---
title: レポート ビューでノイズ除去を設定する | Microsoft Docs
description: いずれも既定で有効になっているトリミングおよび折りたたみを使用し、ノイズを除去し、ご自分のレポートでパフォーマンスの問題がより目立つようにできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.noisereduction.dialog
helpviewer_keywords:
- profiling tools, trimming
- profiling tools, report noise reduction
- profiling tools, folding
ms.assetid: b07e0375-bb73-47e3-8d1d-b9b492fb16c9
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5037cf0184608829d5a86d736bead5b61f5172c5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969335"
---
# <a name="how-to-configure-noise-reduction-in-report-views"></a>方法: レポート ビューでノイズ除去を設定する
パフォーマンス レポートは、コール ツリー ビューや 割り当て ビューに表示されるデータの数を制限して、ノイズを除去するように構成できます。 ノイズ除去を行うことで、パフォーマンスの問題を発見しやすくなります。 これは、パフォーマンス レポートの分析に役立ちます。

 ノイズ除去の構成オプションには、次の設定が含まれます。

- **トリミング** 後述のトリミング手順で説明するように、レポートを分析するとき、構成した値やしきい値の設定の範囲内に収まる関数を省略します。 既定で、トリミング機能は有効になっています。

- **折りたたみ** 後述の折りたたみの手順で説明するように、折りたたみを有効にすると、構成した設定要件を満たすパスにおける連続的な関数がマージされます。 既定で、折りたたみは有効になっています。

### <a name="to-configure-trimming-for-a-performance-report"></a>パフォーマンス レポートのトリミングを構成するには

1. 生成されたレポートの コール ツリー ビューまたは 割り当て ビューを表示している状態で、 **[開発者]** メニューの **[プロファイラー]** をクリックし、 **[不要項目の非表示オプション]** をクリックします。

     **[不要項目の非表示]** ダイアログ ボックスが表示されます。

2. トリミングを有効にするには、次の手順を実行します。

    1. **[トリミングを有効にする]** を選択します。 これは、既定の設定です。

        > [!NOTE]
        > ノイズ除去が有効になっていると、レポートに情報バーが表示されます。 詳細については、「[コール ツリー ビュー](../profiling/call-tree-view.md)」および「[割り当てビュー](../profiling/dotnet-memory-allocations-view.md)」を参照してください。

    2. **[値]** ドロップダウン リストを使用し、適切な設定を選択して、値の設定を構成します。

    3. **[しきい値]** テキスト ボックスに割合の値を入力して、必要なしきい値の設定を構成します。

    4. 生成されたレポートでノイズ除去の警告を有効にするには、 **[不要項目の非表示が有効な場合に警告を表示する]** を選択します。 これは、既定の設定です。

3. トリミングを無効にするには、 **[トリミングを有効にする]** をオフにします。

4. **[OK]** をクリックします。

### <a name="to-configure-folding-for-a-performance-report"></a>パフォーマンス レポートの折りたたみを構成するには

1. **[開発者]** メニューで **[プロファイラー]** をクリックしてから、 **[不要項目の非表示オプション]** をクリックします。

     **[不要項目の非表示]** ダイアログ ボックスが表示されます。

2. 折りたたみを有効にするには、次の手順を実行します。

    1. **[折りたたみを有効にする]** を選択します。 これは、既定の設定です。

        > [!NOTE]
        > ノイズ除去が有効になっていると、レポートに情報バーが表示されます。 詳細については、「[コール ツリー ビュー](../profiling/call-tree-view.md)」および「[割り当てビュー](../profiling/dotnet-memory-allocations-view.md)」を参照してください。

    2. **[値]** ドロップダウン リストを使用し、適切な設定を選択して、値の設定を構成します。

    3. **[しきい値]** テキスト ボックスに割合の値を入力して、必要なしきい値の設定を構成します。

    4. 生成されたレポートでノイズ除去の警告を有効にするには、 **[不要項目の非表示が有効な場合に警告を表示する]** を選択します。 これは、既定の設定です。

3. 折りたたみを無効にするには、 **[折りたたみを有効にする]** をオフにします。

4. **[OK]** をクリックします。

## <a name="see-also"></a>関連項目
- [パフォーマンス ツールのレポート ビューのカスタマイズ](../profiling/customizing-performance-tools-report-views.md)
- [方法: インストルメンテーションで短い関数を除外または含める](../profiling/how-to-exclude-or-include-short-functions-from-instrumentation.md)
- [コール ツリー ビュー](../profiling/call-tree-view.md)
- [割り当て ビュー](../profiling/dotnet-memory-allocations-view.md)
