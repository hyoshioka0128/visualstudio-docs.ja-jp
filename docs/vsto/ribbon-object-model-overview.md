---
title: リボンオブジェクトモデルの概要
description: Visual Studio Tools for Office ランタイムが、実行時にリボンコントロールのプロパティを取得および設定するために使用できる、厳密に型指定されたオブジェクトモデルを公開する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], object model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6306b13cc40d8b93de734168fe1e6df92c256d21
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888694"
---
# <a name="ribbon-object-model-overview"></a>リボンオブジェクトモデルの概要
  は、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 実行時にリボンコントロールのプロパティを取得および設定するために使用できる、厳密に型指定されたオブジェクトモデルを公開します。 たとえば、メニュー コントロールを動的に設定したり、コントロールの表示/非表示をコンテキストに応じて切り替えたりすることができます。 Office アプリケーションがリボンを読み込む前であれば、タブ、グループ、およびコントロールをリボンに追加することもできます。 詳細については、「読み取り専用に [なるプロパティの設定](#SettingReadOnlyProperties)」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 このリボンオブジェクトモデルは、主に [リボンクラス](#RibbonClass)、 [リボンイベント](#RibbonEvents)、および [リボンコントロールクラス](#RibbonControlClasses)で構成されています。

## <a name="ribbon-class"></a><a name="RibbonClass"></a> リボンクラス
 新しい **リボン (ビジュアルデザイナー)** 項目をプロジェクトに追加すると、visual Studio によってプロジェクトに **リボン** クラスが追加されます。 **リボン** クラスは、クラスから継承され <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> ます。

 このクラスは、リボン コード ファイルとリボン デザイナー コード ファイルを分割する部分クラスとして位置付けられます。

## <a name="ribbon-events"></a><a name="RibbonEvents"></a> リボンイベント
 **リボン** クラスには、次の3つのイベントが含まれています。

|Event|説明|
|-----------|-----------------|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Load>|Office アプリケーションがリボンのカスタマイズを読み込むときに発生します。 <xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>イベントハンドラーがリボンコードファイルに自動的に追加されます。 このイベント ハンドラーを使用して、リボンが読み込まれるときにカスタム コードを実行します。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.LoadImage>|リボンが読み込まれるときに、リボンのカスタマイズでイメージをキャッシュできます。 このイベントハンドラーにリボンイメージをキャッシュするコードを記述すると、パフォーマンスがわずかに向上します。 詳細については、「<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage>」を参照してください。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBase.Close>|リボンインスタンスが閉じたときに発生します。|

## <a name="ribbon-controls"></a><a name="RibbonControlClasses"></a> リボンコントロール
 名前空間には、 <xref:Microsoft.Office.Tools.Ribbon> **ツールボックス** の [ **Office リボンコントロール**] グループに表示される各コントロールの型が含まれています。

 各 `Ribbon` コントロールの型を次の表に示します。 各コントロールの説明については、「 [リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

|コントロール名|クラス名|
|------------------|----------------|
|**ボックス**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**Button**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|
|**ButtonGroup**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|
|**CheckBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|
|**ComboBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|
|**リスト**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>|
|**EditBox**|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**デザイン**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**グループ**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**Label**|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|
|**Menu**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**Separator**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|
|**SplitButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**Tab**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ToggleButton**|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|

 <xref:Microsoft.Office.Tools.Ribbon> 名前空間では、<xref:System.Windows.Forms> 名前空間に属するコントロール クラスとの名前の衝突を回避するために、型名にプレフィックス "Ribbon" が追加されています。

 リボン デザイナーにコントロールを追加すると、そのコントロールのクラスがリボン デザイナー コード ファイルにフィールドとして宣言されます。

### <a name="common-tasks-using-the-properties-of-ribbon-controls"></a>リボンコントロールのプロパティを使用する一般的なタスク
 各 `Ribbon` コントロールには、コントロールへのラベルの割り当てやコントロールの表示/非表示の切り替えなど、さまざまなタスクの実行に使用できるプロパティが含まれています。

 場合によっては、リボンが読み込まれるか、動的メニューにコントロールが追加された後に、プロパティが読み取り専用になります。 詳細については、「読み取り専用に [なるプロパティの設定](#SettingReadOnlyProperties)」を参照してください。

 `Ribbon` コントロールのプロパティを使用して実行できる一部のタスクについて、次の表で説明します。

|タスク :|これを行うには、次の手順を実行します。|
|--------------------|--------------|
|コントロールの表示/非表示を切り替える。|Visible プロパティを使用します。|
|コントロールを有効または無効にする。|Enabled プロパティを使用します。|
|コントロールのサイズを設定する。|ControlSize プロパティを使用します。|
|コントロールに表示するイメージを取得する。|Image プロパティを使用します。|
|コントロールのラベルを変更する。|"ラベル" プロパティを使用します。|
|ユーザー定義のデータをコントロールに追加する。|Tag プロパティを使用します。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>、<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>、<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton> コントロール。|Items プロパティを使用します。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>、<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>、<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> のいずれかのコントロールに項目を追加する。|Items プロパティを使用します。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu> にコントロールを追加する。|Items プロパティを使用します。<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>リボンが office アプリケーションに読み込まれた後にコントロールを追加するには、 <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.Dynamic%2A> office アプリケーションにリボンが読み込まれる前に、プロパティを **true** に設定する必要があります。 詳細については、「読み取り専用に [なるプロパティの設定](#SettingReadOnlyProperties)」を参照してください。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> 内の選択された項目を取得する。<br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>、、または <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 。|SelectedItem プロパティを使用します。 <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox> では、<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.Text%2A> プロパティを使用します。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab> 上のグループを取得する。|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab.Groups%2A> プロパティを使用します。|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> に表示する行および列の数を指定する。|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.RowCount%2A> プロパティおよび <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ColumnCount%2A> プロパティを使用します。|

## <a name="set-properties-that-become-read-only"></a><a name="SettingReadOnlyProperties"></a> 読み取り専用になるプロパティの設定
 リボンが読み込まれる前にのみ設定できるプロパティがあります。 それらのプロパティは次の 3 つの方法で設定できます。

- Visual Studio の [ **プロパティ** ] ウィンドウを表示します。

- **リボン** クラスのコンストラクター内。

- プロジェクトの `CreateRibbonExtensibilityObject`、`ThisAddin`、または `ThisWorkbook` クラスの `ThisDocument` メソッド

  動的メニューにはいくつかの例外があります。 メニューを含むリボンが読み込まれた後であっても、新しいコントロールを作成してそれらのプロパティを設定し、それらのコントロールを実行時に動的メニューに追加できます。

  動的メニューに追加するコントロールのプロパティは、いつでも設定できます。

  詳細については、「読み取り専用に [なるプロパティ](#ReadOnlyProperties)」を参照してください。

### <a name="set-properties-in-the-constructor-of-the-ribbon"></a>リボンのコンストラクターでプロパティを設定する
 `Ribbon`**リボン** クラスのコンストラクターで、コントロールのプロパティを設定できます。 このコードは、`InitializeComponent` メソッドの呼び出しの後に置く必要があります。 次のコード例は、現在の時刻が太平洋標準時間 (UTC-8) の 17:00 以降である場合に、新しいボタンをグループに追加します。

 次のコードを追加します。

 [!code-csharp[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.cs#1)]
 [!code-vb[Trin_Ribbon_ObjectModel#1](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/Ribbon1.Designer.vb#1)]

 Visual Studio 2008 からアップグレードした Visual C# プロジェクトでは、リボンコードファイルにコンストラクターが表示されます。

 Visual Basic プロジェクト、または [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] で作成した Visual C# プロジェクトでは、リボン デザイナー コード ファイルにコンストラクターがあります。 このファイルには、 *Ribbonitem* という名前が付けられます。Designer.cs または *Ribbonitem*。デザイナ. vb. このファイルを Visual Basic プロジェクトで表示するには、最初にソリューションエクスプローラーの [ **すべてのファイルを表示** ] ボタンをクリックする必要があります。

### <a name="set-properties-in-the-createribbonextensibilityobject-method"></a>CreateRibbonExtensibilityObject メソッドでのプロパティの設定
 プロジェクトの `Ribbon`、`CreateRibbonExtensibilityObject`、または `ThisAddin` のいずれかのクラスの `ThisWorkbook` メソッドをオーバーライドするときに、`ThisDocument` コントロールのプロパティを設定できます。 メソッドの詳細については `CreateRibbonExtensibilityObject` 、「 [リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

 次の例では、 `CreateRibbonExtensibilityObject` `ThisWorkbook` Excel ブックプロジェクトのクラスのメソッドでリボンプロパティを設定します。

 次のコードを追加します。

 [!code-vb[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/VisualBasic/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.vb#2)]
 [!code-csharp[Trin_Ribbon_ObjectModel#2](../vsto/codesnippet/CSharp/trin_Ribbon_objectmodel_dotnet4/ThisWorkbook.cs#2)]

### <a name="properties-that-become-read-only"></a><a name="ReadOnlyProperties"></a> 読み取り専用になるプロパティ
 次の表は、リボンが読み込まれる前にのみ設定できるプロパティを示しています。

> [!NOTE]
> 動的メニューのコントロールのプロパティは、いつでも設定できます。 この場合、次の表の内容は該当しません。

|プロパティ|リボン コントロール クラス|
|--------------|--------------------------|
|**BoxStyle**|<xref:Microsoft.Office.Tools.Ribbon.RibbonBox>|
|**ButtonType**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**渡さ**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ControlId**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**DialogLauncher**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|
|**動的**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|
|**グローバル**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**グループ**|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|
|**ImageName**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**ItemSize**|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|
|**MaxLength**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**名前**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComponent>|
|**Position**|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonTab><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|
|**RibbonType**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**行**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemImage**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemLabel**|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**ShowItemSelection**|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|
|**SizeString**|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|
|**StartFromScratch**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Tabs**|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon>|
|**Title**|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|

### <a name="set-properties-for-ribbons-that-appear-in-outlook-inspectors"></a>Outlook インスペクターに表示されるリボンのプロパティを設定する
 ユーザーがリボンを含むインスペクターを開くたびにリボンの新しいインスタンスが作成されます。 ただし、上の表に示すプロパティは、リボンの最初のインスタンスが作成される前にのみ設定できます。 最初のインスタンスが作成されると、そのインスタンスによって Outlook がリボンの読み込みに使用する XML ファイルを定義するため、これらのプロパティは読み取り専用になります。

 リボンの他のインスタンスが作成されたときにこれらのプロパティを別の値に設定する条件ロジックがある場合、そのコードは何の効果ももたらしません。

> [!NOTE]
> Outlook リボンに追加するコントロールごとに、 **Name** プロパティが設定されていることを確認します。 実行時にコントロールを Outlook リボンに追加する場合は、コードでこのプロパティを設定する必要があります。 デザイン時にコントロールを Outlook リボンに追加すると、"名前" プロパティが自動的に設定されます。

## <a name="ribbon-control-events"></a>リボンコントロールイベント
 各コントロール クラスに 1 つ以上のイベントが含まれています。 次の表は、それらのイベントについての説明です。

|Event|説明|
|-----------|-----------------|
|ここを|コントロールがクリックされたときに発生します。|
|TextChanged|編集ボックスまたはコンボ ボックス内のテキストが変更されたときに発生します。|
|ItemsLoading|Office によってコントロールの項目コレクションが要求されたときに発生します。 Office では、コードによってコントロールのプロパティが変更されるか、メソッドが呼び出されるまで、項目コレクションがキャッシュされ <xref:Microsoft.Office.Core.IRibbonUI.InvalidateControl%2A> ます。|
|System.windows.forms.toolbar.buttonclick>|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> または <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> 内のボタンがクリックされたときに発生します。|
|SelectionChanged|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown> または <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery> 内の選択項目が変更されたときに発生します。|
|[クリック]|グループの右下にあるダイアログ ランチャー アイコンがクリックされたときに発生します。|

 これらのイベントのイベント ハンドラーには、次の 2 つのパラメーターがあります。

|パラメーター|Description|
|---------------|-----------------|
|*センダー*|イベントを発生させたコントロールを表す <xref:System.Object>。|
|*e*|<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs> を格納している <xref:Microsoft.Office.Core.IRibbonControl>。 このコントロールを使用すると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって提供されるリボン オブジェクト モデルには用意されていないプロパティにアクセスできます。|

## <a name="see-also"></a>関連項目
- [実行時のリボンへのアクセス](../vsto/accessing-the-ribbon-at-run-time.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [方法: リボンのカスタマイズを開始する](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: 実行時にリボンのコントロールを更新する](../vsto/walkthrough-updating-the-controls-on-a-ribbon-at-run-time.md)
- [Outlook のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-outlook.md)
- [方法: 組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)
- [方法: Backstage ビューにコントロールを追加する](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [方法: リボンをリボンデザイナーからリボン XML にエクスポートする](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [方法: アドインのユーザーインターフェイスエラーを表示する](../vsto/how-to-show-add-in-user-interface-errors.md)
