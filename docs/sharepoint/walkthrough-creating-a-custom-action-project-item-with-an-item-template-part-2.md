---
title: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (第2部)
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], creating template wizards
- SharePoint project items, creating template wizards
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ae9c686e46bf6a956d58ac22b823dcc36c2aacce
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189159"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 2)
  SharePoint プロジェクト項目のカスタムの種類を定義し、Visual Studio の項目テンプレートに関連付けると、テンプレートのウィザードを指定することもできます。 ウィザードを使用すると、ユーザーがテンプレートを使用してプロジェクトにプロジェクト項目の新しいインスタンスを追加するときに、ユーザーから情報を収集できます。 収集した情報を使用して、プロジェクト項目を初期化できます。

 このチュートリアルでは、「[チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」で説明されているカスタム動作プロジェクト項目にウィザードを追加します。 ユーザーがカスタム動作プロジェクト項目を SharePoint プロジェクトに追加すると、ウィザードによって、カスタム動作に関する情報 (場所や、エンドユーザーが選択したときに移動する URL など) が収集され、この情報がの要素 .xml ファイルに追加され*ます。* 新しいプロジェクト項目。

 このチュートリアルでは、次のタスクについて説明します。

- 項目テンプレートに関連付けられているカスタム SharePoint プロジェクト項目の種類のウィザードを作成します。

- Visual Studio で SharePoint プロジェクトアイテムの組み込みウィザードに似たカスタムウィザード UI を定義します。

- 置き換え可能パラメーターを使用して、ウィザードで収集したデータで SharePoint プロジェクト ファイルを初期化します。

- ウィザードをデバッグおよびテストします。

> [!NOTE]
> ワークフローのカスタムアクティビティを作成する方法を示すサンプルを[Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities)からダウンロードできます。

## <a name="prerequisites"></a>必要条件
 このチュートリアルを実行するには、まず「[チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成 (パート 1)」](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)を完了して、CustomActionProjectItem ソリューションを作成する必要があります。

 また、このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、SDK の**Vsix プロジェクト**テンプレートを使用して、プロジェクト項目を配置する vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- Visual Studio のプロジェクトおよび項目テンプレート用のウィザード。 詳細については、「[方法: プロジェクトテンプレート](../extensibility/how-to-use-wizards-with-project-templates.md)と <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを使用してウィザードを使用する」を参照してください。

- SharePoint のカスタム動作。 詳細については、「[カスタムアクション](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14))」を参照してください。

## <a name="create-the-wizard-project"></a>ウィザードプロジェクトの作成
 このチュートリアルを完了するには、「[チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)」で作成した CustomActionProjectItem ソリューションにプロジェクトを追加する必要があります。 このプロジェクトで、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装し、ウィザードの UI を定義します。

#### <a name="to-create-the-wizard-project"></a>ウィザードプロジェクトを作成するには

1. Visual Studio で、CustomActionProjectItem ソリューションを開きます。

2. **ソリューションエクスプローラー**で、ソリューションノードのショートカットメニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

3. **[新しいプロジェクト]** ダイアログボックスで、  **C#ビジュアル**または**Visual Basic**ノードを展開し、 **[Windows]** ノードを選択します。

4. **[新しいプロジェクト]** ダイアログボックスの上部で、.NET Framework のバージョンの一覧で **.NET Framework 4.5**が選択されていることを確認します。

5. **[WPF ユーザーコントロールライブラリ]** プロジェクトテンプレートを選択し、プロジェクトの**itemtemplatewizard**という名前を指定して、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **Itemtemplatewizard**プロジェクトをソリューションに追加します。

6. プロジェクトから UserControl1 項目を削除します。

## <a name="configure-the-wizard-project"></a>ウィザードプロジェクトの構成
 ウィザードを作成する前に、Windows Presentation Foundation (WPF) ウィンドウ、コードファイル、およびアセンブリ参照をプロジェクトに追加する必要があります。

#### <a name="to-configure-the-wizard-project"></a>ウィザード プロジェクトを構成するには

