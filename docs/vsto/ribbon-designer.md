---
title: リボン デザイナー
description: リボンデザイナーを使用して、Microsoft Office アプリケーションのリボンにカスタムタブ、グループ、およびコントロールを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- Designer_Microsoft.VisualStudio.Tools.Office.Ribbon.Design.RibbonDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, about Ribbon Designer
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- customizing the Ribbon, about Ribbon Designer
- Ribbon [Office development in Visual Studio], visual designer
- customizing the Ribbon
- custom Ribbon
- designers [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Ribbon [Office development in Visual Studio], common tasks
- Ribbon Designer [Office development in Visual Studio]
- read-only properties
- Ribbon [Office development in Visual Studio], shortcut keys
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b72270da75d27ed2837540369f74e9c5e87b417b
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527998"
---
# <a name="ribbon-designer"></a>リボン デザイナー
  リボン デザイナーは、ビジュアルなデザイン キャンバスです。 リボンデザイナーを使用して、Microsoft Office アプリケーションのリボンにカスタムタブ、グループ、およびコントロールを追加します。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 リボンデザイナーを開くには、プロジェクトに **リボン (ビジュアルデザイナー)** 項目を追加します。 その後、デザイン ツールを使用して、以下のタスクを実行できます。

- [リボン レイアウトのデザイン](#DesigningRibbonLayout)

- [イベントの処理とコントロール プロパティの設定](#HandleEventsSetProperties)

- [Backstage ビューへのコントロールの追加](#CustomizingMicrosoftOfficeButton)

> [!NOTE]
> リボン デザイナーでは行うことのできないタスクがあります。 これらのタスクとその実行方法の詳細については、「 [リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

## <a name="add-a-ribbon-visual-designer-item-to-a-project"></a>プロジェクトへのリボン (ビジュアルデザイナー) 項目の追加
 リボンデザイナーを使用するには、新しい **リボン (ビジュアルデザイナー)** 項目をプロジェクトに追加します。 詳細については、「 [方法: リボンのカスタマイズを開始](../vsto/how-to-get-started-customizing-the-ribbon.md)する」を参照してください。

 新しい **リボン (ビジュアルデザイナー)** 項目を追加すると、visual Studio によって次のファイルがプロジェクトに自動的に追加されます。

- リボン コード ファイル。 このファイルには、[**新しい項目の追加**] ダイアログボックスの **リボン (ビジュアルデザイナー)** 項目に指定した名前が付いています。 このファイルには、リボンのイベントを処理するコードを追加します。

- リボン デザイナー コード ファイル。 このファイルには、リボン デザイナーによって生成されるコードが格納されます。直接編集することはできません。

- リソース ファイル。 このファイルには、リボン上の各コントロールのプロパティ値が含まれています。

  別のプロジェクトの **リボン (ビジュアルデザイナー)** 項目が既にある場合は、[ **既存項目の追加** ] ダイアログボックスを使用して、現在のプロジェクトで再利用できます。

## <a name="design-a-ribbon"></a><a name="DesigningRibbonLayout"></a> リボンをデザインする
 リボン デザイナーを開くには、次の 3 つの方法があります。

- **ソリューションエクスプローラー** で、リボンコードファイルをダブルクリックします。

- **ソリューションエクスプローラー** で、リボンコードファイルを右クリックし、[デザイナーの **表示**] をクリックします。

- **ソリューションエクスプローラー** で、リボンコードファイルを選択し、[**表示**] メニューの [**デザイナー** ] をクリックします。

  リボン デザイナーには、既定のタブとグループがあります。 既定のタブとグループは、リボン デザイナーから削除することができます。 既定のグループを削除するには、[ **Group1**] を右クリックし、[ **削除**] をクリックします。 既定のタブを削除するには、デザイン画面の空の領域を右クリックし、[ **リボンタブの削除**] をクリックします。

  リボン デザイナーにカスタム タブ、グループ、およびコントロールを追加することもできます。 これらのコントロールは、[ **ツールボックス**] の [ **Office リボンコントロール** ] グループにあります。 **Office リボンコントロール** グループからリボンデザイナーにコントロールを追加するには、次の3つの方法があります。

- リボン デザイナーの適切な領域にコントロールをドラッグします。

- コントロールをクリックし、リボン デザイナーの適切な領域をクリックします。

- デザイナーで適切な領域を選択し、 **ツールボックス** のコントロールをダブルクリックします。

### <a name="ribbon-design-workflow"></a>リボンデザインワークフロー
 リボンのレイアウトをデザインするときの基本的な手順は次のとおりです。

1. [リボンにカスタムタブを追加](#AddTabToRibbon)します。

2. [タブにグループを追加](#AddGroupsToTab)します。

3. [グループにコントロールを追加](#AddControlsToGroups)します。

   コントロールはグループにのみドロップできます。コントロールをタブまたはリボンに直接ドラッグすることはできません。 グループはタブでのみ削除できます。グループをリボンに直接ドラッグすることはできません。

   コントロールを正確な位置にドラッグして、配置します。 コントロールのプロパティを設定するには、[ **プロパティ** ] ウィンドウを使用します。

   リボン上のタブから別のタブにコントロールをドラッグすることはできません。 コントロールを別のタブに移動する場合は、[ **切り取り** ] コマンドを使用して1つのタブからコントロールを削除し、別のタブにコントロールを貼り付ける必要があります。コントロールを切り取って貼り付けた場合、イベントハンドラーは動作を停止します。 イベントハンドラーは、[ **プロパティ** ] ウィンドウで再接続できます。 詳細については、「 [プロパティウィンドウ](../ide/reference/properties-window.md)」を参照してください。

### <a name="add-custom-tabs-to-the-ribbon"></a><a name="AddTabToRibbon"></a> リボンへのカスタムタブの追加
 リボンにカスタムタブを追加するには、次の3つの方法があります。

- **ツールボックス** からタブを追加します。

- リボンデザイナーを右クリックし、[ **リボンタブの追加**] をクリックします。

- **タブコレクションエディター** を開き、[**追加**] をクリックします。

   **タブコレクションエディター** を開くには、[**プロパティ**] ウィンドウで、[**タブ**] プロパティを選択し、省略記号ボタン [ ![ASP.NET Mobile Designer](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")] をクリックします。

  タブを追加すると、グループを追加してコントロールを含めることができます。

#### <a name="remove-custom-tabs-from-the-ribbon"></a>リボンからカスタムタブを削除する
 リボンからカスタムタブを削除するには、次の3つの方法があります。

- デザイナーを右クリックし、[ **リボンタブの削除]** をクリックします。

- [**プロパティ**] ウィンドウの [**コマンド**] ペインで、[**リボンタブの削除**] をクリックします。

- **タブコレクションエディター** を開き、[] タブを選択し、[**削除**] をクリックします。

#### <a name="change-the-position-of-a-tab-on-the-ribbon"></a>リボンのタブの位置を変更する
 リボンのカスタムタブの順序を変更できます。 また、リボンの組み込みタブの前または後にカスタムタブを配置することもできます。 詳細については、「 [方法: リボンのタブの位置を変更する](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)」を参照してください。

#### <a name="customize-built-in-tabs-on-the-ribbon"></a>リボンの組み込みタブをカスタマイズする
 組み込みタブは、既に Microsoft Office アプリケーションのリボン上にあるタブです。 たとえば、[ **データ** ] タブは Excel の組み込みタブです。

 組み込みタブにグループとコントロールを追加できます。既定では、カスタムグループは、組み込みタブの最後のグループとして表示されますが、タブ上の組み込みグループの前または後に移動できます。

 組み込みグループを削除することはできません。

 組み込みタブをカスタマイズする方法の詳細については、「 [方法: 組み込みタブをカスタマイズ](../vsto/how-to-customize-a-built-in-tab.md)する」を参照してください。

### <a name="add-groups-to-a-tab"></a><a name="AddGroupsToTab"></a> タブへのグループの追加
 グループは、リボン上のコントロールを論理的に整理します。 タブにグループを追加します。 グループに、他のすべてのコントロールを追加します。

### <a name="add-controls-to-groups"></a><a name="AddControlsToGroups"></a> グループへのコントロールの追加
 グループに 1 つ以上のコントロールを追加します。 各コントロールの説明を次の表に示します。

|コントロール|説明|
|-------------|-----------------|
|**ボックス**|グループ内のコントロールを整理するコンテナー。 区切り記号、グループ、またはタブを除く、任意のコントロールをボックスに追加できます。ボックスは、水平方向または垂直方向のどちらでもかまいません。|
|**Button**|アクションを起動するボタン。 ボタンは、グループ、ボタン グループ、ドロップダウン リスト、ギャラリ、メニュー、分割ボタンのいずれかに追加できます。|
|**ButtonGroup**|1 つ以上のボタン、トグル ボタン、メニュー、分割ボタン、ギャラリを含むグループ。 ボタン グループは、グループまたはメニューに追加できます。|
|**CheckBox**|オンまたはオフにしてオプションの有効/無効を切り換えるボックス。|
|**ComboBox**|リスト ボックスが付属したエディット ボックス。 ユーザーは、選択内容を入力したり、選択したりできます。 ボックスには、現在の選択項目が表示されます。 プロパティを使用して、 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Items%2A> リボンが Office アプリケーションに読み込まれる前または後に、実行時に項目を追加および削除します。|
|**DropDown**|ユーザーが選択できる項目の一覧。 ユーザーがドロップダウン リストに新しい項目を入力することはできません。<br /><br /> 一覧に項目を追加するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Items%2A> プロパティを使用します。 項目の追加や削除は、実行時に行うことができます。<br /><br /> 一覧にボタンを追加するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.Buttons%2A> プロパティを使用します。 ただし、リボンが Office アプリケーションに読み込まれた後は、実行時にボタンを追加したり削除したりすることはできません。|
|**EditBox**|ユーザーがテキストを入力できるボックス。|
|**[ギャラリー]**|ユーザーが選択できる項目を配列やグリッドで視覚的に示すメニュー。 メニューの選択項目のレイアウトを調整できます。 ギャラリの項目やボタンを表示する行や列の数を指定するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> プロパティと <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> プロパティを使用します。|
|**Label**|リボン上のコントロールを識別するために使用できるテキストです。|
|**Menu**|ドロップダウン リスト。次のいずれかのコントロールを含めることができます。<br /><br /> -ボタン<br />-チェックボックス<br />-ギャラリー<br />-メニュー<br />-分割ボタン<br />-トグルボタン<br />-Separator<br /><br /> リボン デザイナーのメニューにコントロールを追加するには、メニューの下向き矢印をクリックし、メニューのデザイン サーフェイスを開きます。 次に、[ **ツールボックス** ] からリボンコントロールをメニューにドラッグします。 コントロールを並べ替えるには、コントロールを目的の位置にドラッグします。<br /><br /> リボンが Office アプリケーションに読み込まれた後にコントロールを追加するには、 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> リボンが読み込まれる前に、プロパティを **true** に設定する必要があります。 この方法の詳細については、「 [リボンオブジェクトモデルの概要](../vsto/ribbon-object-model-overview.md)」を参照してください。|
|**Separator**|一覧内の項目を分割するために使用する細いバー。 グループに追加すると、バーは垂直に表示されます。 メニュー追加すると、バーは水平に表示されます。|
|**SplitButton**|メニューが付属したボタン。 以下の任意のコントロールを含めることができます。<br /><br /> -ボタン<br />-チェックボックス<br />-ギャラリー<br />-メニュー<br />-分割ボタン<br />-トグルボタン<br />-Separator<br /><br /> メニューと同様に、分割ボタンにも独自のデザイン サーフェイスがあります。 ただし、メニューとは異なり、[分割] ボタンの項目を更新できるのは、リボンが Office アプリケーションに読み込まれる前だけです。 分割ボタンの項目を更新する方法の詳細については、「 [リボンオブジェクトモデルの概要](../vsto/ribbon-object-model-overview.md)」を参照してください。|
|**ToggleButton**|押された状態または押されていない状態で表示されるボタン。|

## <a name="handle-events-and-setting-properties"></a><a name="HandleEventsSetProperties"></a> イベントの処理とプロパティの設定
 リボンデザイナーを使用すると、[ **プロパティ** ] ウィンドウを使用して、デザイン時にコントロールのプロパティを設定できます。 さらに、リボンは、実行時にリボンコントロールのプロパティを取得および設定するために使用できる、厳密に型指定されたオブジェクトモデルを公開します。

 デザイナー上の任意のコントロールをダブルクリックすると、そのコントロールの既定のイベントのイベント ハンドラーが開きます。 [ **プロパティ** ] ウィンドウを使用すると、他のすべてのコントロールイベントのイベントハンドラーを作成できます。

 リボンのイベントとプロパティは、<xref:Microsoft.Office.Tools.Ribbon> 名前空間に格納されています。 **リボン (ビジュアルデザイナー)** 項目によって、プロジェクト内のこのアセンブリへの参照が自動的に追加され、リボンコードファイルの先頭に適切な **Using** または **Imports** ステートメントが挿入されます。

 リボンイベントの処理、および実行時のリボンコントロールのプロパティの設定の詳細については、「 [リボンオブジェクトモデルの概要](../vsto/ribbon-object-model-overview.md)」を参照してください。

## <a name="customize-backstage-view"></a><a name="CustomizingMicrosoftOfficeButton"></a> Backstage ビューのカスタマイズ
 リボンデザイナーを使用すると、[ **ファイル** ] タブをクリックしたときに表示されるメニューにコントロールを追加できます。このメニューを Backstage ビューと呼びます。

 リボン デザイナーを使用して、ビルトイン コントロールの前または後ろにコントロールを配置することはできません。 ビルトイン コントロールは、Backstage ビューで既に表示されているコントロールです。 ビルトイン コントロールの前または後ろにコントロールを配置するには、リボン XML を使用する必要があります。 **リボン (xml)** の詳細については、「[リボン xml](../vsto/ribbon-xml.md)」を参照してください。 Backstage ビューのカスタマイズの詳細については、「 [開発者向け office 2010 backstage ビューの概要](/previous-versions/office/developer/office-2010/ee691833(v=office.14)) 」および「 [開発者向けの office 2010 Backstage ビューのカスタマイズ](/previous-versions/office/developer/office-2010/ee815851(v=office.14))」を参照してください。

 [!INCLUDE[appliesto_ribbon_2010](../vsto/includes/appliesto-ribbon-2010-md.md)]

 Backstage ビューにコントロールを追加する方法については、「 [方法: backstage ビューにコントロールを追加](../vsto/how-to-add-controls-to-the-backstage-view.md)する」を参照してください。

## <a name="accessibility-in-the-ribbon-designer"></a><a name="Accessibility"></a> リボンデザイナーのユーザー補助機能
 キーボード ショートカットを使用して、リボン デザイナーのコントロールを移動できます。 キーボード ショートカットには、すべてのコントロールに適用されるものと、メニューを備えたコントロールにのみ適用されるものがあります。

 すべてのコントロールに適用されるキーボード ショートカットを、次の表に示します。

|アクション|キーボード ショートカット|
|------------|-----------------------|
|一覧内の直前のコントロールの前に、コントロールを移動します。|**Ctrl** +**上**<br /><br /> **Ctrl** +**左**|
|一覧内の次のコントロールの後ろに、コントロールを移動します。|**Ctrl** +**ダウン**<br /><br /> **Ctrl** +**右**|
|コントロールでの選択を、同じグループ内の別のコントロールに移動します。 ドロップダウン パネルの場合は、親コントロールとドロップダウン パネル内のコントロールの間で移動します。|**Up**<br /><br /> **[下へ]**|
|すべてのコントロールを通して前方に進む処理を反復します。|**Tab**|
|すべてのコントロールを通して後方に進む処理を反復します。|**Shift**+**Tab**|
|選択したコントロール (1 つまたは一連のコントロール) を削除します。|**削除**|
|選択したコントロールをコピーします。|**Ctrl** +**C**|
|選択したコントロールを切り取ります。|**Ctrl** +**X**|
|クリップボードからコントロールを貼り付けます。|**Ctrl** +**V**|
|[ **ツールボックス**] を選択します。|**Ctrl** +**Alt** +**X**|
|親コンポーネントを選択します。|**Esc**|

 Microsoft Office メニュー、<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>、および <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> にのみ適用されるキーボード ショートカットを、次の表に示します。

|アクション|キーボード ショートカット|
|------------|-----------------------|
|ドロップダウン パネルが開いていて、パネル上で選択されているコントロールがある場合は、その親コントロールを選択します。|**Left**|
|ドロップダウン パネルが開いていて、親コントロールが選択されている場合は、ドロップダウン パネルを閉じます。|**Left**|
|ドロップダウン パネルを開きます。|**Right**|
|ドロップダウン パネルが開いている場合は、そのパネルにある最初のコントロールを選択します。|**Right**|
|ドロップダウン パネルを閉じます。|**Esc**|

## <a name="see-also"></a>関連項目

- [リボンの概要](../vsto/ribbon-overview.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [方法: リボンをリボンデザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
