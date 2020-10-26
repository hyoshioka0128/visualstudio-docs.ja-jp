---
title: コードメトリックスデータの操作 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
ms.assetid: 988193ec-b4a3-4e11-b5a1-7334979807d5
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c2460b4e8b9e0b9043178989fcf8825815471be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72645706"
---
# <a name="working-with-code-metrics-data"></a>コード メトリックス データの操作
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **コードメトリックスの結果** ] ウィンドウには、コードメトリックス分析によって生成されるデータが表示されます。 コードメトリックスのデータ値の詳細については、「 [コードメトリックスの値](../code-quality/code-metrics-values.md)」を参照してください。

 このトピックには、次のセクションが含まれます。

- [コードメトリックスの結果ウィンドウ](../code-quality/working-with-code-metrics-data.md#BKMK_CodeMetricsResultsWindow)

- [コードメトリックスの結果の表示](../code-quality/working-with-code-metrics-data.md#BKMK_DisplayingCodeMetricsResults)

- [コードメトリックスの結果のフィルター処理](../code-quality/working-with-code-metrics-data.md#BKMK_FilteringCodeMetricsResults)

- [データ列の追加、削除、および並べ替え](../code-quality/working-with-code-metrics-data.md#BKMK_AddingRemovingandRearrangingDataColumns)

- [クリップボードまたは Excel へのデータのコピー](../code-quality/working-with-code-metrics-data.md#BKMK_Copying_Data_to_the_Clipboard_or_Excel)

- [コードメトリックスの結果に基づいて作業項目を作成する](../code-quality/working-with-code-metrics-data.md#BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results)

## <a name="code-metrics-results-window"></a><a name="BKMK_CodeMetricsResultsWindow"></a> Code Metrics Results Window
 [ **コードメトリックスの結果** ] ウィンドウには、計算された結果を表示するためのツールバーが上部と列に表示されます。

|列|説明|
|------------|-----------------|
|**Hierarchy**|[ **階層** ] 列には、展開または折りたたむことができるコード階層のツリービューが含まれており、必要な詳細レベルを確認できます。 残りの列には、計算された結果が表示されます。 結果列は、必要に応じて表示または非表示にすることができます。|
|**保守容易性**|**保守性**列には、数値の結果に加えてアイコンが含まれています。 緑色のアイコンは、比較的高度な保守性を示しています。 黄色のアイコンは、保守性のレベルが中程度であることを示します。 赤いアイコンは、保守性が低く、問題が発生する可能性があることを示しています。 これらのカラーインジケーターは、FxCop ルール AvoidUnmaintainableCode によって使用される重大度カテゴリに対応します。 このルールでは、保守容易性インデックスが10未満の場合にエラーが発生します。インデックスが 10 ~ 20 の場合は警告が発生し、インデックスが20を超える場合は警告は発生しません。 保守容易性のインデックスは、サイクロマティックの複雑さ、コードの行、および計算の複雑さという3つのメトリックを合成したものです。 この値は、単位では表現されません。|

## <a name="displaying-code-metrics-results"></a><a name="BKMK_DisplayingCodeMetricsResults"></a> コードメトリックスの結果の表示
 コードメトリックスの結果を生成すると、[コードメトリックスの結果] ウィンドウが自動的に表示されます。 ウィンドウはいつでも表示できます。

#### <a name="to-display-the-code-metrics-results-window"></a>コードメトリックスの結果ウィンドウを表示するには

- [ **分析** ] メニューの [ **ウィンドウ** ] をクリックし、[ **コードメトリックスの結果**] をクリックします。

     \- または

- [ **表示** ] メニューの [ **その他のウィンドウ** ] をポイントし、[ **コードメトリックスの結果**] をクリックします。

     [コードメトリックスの結果] ウィンドウは、結果が含まれていない場合でも表示されます。

#### <a name="to-view-code-metrics-details"></a>コードメトリックスの詳細を表示するには

- コードメトリックスの結果が生成された場合は、[ **階層** ] 列のツリーを展開します。

## <a name="filtering-code-metrics-results"></a><a name="BKMK_FilteringCodeMetricsResults"></a> コードメトリックスの結果のフィルター処理
 上部にあるツールバーを使用して、[ **コードメトリックスの結果** ] ウィンドウに表示される結果をフィルター処理できます。 たとえば、保守容易性インデックスが65未満の結果のみを表示することができます。

 [ **フィルター** ] ドロップダウンボックスには、結果列の名前が表示されます。 フィルターが定義されると、一覧の一番下にインデントと共に追加されます。 一覧には、定義された最後の10個のフィルターを含めることができます。

#### <a name="to-filter-the-code-metrics-results"></a>コードメトリックスの結果をフィルター処理するには

1. [ **フィルター** ] ボックスの一覧から列名を選択します。

2. [ **最小**] で、表示する最小値を入力します。

3. [ **最大**] で、表示される最大値を入力します。

4. [ **フィルターの適用** ] ボタンをクリックします。

5. 結果の詳細を表示するには、階層ツリーを展開します。

## <a name="adding-removing-and-rearranging-data-columns"></a><a name="BKMK_AddingRemovingandRearrangingDataColumns"></a> データ列の追加、削除、および並べ替え
 [ **コードメトリックスの結果** ] ウィンドウで結果列を追加または削除できます。 また、結果列を目的の順序で表示されるように再配置することもできます。

#### <a name="to-remove-a-column"></a>列を削除するには

1. [ **列の追加と削除** ] ボタンをクリックします。

     \- または

     列見出しを右クリックし、[ **列の追加と削除**] をクリックします。

2. [ **列の追加と削除** ] ダイアログボックスで、削除する列のチェックボックスをオフにし、[ **OK**] をクリックします。

#### <a name="to-add-a-previously-removed-column"></a>以前に削除した列を追加するには

1. [ **列の追加と削除** ] ボタンをクリックします。

     \- または

     列見出しを右クリックし、[ **列の追加と削除**] をクリックします。

2. [ **列の追加と削除** ] ダイアログボックスで、追加する列のチェックボックスをオンにし、[ **OK**] をクリックします。

#### <a name="to-rearrange-columns"></a>列を再配置するには

1. [ **列の追加と削除** ] ボタンをクリックします。

     \- または

     列見出しを右クリックし、[ **列の追加と削除**] をクリックします。

2. [ **列の追加と削除** ] ダイアログボックスで、移動する列を選択し、上矢印または下矢印をクリックします。

3. 列が必要な位置に配置されたら、[ **OK]** をクリックします。

## <a name="copying-data-to-the-clipboard-or-excel"></a><a name="BKMK_Copying_Data_to_the_Clipboard_or_Excel"></a> クリップボードまたは Excel へのデータのコピー
 選択した行のコードメトリックスデータをクリップボードにコピーするには、各データ列の名前と値の1行を含むテキスト文字列を選択します。 また、[ **Microsoft excel でリストを開く** ] をクリックして、すべてのコードメトリックスの結果を excel スプレッドシートにエクスポートすることもできます。

## <a name="creating-a-work-item-based-on-code-metric-results"></a><a name="BKMK_Creating_a_Work_Item_Based_on_Code_Metric_Results"></a> コードメトリックスの結果に基づいて作業項目を作成する
 [!INCLUDE[esprfound](../includes/esprfound-md.md)]**コードメトリックスの結果**ウィンドウで、結果に基づいて作業項目を作成できます。 作業項目が作成されると、によって [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [ **タイトル** ] フィールドにタイトルとコードメトリックスデータが自動的に [ **履歴** ] タブに入力されます。

 作業項目を作成する方法の詳細については、「 [作業項目 &#91;リダイレクト&#93;を作成 ](https://msdn.microsoft.com/24b2e064-16ac-4bf0-8de4-98a1f48b8c4b)する」を参照してください。

#### <a name="to-create-a-work-item-based-on-a-result"></a>結果に基づいて作業項目を作成するには

1. 結果を右クリックします。

2. [ **作業項目の作成**] をポイントし、作成する作業項目の種類 (**バグ**、 **タスク**など) をクリックします。

3. すべての必須フィールドに入力して、作業項目フォームを完成させます。

4. [ **ファイル** ] メニューの [ **すべてを保存** ] をクリックして、作業項目を保存します。

#### <a name="to-create-a-bug-based-on-a-result"></a>結果に基づいてバグを作成するには

1. 結果をクリックして選択します。

2. [ **作業項目の作成** ] ボタンをクリックします。

3. すべての必須フィールドに入力して、作業項目フォームを完成させます。

4. [ **ファイル** ] メニューの [ **すべてを保存** ] をクリックして、作業項目を保存します。

## <a name="see-also"></a>参照
 [マネージコードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)[方法: コードメトリックスデータを生成する](../code-quality/how-to-generate-code-metrics-data.md)