1. **ソリューションエクスプローラー**で、 **itemtemplatewizard**プロジェクトノードからショートカットメニューを開き、 **[プロパティ]** を選択します。

2. **プロジェクトデザイナー**で、ターゲットフレームワークが .NET Framework 4.5 に設定されていることを確認します。

     ビジュアルC#プロジェクトの場合は、 **[アプリケーション]** タブでこの値を設定できます。Visual Basic プロジェクトの場合は、 **[コンパイル]** タブでこの値を設定できます。詳細については、「[方法: .NET Framework のバージョンをターゲット](../ide/visual-studio-multi-targeting-overview.md)にする」を参照してください。

3. **Itemtemplatewizard**プロジェクトで、**ウィンドウ (WPF)** 項目をプロジェクトに追加し、その項目に**wizardwindow**という名前を指定します。

4. CustomActionWizard と String という名前の2つのコードファイルを追加します。

5. **Itemtemplatewizard**プロジェクトのショートカットメニューを開き、[参照の**追加**] を選択します。

6. **[参照マネージャー-ItemTemplateWizard]** ダイアログボックスの **[アセンブリ]** ノードで、 **[拡張機能]** ノードを選択します。

7. 次のアセンブリの横にあるチェックボックスをオンにし、 **[OK]** をクリックします。

    - EnvDTE

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

8. **ソリューションエクスプローラー**の ItemTemplateWizard プロジェクトの **[参照]** フォルダーで、 **EnvDTE**参照を選択します。

9. **[プロパティ]** ウィンドウで、 **[相互運用機能型の埋め込み]** プロパティの値を**False**に変更します。

## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>カスタムアクションの既定の場所と ID 文字列を定義する
 すべてのカスタムアクションには、`GroupID` で指定された場所と ID と、 *Elements .xml*ファイル内の `CustomAction` 要素の `Location` 属性があります。 この手順では、ItemTemplateWizard プロジェクトでこれらの属性の有効な文字列をいくつか定義します。 このチュートリアルを完了すると、ユーザーがウィザードで場所と ID を指定したときに、これらの文字列がカスタム動作プロジェクト項目の*Elements .xml*ファイルに書き込まれます。

 わかりやすくするために、このサンプルでは、使用可能な既定の場所と Id のサブセットのみをサポートしています。 完全な一覧については、「[既定のカスタムアクションの場所と id](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))」を参照してください。

#### <a name="to-define-the-default-location-and-id-strings"></a>既定の場所と ID 文字列を定義するには

1. 開き.

2. **Itemtemplatewizard**プロジェクトで、文字列コードファイル内のコードを次のコードに置き換えます。

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs#6)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb#6)]

## <a name="create-the-wizard-ui"></a>ウィザード UI を作成する
 ウィザードの UI を定義する XAML を追加し、ウィザードの一部のコントロールを ID 文字列にバインドするコードをいくつか追加します。 作成するウィザードは、Visual Studio の SharePoint プロジェクト用の組み込みウィザードに似ています。

#### <a name="to-create-the-wizard-ui"></a>ウィザードの UI を作成するには

1. **Itemtemplatewizard**プロジェクトで、 **wizardwindow .xaml**ファイルのショートカットメニューを開き、 **[開く]** をクリックしてデザイナーでウィンドウを開きます。

