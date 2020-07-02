---
title: データへの WPF コントロールのバインド (パート 2) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 00dd5147-db0b-4b59-8d6c-8229b09ca9dd
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 06428a633aec41489a8a77655d6ea9442ffffaa0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540089"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>Visual Studio でデータに WPF コントロールをバインドする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データバインドコントロールを作成する [!INCLUDE[TLA#tla_titlewinclient](../includes/tlasharptla-titlewinclient-md.md)] には、[**データソース**] ウィンドウを使用します。 最初に、データソースを [**データソース**] ウィンドウに追加します。 次に、[**データソース**] ウィンドウから**WPF デザイナー**に項目をドラッグします。

## <a name="add-a-data-source-to-the-data-sources-window"></a><a name="adding"></a>[データソース] ウィンドウにデータソースを追加する
 データバインドコントロールを作成するには、まずデータソースを [**データソース**] ウィンドウに追加する必要があります。

#### <a name="to-add-a-data-source-to-the-data-sources-window"></a>[データ ソース] ウィンドウにデータ ソースを追加するには

1. [**表示**] メニューの [**その他のウィンドウ**] をポイントし、[**データソース**] をクリックします。

2. **[新しいデータ ソースの追加]** をクリックして、**データ ソース構成ウィザード**の操作を完了します。

