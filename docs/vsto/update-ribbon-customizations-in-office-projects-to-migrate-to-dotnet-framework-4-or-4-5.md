---
title: .NET Framework 4.5 に移行されたリボンのカスタマイズを更新する
description: ターゲットフレームワークが .NET Framework 4 以降に変更された場合に、プロジェクトコードを変更する必要があることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a831bced793f13394a89d278a6be1cda959c775a
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527939"
---
# <a name="update-ribbon-customizations-migrated-to-net-framework-45"></a>.NET Framework 4.5 に移行されたリボンのカスタマイズを更新する

  [ **リボン (ビジュアルデザイナー)** ] プロジェクト項目を使用して作成されたリボンのカスタマイズがプロジェクトに含まれている場合、ターゲットフレームワークが以降に変更された場合は、プロジェクトコードに次の変更を加える必要があり [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ます。

- 生成されたリボン コードを変更する。

- 実行時にリボンコントロールをインスタンス化するコード、リボンイベントを処理するコード、またはリボンコンポーネントの位置をプログラムによって設定するコードを変更します。

## <a name="update-the-generated-ribbon-code"></a>生成されたリボンコードを更新する
 プロジェクトのターゲット フレームワークを [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降に変更する場合は、次の手順を実行して、リボン項目に対して生成されたコードを変更する必要があります。 更新する必要があるコード ファイルは、プログラミング言語の種類とプロジェクトの作成方法に応じて次のように異なります。

- Visual Basic プロジェクト、またはで作成した Visual C# プロジェクトでは、 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] または [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] リボンの分離コードファイル (*ribbonitem*) のすべての手順を実行します。Designer.cs または *Ribbonitem*。デザイナー .vb)。 Visual Basic プロジェクトの分離コードファイルを表示するには、**ソリューションエクスプローラー** の [**すべてのファイルを表示**] ボタンをクリックします。

- Visual Studio 2008 で作成してからにアップグレードした Visual C# プロジェクトでは [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 、リボンコードファイルの最初の2つの手順 (*ribbonitem*.Cs または *ribbonitem*.vb) を実行し、リボンの分離コードファイルで残りの手順を実行します。

### <a name="to-change-the-generated-ribbon-code"></a>生成されたリボン コードを変更するには

1. <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> の代わりに `Microsoft.Office.Tools.Ribbon.OfficeRibbon` から派生するように、リボン クラスの宣言を変更します。

2. リボン クラスのコンストラクターを次のように変更します。 コンストラクターに独自のコードを追加している場合は、コードを変更しないでください。 Visual Basic プロジェクトでは、パラメーターなしのコンストラクターのみを変更します。 その他のコンストラクターは無視します。

     .NET Framework 3.5 を対象とするプロジェクトのリボン クラスの既定のコンストラクターを次のコード例に示します。

    ```vb
    Public Sub New()
        MyBase.New()
        InitializeComponent()
    End Sub
    ```

    ```csharp
    public Ribbon1()
    {
        InitializeComponent();
    }
    ```

     [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトのリボン クラスの既定のコンストラクターを次のコード例に示します。

    ```vb
    Public Sub New()
        MyBase.New(Globals.Factory.GetRibbonFactory())
        InitializeComponent()
    End Sub
    ```

    ```csharp
    public Ribbon1()
        : base(Globals.Factory.GetRibbonFactory())
    {
        InitializeComponent();
    }
    ```

3. `InitializeComponent` メソッドでは、代わりに <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> オブジェクトのいずれかのヘルパー メソッドが使用されるように、リボン コントロールを構築するすべてのコードを変更します。

    > [!NOTE]
    > Visual C# プロジェクトでは、`Component Designer generated code` メソッドを表示するために `InitializeComponent` という名前の領域を展開する必要があります。

     たとえば、.NET Framework 3.5 を対象とするプロジェクトで、<xref:Microsoft.Office.Tools.Ribbon.RibbonButton> という名前の `button1` をインスタンス化する次のコード行がファイルに含まれていると仮定します。

    ```vb
    Me.button1 = New Microsoft.Office.Tools.Ribbon.RibbonButton()
    ```

    ```csharp
    this.button1 = new Microsoft.Office.Tools.Ribbon.RibbonButton();
    ```

     [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトでは、代わりに次のコードを使用する必要があります。

    ```vb
    Me.button1 = Me.Factory.CreateRibbonButton()
    ```

    ```csharp
    this.button1 = this.Factory.CreateRibbonButton();
    ```

     リボンコントロールのヘルパーメソッドの完全な一覧については、「 [リボンコントロールのインスタンス化](#ribboncontrols)」を参照してください。

4. Visual C# プロジェクトでは、代わりに特定のリボン デリゲートが使用されるように、`InitializeComponent` デリゲートを使用する <xref:System.EventHandler%601> メソッドのコード行を変更します。

     たとえば、.NET Framework 3.5 を対象とするプロジェクトで、<xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> イベントを処理する次のコード行がファイルに含まれていると仮定します。

    \<CodeContentPlaceHolder>8 </CodeContentPlaceHolder> 以降を対象とするプロジェクトで [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] は、代わりに次のコードを使用する必要があります。

    \<CodeContentPlaceHolder>9 </CodeContentPlaceHolder> リボンデリゲートの完全な一覧については、「 [リボンイベントの処理](#ribbonevents)」を参照してください。

5. Visual Basic プロジェクトでは、ファイルの最後にある `ThisRibbonCollection` クラスを検索します。 このクラスが `Microsoft.Office.Tools.Ribbon.RibbonReadOnlyCollection` から継承されないように、クラスの宣言を変更します。

## <a name="instantiate-ribbon-controls"></a><a name="ribboncontrols"></a> リボンコントロールのインスタンス化
 リボン コントロールを動的にインスタンス化するすべてのコードを変更する必要があります。 .NET Framework 3.5 を対象とするプロジェクトでは、リボン コントロールは特定のシナリオで直接インスタンス化できるクラスです。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトでは、これらのコントロールはインターフェイスであるため、直接インスタンス化できません。 コントロールを作成するには、<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> オブジェクトが提供するメソッドを使用する必要があります。

 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> オブジェクトにアクセスするには、次の 2 つの方法があります。

- リボンクラスのファクトリプロパティを使用します。 この方法は、リボン クラス内のコードから使用します。

- `Globals.Factory.GetRibbonFactory` メソッドの使用。 この方法は、リボン クラス外のコードから使用します。 Globals クラスの詳細については、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

  次のコード例は、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトのリボン クラスで <xref:Microsoft.Office.Tools.Ribbon.RibbonButton> を作成する方法を示しています。

\<CodeContentPlaceHolder>10 </CodeContentPlaceHolder> 
 \<CodeContentPlaceHolder> 11 </CodeContentPlaceHolder> 次の表に、プログラムによって作成できるコントロールと、以降を対象とするプロジェクトでのコントロールの作成に使用するメソッドを示し [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ます。

|コントロール|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降のプロジェクトで使用する RibbonFactory メソッド|
|-------------| - |
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonButton%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonButtonGroup%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonCheckBox%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonComboBox%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDialogLauncher%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>:|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDropDown%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDownItem>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDropDownItem%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonEditBox%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonGallery%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonGroup%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonLabel%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonManager>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonManager%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonMenu%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonSeparator%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonSplitButton%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonTab%2A>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonToggleButton%2A>|

## <a name="handle-ribbon-events"></a><a name="ribbonevents"></a> リボンイベントの処理
 リボン コントロールのイベントを処理するすべてのコードを変更する必要があります。 .NET Framework 3.5 を対象とするプロジェクトでは、これらのイベントは汎用の <xref:System.EventHandler%601> デリゲートによって処理されます。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトでは、これらのイベントは他のデリゲートによって処理されるようになりました。

 次の表は、リボンのイベントと、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトでこれらのイベントに関連付けられているデリゲートを示しています。

|event|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降のプロジェクトで使用するデリゲート|
|-----------| - |
|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage> 生成されたリボンクラスのイベント|<xref:Microsoft.Office.Tools.Ribbon.RibbonLoadImageEventHandler>|
|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>|<xref:Microsoft.Office.Tools.Ribbon.RibbonUIEventHandler>|
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.TextChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.ButtonClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.SelectionChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox.TextChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ButtonClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click>|<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventHandler>|

## <a name="set-the-position-of-a-ribbon-component-programmatically"></a>リボンコンポーネントの位置をプログラムによって設定する
 リボンのグループ、タブ、またはコントロールの位置を設定するすべてのコードを変更する必要があります。 .NET Framework 3.5 を対象とするプロジェクトでは、静的な `AfterOfficeId` クラスの `BeforeOfficeId` メソッドと `Microsoft.Office.Tools.Ribbon.RibbonPosition` メソッドを使用して、グループ、タブ、またはコントロールの `Position` プロパティを割り当てることができます。 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 以降を対象とするプロジェクトでは、<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> オブジェクトが提供する <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.RibbonPosition%2A> プロパティを使用して、これらのメソッドにアクセスする必要があります。

 <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> オブジェクトにアクセスするには、次の 2 つの方法があります。

- リボン クラスの `Factory` プロパティの使用。 この方法は、リボン クラス内のコードから使用します。

- `Globals.Factory.GetRibbonFactory` メソッドの使用。 この方法は、リボン クラス外のコードから使用します。 Globals クラスの詳細については、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

  次のコード例は、.NET Framework 3.5 を対象とするプロジェクトでリボン クラスのタブの `Position` プロパティを設定する方法を示しています。

```vb
Me.tab1.Position = RibbonPosition.AfterOfficeId("TabHome")
```

```csharp
this.tab1.Position = RibbonPosition.AfterOfficeId("TabHome");
```

 次のコード例は、同じタスクを [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] を対象とするプロジェクトで行う方法を示しています。

```vb
Me.tab1.Position = Me.Factory.RibbonPosition.AfterOfficeId("TabHome")
```

```csharp
this.tab1.Position = this.Factory.RibbonPosition.AfterOfficeId("TabHome");
```

## <a name="see-also"></a>関連項目
- [Office ソリューションを .NET Framework 4 以降に移行する](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)
- [リボン デザイナー](../vsto/ribbon-designer.md)