2. XAML ビューで、現在の XAML を次の XAML に置き換えます。 XAML は、見出し、カスタムアクションの動作を指定するコントロール、およびウィンドウの下部にあるナビゲーションボタンを含む UI を定義します。

    > [!NOTE]
    > このコードを追加すると、プロジェクトにコンパイルエラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

     [!code-xml[SPExtensibility.ProjectItem.CustomAction#9](../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml#9)]

    > [!NOTE]
    > この XAML で作成されるウィンドウは、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基底クラスから派生します。 カスタム WPF ダイアログボックスを Visual Studio に追加する場合は、Visual Studio の他のダイアログボックスとの一貫性のあるスタイルを持つように、このクラスからダイアログボックスを派生させ、モーダルダイアログボックスで発生する可能性のある問題を回避することをお勧めします。 詳細については、「[モーダルダイアログボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

3. Visual Basic プロジェクトを開発している場合は、`Window` 要素の `x:Class` 属性の `WizardWindow` クラス名から `ItemTemplateWizard` 名前空間を削除します。 この要素は XAML の 1 行目にあります。 完了すると、最初の行は次のコードのようになります。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. WizardWindow .xaml ファイルの分離コードファイルで、現在のコードを次のコードに置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs#7)]

## <a name="implement-the-wizard"></a>ウィザードを実装する
 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装して、ウィザードの機能を定義します。

#### <a name="to-implement-the-wizard"></a>ウィザードを実装するには

1. **Itemtemplatewizard**プロジェクトで、 **CustomActionWizard**コードファイルを開き、このファイルの現在のコードを次のコードに置き換えます。

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs#8)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb#8)]

## <a name="checkpoint"></a>チェックポイント
 この段階で、ウィザードに必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、プロジェクトをビルドして確認してください。

#### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="associate-the-wizard-with-the-item-template"></a>ウィザードを項目テンプレートに関連付ける
 ウィザードの実装が完了したので、次の3つの主要な手順を実行して、このウィザードを**カスタムアクション**項目テンプレートに関連付ける必要があります。

1. ウィザード アセンブリに厳密な名前で署名します。

2. ウィザード アセンブリの公開キー トークンを取得します。

3. **カスタムアクション**項目テンプレートの .vstemplate ファイルに、ウィザードアセンブリへの参照を追加します。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>ウィザード アセンブリに厳密な名前で署名するには

1. **ソリューションエクスプローラー**で、 **itemtemplatewizard**プロジェクトノードからショートカットメニューを開き、 **[プロパティ]** を選択します。

2. **[署名]** タブで、 **[アセンブリの署名]** チェックボックスをオンにします。

3. [**厳密な名前のキーファイルを選択**してください] ボックスの一覧の [ **\<新規作成] を選択します。>** 。

4. **[厳密な名前キーの作成]** ダイアログボックスで、名前を入力し、 **[キーファイルをパスワードで保護]** する チェックボックスをオフにして、 **[OK]** をクリックします。

5. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>ウィザード アセンブリの公開キー トークンを取得するには

1. Visual Studio のコマンドプロンプトウィンドウで、次のコマンドを実行します。 *PathToWizardAssembly*は、開発用コンピューターの itemtemplatewizard プロジェクトのビルドされた itemtemplatewizard .dll アセンブリへの完全パスに置き換えます。

    ```xml
    sn.exe -T PathToWizardAssembly
    ```

     *Itemtemplatewizard .dll*アセンブリの公開キートークンは、Visual Studio の [コマンドプロンプト] ウィンドウに書き込まれます。

2. Visual Studio コマンド プロンプト ウィンドウは開いたままにします。 次の手順を完了するには、公開キートークンが必要です。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>.vstemplate ファイルにウィザード アセンブリへの参照を追加するには

1. **ソリューションエクスプローラー**で、 **[itemtemplate]** プロジェクトノードを展開し、 *itemtemplate .vstemplate*ファイルを開きます。

2. ファイルの末尾の近くで、次の `WizardExtension` 要素を `</TemplateContent>` タグと `</VSTemplate>` タグの間に追加します。 `PublicKeyToken` 属性の自分の*トークン*値を、前の手順で取得した公開キートークンに置き換えます。

    ```xml
    <WizardExtension>
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>
    </WizardExtension>
    ```

     `WizardExtension` 要素の詳細については、「 [WizardExtension &#40;Element Visual Studio&#41;Templates](../extensibility/wizardextension-element-visual-studio-templates.md)」を参照してください。

3. ファイルを保存して閉じます。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>置換可能なパラメーターを項目テンプレートの*Elements .xml*ファイルに追加する
 ItemTemplate プロジェクトの*Elements .xml*ファイルに置き換え可能なパラメーターをいくつか追加します。 これらのパラメーターは、前に定義した `PopulateReplacementDictionary` クラスの `CustomActionWizard` メソッドで初期化されます。 ユーザーがカスタム動作プロジェクト項目をプロジェクトに追加すると、Visual Studio によって、新しいプロジェクト項目の*Elements .xml*ファイル内のこれらのパラメーターが、ウィザードで指定した値に自動的に置き換えられます。

 置き換え可能パラメーターはトークンであり、先頭と末尾にはドル記号 ($) が付いています。 独自の置換可能なパラメーターを定義するだけでなく、SharePoint プロジェクトシステムで定義および初期化する組み込みパラメーターを使用することもできます。 詳細については、「[置換可能なパラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>置き換え可能パラメーターを*Elements .xml*ファイルに追加するには

1. ItemTemplate プロジェクトで、 *Elements .xml*ファイルの内容を次の xml に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="$IdValue$"
                    GroupId="$GroupIdValue$"
                    Location="$LocationValue$"
                    Sequence="1000"
                    Title="$TitleValue$"
                    Description="$DescriptionValue$" >
        <UrlAction Url="$UrlValue$"/>
      </CustomAction>
    </Elements>
    ```

     新しい XML により、`Id`、`GroupId`、`Location`、`Description`、および `Url` 属性の値が置換可能なパラメーターに変更されます。

2. ファイルを保存して閉じます。

## <a name="add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加する
 VSIX プロジェクトの source.extension.vsixmanifest ファイルで、ウィザードプロジェクトへの参照を追加して、プロジェクト項目が含まれている VSIX パッケージと共に配置されるようにします。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加するには

1. **ソリューションエクスプローラー**で、CustomActionProjectItem プロジェクトの**source.extension.vsixmanifest**ファイルからショートカットメニューを開き、 **[開く]** をクリックして、マニフェストエディターでファイルを開きます。

2. マニフェストエディターで **[アセット]** タブを選択し、 **[新規作成]** をクリックします。

     **[新しい資産の追加]** ダイアログボックスが表示されます。

3. **[種類]** ボックスの一覧で、 **[VisualStudio]** を選択します。

4. **[ソース]** ボックスの一覧で、**現在のソリューション内のプロジェクト**を選択します。

5. **[プロジェクト]** ボックスの一覧で **[itemtemplatewizard]** を選択し、 **[OK]** をクリックします。

6. メニューバーで [**ビルド** > **ビルド**] を選択し、ソリューションがエラーなしでコンパイルされることを確認します。

## <a name="test-the-wizard"></a>ウィザードをテストする
 これで、ウィザードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで CustomActionProjectItem ソリューションのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで、SharePoint プロジェクトのカスタムアクションプロジェクト項目のウィザードをテストします。 最後に、SharePoint プロジェクトをビルドして実行し、カスタム動作が正常に機能することを確認します。

#### <a name="to-start-to-debug-the-solution"></a>ソリューションのデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、CustomActionProjectItem ソリューションを開きます。

2. ItemTemplateWizard プロジェクトで、CustomActionWizard コードファイルを開き、`RunStarted` メソッドのコードの最初の行にブレークポイントを追加します。

3. メニューバーで、 **[デバッグ]**  >  **[例外]** の順に選択します。

4. **[例外]** ダイアログボックスで、**共通言語ランタイムの例外**の**スロー**されたチェックボックスと**ユーザーが処理しない**チェックボックスがオフになっていることを確認し、 **[OK]** をクリックします。

5. F5 キーを**押す**か、メニューバーで **[デバッグ]** 、[デバッグ > **開始**] の順に選択して、デバッグを開始します。

     Visual Studio によって%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Action プロジェクト Item/1.0 に拡張機能がインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-wizard-in-visual-studio"></a>Visual Studio でウィザードをテストするには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ファイル** > **新しい** > **プロジェクト**] を選択します。

2. **ビジュアルC#** または**Visual Basic**ノードを展開します (項目テンプレートでサポートされている言語によって異なります)。 **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. プロジェクトテンプレートの一覧で **[SharePoint 2010 プロジェクト]** を選択し、プロジェクトに**CustomActionWizardTest**という名前を指定して、 **[OK]** をクリックします。

4. **SharePoint カスタマイズウィザード**で、デバッグに使用するサイトの URL を入力し、 **[完了]** をクリックします。

5. **ソリューションエクスプローラー**で、プロジェクトノードのショートカットメニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

6. **[新しい項目の追加-CustomItemWizardTest]** ダイアログボックスで、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを展開します。

7. プロジェクト項目の一覧で、 **[カスタム動作]** 項目を選択し、 **[追加]** をクリックします。

8. Visual Studio のもう一方のインスタンスで、先ほど `RunStarted` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

9. F5 キーを**押す**か、メニューバーで [**デバッグ** > **続行**] を選択して、プロジェクトのデバッグを続けます。

     SharePoint カスタマイズウィザードが表示されます。

10. **[場所]** で、 **[リストの編集]** オプションボタンを選択します。

11. **[グループ ID]** ボックスの一覧で、 **[通信]** を選択します。

12. **[タイトル]** ボックスに「 **SharePoint デベロッパーセンター**」と入力します。

13. **[説明]** ボックスに「」と入力すると、 **SharePoint デベロッパーセンターの Web サイトが開き**ます。

14. **[URL]** ボックスに「 **https://docs.microsoft.com/sharepoint/dev/** 」と入力し、 **[完了]** をクリックします。

     Visual Studio によって、 **[customaction1]** という名前の項目がプロジェクトに追加され、エディターで*要素 .xml*ファイルが開きます。 ウィザードで指定した値が*要素 .xml*に含まれていることを確認します。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>SharePoint のカスタム動作をテストするには

1. Visual Studio の実験用インスタンスで、F5 キーを**押す**か、メニューバーで **[デバッグ]** 、[**デバッグ > 開始**] の順に選択します。

     カスタムアクションがパッケージ化され、プロジェクトの **[サイト URL]** プロパティで指定された SharePoint サイトに配置されます。 web ブラウザーが開き、このサイトの既定のページが表示されます。

    > [!NOTE]
    > **[スクリプトデバッグを無効]** にする ダイアログボックスが表示されたら、 **[はい]** をクリックします。

2. SharePoint サイトの リスト 領域で、**タスク** リンクを選択します。

     **[タスク-すべてのタスク]** ページが表示されます。

3. リボンの **[リストツール]** タブで、 **[リスト]** タブを選択し、 **[設定]** グループで **[リストの設定]** を選択します。

     **[リストの設定]** ページが表示されます。

4. ページの上部付近にある **[通信]** 見出しの下にある **[SharePoint デベロッパーセンター]** リンクを選択し、ブラウザーが web サイト https://docs.microsoft.com/sharepoint/dev/ を開いてブラウザーを閉じていることを確認します。

## <a name="cleaning-up-the-development-computer"></a>開発用コンピューターのクリーンアップ
 プロジェクト項目のテストが終わったら、プロジェクト項目テンプレートを Visual Studio の実験用インスタンスから削除します。

#### <a name="to-clean-up-the-development-computer"></a>開発コンピューターをクリーンアップするには

1. Visual Studio の実験用インスタンスのメニューバーで、 **[ツール]** [ > の**拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、**カスタム動作プロジェクト項目**の拡張機能を選択し、 **[アンインストール]** をクリックします。

3. 表示されるダイアログボックスで、 **[はい]** をクリックして拡張機能をアンインストールすることを確認し、 **[今すぐ再起動]** ボタンをクリックしてアンインストールを完了します。

4. Visual Studio の両方のインスタンス (実験用インスタンスと、CustomActionProjectItem ソリューションが開いている Visual Studio のインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [方法: プロジェクト テンプレートでウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
- [既定のカスタム動作の場所と Id](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))