3. 次のいずれかのタスクを実行して、データ バインド コントロールを作成します。

    - [1 つのデータフィールドにバインドされたコントロールを作成](#simple)する。

    - [複数のデータフィールドにバインドされたコントロールを作成](#complex)する。

    - [複数のデータフィールドにバインドされるコントロールのセットを作成](#details)する。

    - [デザイナーの既存のコントロールにデータをバインドする](#existing)。

## <a name="create-a-control-that-is-bound-to-a-single-field-of-data"></a><a name="simple"></a>1つのデータフィールドにバインドされたコントロールを作成する
 [**データソース**] ウィンドウにデータソースを追加した後、やなどの単一のデータフィールドを表示する新しいデータバインドコントロールを作成できます <xref:System.Windows.Controls.ComboBox> <xref:System.Windows.Controls.TextBox> 。

#### <a name="to-create-a-control-that-is-bound-to-a-single-field-of-data"></a>単一のデータ フィールドにバインドされるコントロールを作成するには

1. [**データソース**] ウィンドウで、テーブルまたはオブジェクトを表す項目を展開します。 バインドする列またはプロパティを表す子項目を検索します。 視覚的な例については、「[[データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)」を参照してください。

2. 必要に応じて、作成するコントロールを選択します。 [**データソース**] ウィンドウの各項目には、デザイナーに項目をドラッグしたときに作成される既定のコントロールがあります。 既定のコントロールは、項目の基になるデータ型によって異なります。

     既定以外のコントロールを選択するには、項目の横にあるドロップダウン矢印をクリックし、コントロールを選択します。 詳細については、「[[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

3. デザイナーの有効なコンテナーに項目をドラッグします。 有効なコンテナーの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]新しいデータバインドコントロールを作成し、適切なタイトルを <xref:System.Windows.Controls.Label> コンテナーに作成します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]では、 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] コントロールをデータにバインドするためのコードとコードも生成されます。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

## <a name="create-a-control-that-is-bound-to-multiple-fields-of-data"></a><a name="complex"></a>複数のデータフィールドにバインドされたコントロールを作成する
 [**データソース**] ウィンドウにデータソースを追加した後、やなど、複数のデータフィールドを表示する新しいデータバインドコントロールを作成でき <xref:System.Windows.Controls.DataGrid> ます <xref:System.Windows.Controls.ListView> 。

#### <a name="to-create-a-control-that-is-bound-to-multiple-fields-of-data"></a>複数のデータ フィールドにバインドされるコントロールを作成するには

1. [**データソース**] ウィンドウで、テーブルまたはオブジェクトを表すアイテムを選択します。 視覚的な例については、「[[データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)」を参照してください。

2. 必要に応じて、作成するコントロールを選択します。 既定では、データテーブルまたはオブジェクトを表す [**データソース**] ウィンドウの各項目は、 <xref:System.Windows.Controls.DataGrid> (プロジェクトが .NET Framework 4 を対象としている場合) または <xref:System.Windows.Controls.ListView> (以前のバージョンの .NET Framework の場合) を作成するように設定されます。

     既定以外のコントロールを選択するには、項目の横にあるドロップダウン矢印をクリックし、コントロールを選択します。 詳細については、「[[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

    > [!NOTE]
    > 特定の列またはプロパティを表示しないようにする場合は、項目を展開してその子を表示します。 表示しない列またはプロパティの横にあるドロップダウン矢印をクリックし、[**なし**] をクリックします。

3. デザイナーで、<xref:System.Windows.Controls.Grid> などの有効なコンテナーに項目をドラッグします。 有効なコンテナーの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]新しいデータバインドコントロールをコンテナーに作成します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]では、 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] コントロールをデータにバインドするためのコードとコードも生成されます。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

## <a name="create-a-set-of-controls-that-are-bound-to-multiple-fields-of-data"></a><a name="details"></a>複数のデータフィールドにバインドされるコントロールのセットを作成する
 [**データ**ソース] ウィンドウにデータソースを追加した後、データテーブルまたはオブジェクトをコントロールのセットにバインドできます。 テーブルまたはオブジェクトの列やプロパティごとに、異なるコントロールが作成されます。

#### <a name="to-create-a-set-of-controls-that-are-bound-to-multiple-fields-of-data"></a>複数のデータ フィールドにバインドされるコントロール セットを作成するには

1. [**データソース**] ウィンドウで、テーブルまたはオブジェクトを表すアイテムを選択します。 視覚的な例については、「[[データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)」を参照してください。

2. 項目の横にあるドロップダウン矢印をクリックし、[**詳細**] を選択します。

    > [!NOTE]
    > 特定の列またはプロパティを表示しないようにする場合は、項目を展開してその子を表示します。 表示しない列またはプロパティの横にあるドロップダウン矢印をクリックし、[**なし**] をクリックします。

3. デザイナーで、<xref:System.Windows.Controls.Grid> などの有効なコンテナーに項目をドラッグします。 有効なコンテナーの詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]コンテナー内に新しいデータバインドコントロールを作成します。 各コントロールは別々の列またはプロパティにバインドされ、適切なタイトルの <xref:System.Windows.Controls.Label> コントロールが追加されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]また、 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] は、コントロールをデータにバインドするためのコードも生成します。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

## <a name="binddata-to-existing-controls-in-the-designer"></a><a name="existing"></a>デザイナーの既存のコントロールに対する binddata
 [**データ**ソース] ウィンドウにデータソースを追加すると、デザイナーの既存のコントロールにデータバインディングを追加できます。

#### <a name="to-bind-data-to-an-existing-control-in-the-designer"></a>デザイナー内の既存のコントロールにデータをバインドするには

1. [**データソース**] ウィンドウで、次のいずれかの手順を実行します。

    - <xref:System.Windows.Controls.DataGrid> や <xref:System.Windows.Controls.ListView> など、複数のデータ フィールドを表示する既存のコントロールにデータ バインディングを追加するには、コントロールにバインドするテーブルまたはオブジェクトを表す項目を選択します。

    - <xref:System.Windows.Controls.ComboBox> や <xref:System.Windows.Controls.TextBox> など、単一のデータ フィールドを表示する既存のコントロールにデータ バインディングを追加するには、データが格納されているテーブルまたはオブジェクトを表す項目を展開し、コントロールにバインドするデータを表す項目を選択します。

2. 選択した項目を [**データソース**] ウィンドウからデザイナーの既存のコントロールにドラッグします。 コントロールは、有効なドロップ ターゲットである必要があります。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)][!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)]コントロールをデータにバインドするためのコードとコードを生成します。 詳細については、「 [Visual Studio でのデータへの WPF コントロールのバインド](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)」を参照してください。

    > [!NOTE]
    > コントロールが既にデータにバインドされている場合は、コントロールのデータ バインディングが、最後にコントロールにドラッグされた項目に再設定されます。

## <a name="see-also"></a>関連項目
 [Visual Studio のデータに wpf コントロールをバインドする](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [wpf アプリケーションで参照テーブルを作成](../data-tools/create-lookup-tables-in-wpf-applications.md)する wpf[アプリケーションの関連データを表示](../data-tools/display-related-data-in-wpf-applications.md)する wpf コントロールを[dataset に](../data-tools/bind-wpf-controls-to-a-dataset.md)バインドする[WCF データサービスへの wpf コントロールのバインド](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)[チュートリアル: wpf アプリケーションでの関連データの表示](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)
