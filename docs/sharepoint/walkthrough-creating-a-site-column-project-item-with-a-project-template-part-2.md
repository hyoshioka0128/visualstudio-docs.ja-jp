---
title: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (第2部)
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
ms.openlocfilehash: c3b2fc34807be6ae03fe5aacab64439c918a0f5e
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189138"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (第2部)
  SharePoint プロジェクト項目のカスタム種類を定義し、Visual Studio でその種類をプロジェクト テンプレートと関連付けてから、テンプレート用のウィザードを用意することもできます。 ウィザードを使用すると、ユーザーがテンプレートを使用してプロジェクト項目を含む新しいプロジェクトを作成するときに、ユーザーから情報を収集できます。 収集した情報を使用して、プロジェクト項目を初期化できます。

 このチュートリアルでは、「[チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」で説明されている [サイト列] プロジェクトテンプレートにウィザードを追加します。 ユーザーがサイト列プロジェクトを作成すると、ウィザードはサイトの列 (基本型やグループなど) に関する情報を収集し、この情報を新しいプロジェクトの*要素 .xml*ファイルに追加します。

 このチュートリアルでは、次のタスクについて説明します。

- プロジェクト テンプレートに関連付けるカスタム SharePoint プロジェクト項目の種類に対するウィザードを作成します。

- Visual Studio の SharePoint プロジェクト用の組み込みウィザードと似たカスタム ウィザードの UI を定義します。

- ウィザードの実行中にローカル SharePoint サイトを呼び出すために使用される2つの*sharepoint コマンド*を作成する。 SharePoint コマンドは、SharePoint サーバー オブジェクト モデルの API を呼び出すために Visual Studio 拡張機能で使用できるメソッドです。 詳細については、「 [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

- 置き換え可能パラメーターを使用して、ウィザードで収集したデータで SharePoint プロジェクト ファイルを初期化します。

- 新しい各 Site Column プロジェクト インスタンスで新しい .snk ファイルを作成します。 このファイルを使用してプロジェクトの出力に署名し、SharePoint ソリューション アセンブリをグローバル アセンブリ キャッシュに配置できるようにします。

- ウィザードをデバッグおよびテストします。

> [!NOTE]
> 一連のサンプルワークフローについては、「 [SharePoint workflow samples](/sharepoint/dev/general-development/sharepoint-workflow-samples)」を参照してください。

## <a name="prerequisites"></a>必要条件
 このチュートリアルを実行するには、まず「[チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)」](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)を完了して、SiteColumnProjectItem ソリューションを作成する必要があります。

 また、このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、SDK の**Vsix プロジェクト**テンプレートを使用して、プロジェクト項目を配置する vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- Visual Studio のプロジェクトおよび項目テンプレート用のウィザード。 詳細については、「[方法: プロジェクトテンプレート](../extensibility/how-to-use-wizards-with-project-templates.md)と <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを使用してウィザードを使用する」を参照してください。

- SharePoint のサイト内の列。 詳細については、「[列](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))」を参照してください。

## <a name="understand-the-wizard-components"></a>ウィザードのコンポーネントについて
 このチュートリアルで説明されているウィザードには、いくつかのコンポーネントが含まれています。 次の表は、これらのコンポーネントについての説明です。

|コンポーネント|説明|
|---------------|-----------------|
|ウィザード実装|これは `SiteColumnProjectWizard` という名前のクラスであり、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装します。 このインターフェイスは、ウィザードの起動および終了時と、ウィザードの実行中の特定のタイミングで Visual Studio によって呼び出されるメソッドを定義します。|
|ウィザード UI|これは、`WizardWindow` という名前の WPF ベースのウィンドウです。 このウィンドウには、`Page1` および `Page2` という名前の 2 つのユーザー コントロールが含まれます。 これらのユーザー コントロールは、ウィザードの 2 つのページを表します。<br /><br /> このチュートリアルでは、ウィザード実装の <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> メソッドによって、ウィザード UI が表示されます。|
|ウィザード データ モデル|これは、`SiteColumnWizardModel` という名前の中間クラスであり、ウィザード UI とウィザード実装の間のレイヤーを提供します。 このサンプルでは、このクラスを使用して、ウィザード実装とウィザード UI を互いに抽象化できるようにします。このクラスは、すべてのウィザードで必須コンポーネントとなるわけではありません。<br /><br /> このチュートリアルでは、ウィザード UI が表示されるときに、ウィザード実装によって、ウィザード ウィンドウに `SiteColumnWizardModel` オブジェクトが渡されます。 ウィザード UI は、このオブジェクトのメソッドを使用して UI にコントロールの値を保存し、入力されたサイト URL が有効であることの確認などのタスクを実行します。 ユーザーがウィザードを終了すると、ウィザード実装は `SiteColumnWizardModel` オブジェクトを使用して、UI の最終的な状態を判断します。|
|プロジェクト署名マネージャー|これは、`ProjectSigningManager` という名前のヘルパー クラスであり、新しい各プロジェクト インスタンスで新しい key.snk ファイルを作成するためにウィザード実装によって使用されます。|
|SharePoint コマンド|これらは、ウィザードの実行中にローカル SharePoint サイトへの呼び出しを行うためにウィザード データ モデルによって使用されるメソッドです。 SharePoint コマンドは .NET Framework 3.5 をターゲットとする必要があるため、これらのコマンドは他のウィザード コードとは異なるアセンブリに実装されます。|

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、「[チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (パート 1:)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)」で作成した SiteColumnProjectItem ソリューションにいくつかのプロジェクトを追加する必要があります。

- WPF プロジェクト。 このプロジェクトで、<xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装し、ウィザードの UI を定義します。

- SharePoint コマンドを定義するクラス ライブラリ プロジェクト。 このプロジェクトは .NET Framework 3.5 を対象にする必要があります。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-wpf-project"></a>WPF プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で、SiteColumnProjectItem ソリューションを開きます。

2. **ソリューションエクスプローラー**で、 **SiteColumnProjectItem**ソリューションノードのショートカットメニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

3. **[新しいプロジェクトの追加]** ダイアログボックスの上部で、.NET Framework のバージョンの一覧で **.NET Framework 4.5**が選択されていることを確認します。

4. **C#ビジュアル**ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードを選択します。

5. プロジェクトテンプレートの一覧で **[WPF ユーザーコントロールライブラリ]** を選択し、プロジェクトに**projecttemplatewizard**という名前を指定して、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]、 **Projecttemplatewizard**プロジェクトをソリューションに追加し、既定の UserControl1 ファイルを開きます。

6. UserControl1.xaml ファイルをプロジェクトから削除します。

#### <a name="to-create-the-sharepoint-commands-project"></a>SharePoint コマンド プロジェクトを作成するには

1. **ソリューションエクスプローラー**で、SiteColumnProjectItem ソリューションノードのショートカットメニューを開き、 **[追加]** 、 **[新しいプロジェクト]** の順に選択します。

2. **[新しいプロジェクトの追加]** ダイアログボックスの上部にある .NET Framework のバージョンの一覧で **[.NET Framework 3.5]** を選択します。

3. **C#ビジュアル**ノードまたは **[Visual Basic]** ノードを展開し、 **[Windows]** ノードを選択します。

4. **[クラスライブラリ]** プロジェクトテンプレートを選択し、プロジェクトに**sharepointcommands**という名前を指定して、 **[OK]** をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、 **Sharepointcommands**プロジェクトがソリューションに追加され、既定の Class1 コードファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-projects"></a>プロジェクトを構成する
 ウィザードを作成する前に、いくつかのコード ファイルとアセンブリ参照をプロジェクトに追加する必要があります。

#### <a name="to-configure-the-wizard-project"></a>ウィザード プロジェクトを構成するには

1. **ソリューションエクスプローラー**で、 **projecttemplatewizard**プロジェクトノードのショートカットメニューを開き、 **[プロパティ]** を選択します。

2. **プロジェクトデザイナー**で、Visual Basic プロジェクトのビジュアルC#プロジェクトまたは **コンパイル** タブの アプリケーション タブを選択します。

3. ターゲット フレームワークが .NET Framework 4.5 Client Profile ではなく .NET Framework 4.5 に設定されていることを確認します。

     詳細については、「[方法: .NET Framework のバージョンをターゲットにする](../ide/visual-studio-multi-targeting-overview.md)」を参照してください。

4. **Projecttemplatewizard**プロジェクトのショートカットメニューを開き、 **[追加]** 、 **[新しい項目]** の順に選択します。

5. [**ウィンドウ (WPF)]** 項目を選択し、[アイテム**ウィザード] ウィンドウ**に名前を指定して、 **[追加]** ボタンをクリックします。

6. 2つの**ユーザーコントロール (WPF)** 項目をプロジェクトに追加し、 **Page1**と**Page2**という名前を指定します。

7. 次の名前で 4 つのコード ファイルをプロジェクトに追加します。

    - SiteColumnProjectWizard

    - SiteColumnWizardModel

    - ProjectSigningManager

    - CommandIds

8. **Projecttemplatewizard**プロジェクトノードのショートカットメニューを開き、[参照の**追加**] を選択します。

9. **[アセンブリ]** ノードを展開し、 **[拡張機能]** ノードを選択して、次のアセンブリの横にあるチェックボックスをオンにします。

    - EnvDTE

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.Shell.Interop.10.0

    - Microsoft.VisualStudio.Shell.Interop.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

10. **[OK** ] をクリックして、アセンブリをプロジェクトに追加します。

11. **ソリューションエクスプローラー**で、 **projecttemplatewizard**プロジェクトの **[参照]** フォルダーの下にある **[EnvDTE]** を選択します。

12. **[プロパティ]** ウィンドウで、 **[相互運用機能型の埋め込み]** プロパティの値を**False**に変更します。

13. Visual Basic プロジェクトを開発している場合は、プロジェクト**デザイナー**を使用して、プロジェクトに ProjectTemplateWizard 名前空間をインポートします。

     詳細については、「[方法: インポートされた&#40;名前&#41;空間を追加または削除する Visual Basic](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)」を参照してください。

#### <a name="to-configure-the-sharepointcommands-project"></a>SharePointcommands プロジェクトを構成するには

1. **ソリューションエクスプローラー**で、 **[sharepointcommands]** プロジェクトノードを選択します。

2. メニューバーで、 **[プロジェクト]** 、 **[既存項目の追加]** の順に選択します。

3. **[既存項目の追加]** ダイアログボックスで、ProjectTemplateWizard プロジェクトのコードファイルが格納されているフォルダーを参照し、次**に、そのコードファイル**を選択します。

4. **[追加]** ボタンの横にある矢印をクリックし、表示されるメニューの **[リンクとして追加]** オプションを選択します。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] により、コードファイルが**Sharepointcommands**プロジェクトにリンクとして追加されます。 コードファイルは**Projecttemplatewizard**プロジェクトにありますが、ファイル内のコードは**sharepointcommands**プロジェクトでもコンパイルされます。

5. **Sharepointcommands**プロジェクトで、Commands という名前の別のコードファイルを追加します。

6. SharePointCommands プロジェクトを選択し、メニューバーで **[プロジェクト]** を選択し >  **[参照の追加]** をクリックします。

7. **[アセンブリ]** ノードを展開し、 **[拡張機能]** ノードを選択して、次のアセンブリの横にあるチェックボックスをオンにします。

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

8. **[OK** ] をクリックして、アセンブリをプロジェクトに追加します。

## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>ウィザードモデル、署名マネージャー、および SharePoint コマンド Id の作成
 ProjectTemplateWizard プロジェクトにコードを追加して、サンプルの次のコンポーネントを実装します。

- SharePoint コマンド ID。 これらは、ウィザードによって使用される SharePoint コマンドを識別する文字列です。 このチュートリアルの後半で、SharePointCommands プロジェクトにコードを追加してコマンドを実装します。

- ウィザード データ モデル。

- プロジェクト署名マネージャー。

  これらのコンポーネントの詳細については、「[ウィザードのコンポーネント](#understand-the-wizard-components)について」を参照してください。

#### <a name="to-define-the-sharepoint-command-ids"></a>SharePoint コマンド ID を定義するには

1. ProjectTemplateWizard プロジェクトで、CommandIds コード ファイルを開き、このファイルの内容全体を次のコードに置き換えます。

     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs#5)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb#5)]

#### <a name="to-create-the-wizard-model"></a>ウィザード モデルを作成するには

1. SiteColumnWizardModel コード ファイルを開き、このファイルの内容全体を次のコードに置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb#6)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs#6)]

#### <a name="to-create-the-project-signing-manager"></a>プロジェクト署名マネージャーを作成するには

1. ProjectSigningManager コード ファイルを開き、このファイルの内容全体を次のコードに置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb#8)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs#8)]

## <a name="create-the-wizard-ui"></a>ウィザード UI を作成する
 ウィザード ウィンドウの UI と、ウィザード ページの UI を提供する 2 つのユーザー コントロールを定義する XAML を追加し、ウィンドウとユーザー コントロールの動作を定義するコードを追加します。 作成するウィザードは、Visual Studio の SharePoint プロジェクト用の組み込みウィザードに似ています。

> [!NOTE]
> 以降の手順では、プロジェクトに XAML またはコードを追加した後で、いくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

#### <a name="to-create-the-wizard-window-ui"></a>ウィザード ウィンドウの UI を作成するには

1. ProjectTemplateWizard プロジェクトで、WizardWindow .xaml ファイルのショートカットメニューを開き、 **[開く]** をクリックしてデザイナーでウィンドウを開きます。

2. デザイナーの XAML ビューで、現在の XAML を次の XAML に置き換えます。 この XAML は、見出しを含む UI、ウィザード ページが含まれる <xref:System.Windows.Controls.Grid>、およびウィンドウの下部に示されるナビゲーション ボタンを定義します。

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#10](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml#10)]

    > [!NOTE]
    > この XAML で作成されるウィンドウは、<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> 基底クラスから派生します。 カスタムの WPF ダイアログ ボックスを Visual Studio に追加する場合は、ダイアログ ボックスをこのクラスから派生し、スタイルを他の Visual Studio ダイアログ ボックスと一貫させ、発生する可能性のあるモーダル ダイアログの問題を回避することをお勧めします。 詳細については、「[モーダルダイアログボックスの作成と管理](../extensibility/creating-and-managing-modal-dialog-boxes.md)」を参照してください。

3. Visual Basic プロジェクトを開発している場合は、`Window` 要素の `x:Class` 属性の `WizardWindow` クラス名から `ProjectTemplateWizard` 名前空間を削除します。 この要素は XAML の 1 行目にあります。 完了すると、最初の行は次の例のようになります。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. WizardWindow.xaml ファイルの分離コード ファイルを開きます。

5. このファイルの内容を、ファイルの先頭の `using` 宣言を除いて、次のコードに置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb#4)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs#4)]

#### <a name="to-create-the-first-wizard-page-ui"></a>1 つ目のウィザード ページの UI を作成するには

1. ProjectTemplateWizard プロジェクトで、Page1 ファイルのショートカットメニューを開き、 **[開く]** をクリックしてデザイナーでユーザーコントロールを開きます。

2. デザイナーの XAML ビューで、現在の XAML を次の XAML に置き換えます。 この XAML で定義している UI には、ユーザーがデバッグに使用するローカル サイトの URL を入力できるテキスト ボックスが含まれます。 この UI には、ユーザーがプロジェクトをサンドボックス化するかどうかを指定できるオプション ボタンも含まれます。

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#11](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml#11)]

3. Visual Basic プロジェクトを開発している場合は、`ProjectTemplateWizard` 要素の `Page1` 属性の `x:Class` クラス名から `UserControl` 名前空間を削除します。 これは XAML の 1 行目にあります。 変更後の 1 行目は次のようになります。

    ```xml
    <UserControl x:Class="Page1"
    ```

4. Page1.xaml ファイルの内容を、ファイルの先頭にある `using` 宣言を除いて、次のコードに置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs#2)]

#### <a name="to-create-the-second-wizard-page-ui"></a>2 つ目のウィザード ページの UI を作成するには

1. ProjectTemplateWizard プロジェクトで、Page2 ファイルのショートカットメニューを開き、 **[開く]** を選択します。

     ユーザー コントロールがデザイナーで開きます。

2. XAML ビューで、現在の XAML を次の XAML に置き換えます。 この XAML は、サイト内の列の基本型を選択するためのドロップダウン リスト、ギャラリーでサイト内の列を表示する組み込みまたはカスタムのグループを指定するためのコンボ ボックス、およびサイト内の列の名前を指定するためのボックスが含まれる UI を定義します。

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#12](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml#12)]

3. Visual Basic プロジェクトを開発している場合は、`ProjectTemplateWizard` 要素の `Page2` 属性の `x:Class` クラス名から `UserControl` 名前空間を削除します。 これは XAML の 1 行目にあります。 変更後の 1 行目は次のようになります。

    ```xml
    <UserControl x:Class="Page2"
    ```

4. Page2.xaml ファイルの分離コード ファイルの内容を、ファイルの先頭にある `using` 宣言を除いて、次のコードに置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb#3)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs#3)]

## <a name="implement-the-wizard"></a>ウィザードを実装する
 <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> インターフェイスを実装することで、ウィザードの主要機能を定義します。 このインターフェイスは、ウィザードの起動および終了時と、ウィザードの実行中の特定のタイミングで Visual Studio によって呼び出されるメソッドを定義します。

#### <a name="to-implement-the-wizard"></a>ウィザードを実装するには

1. ProjectTemplateWizard プロジェクトで、SiteColumnProjectWizard コード ファイルを開きます。

2. このファイルの内容全体を次のコードで置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs#7)]

## <a name="create-the-sharepoint-commands"></a>SharePoint コマンドを作成する
 SharePoint サーバー オブジェクト モデルを呼び出す 2 つのカスタム コマンドを作成します。 一方のコマンドは、ウィザードでユーザーが入力するサイトの URL が有効かどうかを判断します。 もう一方のコマンドは、指定した SharePoint サイトからすべてのフィールドの型を取得して、ユーザーが新しいサイト内の列の基本として使用するフィールドの型を選択できるようにします。

#### <a name="to-define-the-sharepoint-commands"></a>SharePoint コマンドを定義するには

1. **Sharepointcommands**プロジェクトで、Commands コードファイルを開きます。

2. このファイルの内容全体を次のコードで置き換えます。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb#9)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs#9)]

## <a name="checkpoint"></a>チェックポイント
 この段階で、ウィザードに必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、プロジェクトをビルドして確認してください。

#### <a name="to-build-your-project"></a>プロジェクトをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="removing-the-keysnk-file-from-the-project-template"></a>プロジェクトテンプレートからのキー .snk ファイルの削除
 [「チュートリアル: プロジェクトテンプレートを使用してサイト列プロジェクト項目を作成する (パート 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md))」では、作成したプロジェクトテンプレートに、各サイト列プロジェクトインスタンスの署名に使用されるキー .snk ファイルが含まれています。 ウィザードでプロジェクトごとに新しい key.snk ファイルが生成されるようになったため、この key.snk ファイルはもう必要ありません。 プロジェクト テンプレートから key.snk ファイルを削除し、このファイルへの参照を削除します。

#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>プロジェクト テンプレートから key.snk ファイルを削除するには

1. **ソリューションエクスプローラー**の **[SiteColumnProjectTemplate]** ノードで、**キーの .snk**ファイルのショートカットメニューを開き、 **[削除]** を選択します。

2. 確認のダイアログボックスが表示されたら、 **[OK]** をクリックします。

3. **SiteColumnProjectTemplate**ノードの下で、SiteColumnProjectTemplate ファイルを開き、そこから次の要素を削除します。

    ```xml
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
    ```

4. ファイルを保存して閉じます。

5. **SiteColumnProjectTemplate**ノードの下で、projecttemplate .csproj ファイルまたは projecttemplate .vbproj ファイルを開き、そこから次の `PropertyGroup` 要素を削除します。

    ```xml
    <PropertyGroup>
      <SignAssembly>true</SignAssembly>
      <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
    </PropertyGroup>
    ```

6. 次の `None` 要素を削除します。

    ```xml
    <None Include="key.snk" />
    ```

7. ファイルを保存して閉じます。

## <a name="associating-the-wizard-with-the-project-template"></a>ウィザードとプロジェクトテンプレートの関連付け
 ウィザードの実装が完了したので、ウィザードを **[サイト列]** プロジェクトテンプレートに関連付ける必要があります。 これを行うために必要となる手順は次の 3 つです。

1. ウィザード アセンブリに厳密な名前で署名します。

2. ウィザード アセンブリの公開キー トークンを取得します。

3. **サイト列**プロジェクトテンプレートの .vstemplate ファイルに、ウィザードアセンブリへの参照を追加します。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>ウィザード アセンブリに厳密な名前で署名するには

1. **ソリューションエクスプローラー**で、 **projecttemplatewizard**プロジェクトのショートカットメニューを開き、 **[プロパティ]** を選択します。

2. **[署名]** タブで、 **[アセンブリの署名]** チェックボックスをオンにします。

3. [**厳密な名前のキーファイルを選択**してください] ボックスの一覧の [ **\<新規作成] を選択します。>** 。

4. **[厳密な名前キーの作成]** ダイアログボックスで、新しいキーファイルの名前を入力し、 **[キーファイルをパスワードで保護]** する チェックボックスをオフにして、 **[OK]** をクリックします。

5. **Projecttemplatewizard**プロジェクトのショートカットメニューを開き、 **[ビルド]** をクリックして、projecttemplatewizard .dll ファイルを作成します。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>ウィザード アセンブリの公開キー トークンを取得するには

1. [**スタート] ボタン**をクリックし、 **[すべてのプログラム]** 、 **[Microsoft Visual Studio]** 、 **[Visual Studio Tools]** 、 **[開発者コマンドプロンプト]** の順に選択します。

     Visual Studio コマンド プロンプト ウィンドウが開きます。

2. 次のコマンドを実行します。 *PathToWizardAssembly*は、開発用コンピューター上の projecttemplatewizard プロジェクトのビルドされた projecttemplatewizard .dll アセンブリへの完全パスに置き換えます。

    ```cmd
    sn.exe -T PathToWizardAssembly
    ```

     ProjectTemplateWizard.dll アセンブリに対する公開キー トークンが Visual Studio コマンド プロンプト ウィンドウに記述されます。

3. Visual Studio コマンド プロンプト ウィンドウは開いたままにします。 次の手順の間に、公開キー トークンが必要になります。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>.vstemplate ファイルにウィザード アセンブリへの参照を追加するには

1. **ソリューションエクスプローラー**で、 **SiteColumnProjectTemplate**プロジェクトノードを展開し、SiteColumnProjectTemplate ファイルを開きます。

2. ファイルの末尾の近くで、次の `WizardExtension` 要素を `</TemplateContent>` タグと `</VSTemplate>` タグの間に追加します。 `PublicKeyToken` 属性の*トークン*値を、前の手順で取得した公開キートークンに置き換えます。

    ```xml
    <WizardExtension>
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>
    </WizardExtension>
    ```

     `WizardExtension` 要素の詳細については、「 [WizardExtension &#40;Element Visual Studio&#41;Templates](../extensibility/wizardextension-element-visual-studio-templates.md)」を参照してください。

3. ファイルを保存して閉じます。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>置き換え可能パラメーターをプロジェクトテンプレートの Elements .xml ファイルに追加する
 SiteColumnProjectTemplate プロジェクトの*要素 .xml*ファイルに置き換え可能なパラメーターをいくつか追加します。 これらのパラメーターは、前に定義した `RunStarted` クラスの `SiteColumnProjectWizard` メソッドで初期化されます。 ユーザーがサイト列プロジェクトを作成すると、Visual Studio によって、新しいプロジェクトの*Elements .xml*ファイル内のこれらのパラメーターが、ウィザードで指定した値に自動的に置き換えられます。

 置き換え可能パラメーターはトークンであり、先頭と末尾にはドル記号 ($) が付いています。 独自の置き換え可能パラメーターを定義するだけでなく、SharePoint プロジェクト システムによって定義されて初期化される組み込みパラメーターを使用することもできます。 詳細については、「[置換可能なパラメーター](../sharepoint/replaceable-parameters.md)」を参照してください。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>置き換え可能パラメーターを Elements.xml ファイルに追加するには

1. SiteColumnProjectTemplate プロジェクトで、*要素 .xml*ファイルの内容を次の xml に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
             Name="$fieldname$"
             DisplayName="$fieldname$"
             Type="$selectedfieldtype$"
             Group="$selectedgrouptype$">
      </Field>
    </Elements>
    ```

     新しい XML では、`Name`、`DisplayName`、`Type`、`Group` の各属性の値がカスタムの置き換え可能パラメーターに変更されます。

2. ファイルを保存して閉じます。

## <a name="add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加する
 Site Column プロジェクト テンプレートが含まれる VSIX パッケージと共にウィザードを配置するには、ウィザード プロジェクトと SharePoint コマンド プロジェクトへの参照を VSIX プロジェクトの source.extension.vsixmanifest ファイルに追加します。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>VSIX パッケージにウィザードを追加するには

1. **ソリューションエクスプローラー**の**SiteColumnProjectItem**プロジェクトで、 **source.extension.vsixmanifest**ファイルのショートカットメニューを開き、 **[開く]** を選択します。

     Visual Studio によってマニフェスト エディターでファイルが開きます。

2. エディターの **[アセット]** タブで、 **[新規]** ボタンをクリックします。

     **[新しい資産の追加]** ダイアログボックスが表示されます。

3. **[種類]** ボックスの一覧で、 **[VisualStudio]** を選択します。

4. **[ソース]** ボックスの一覧で、**現在のソリューション内のプロジェクト**を選択します。

5. **[プロジェクト]** ボックスの一覧で **[projecttemplatewizard]** を選択し、 **[OK]** をクリックします。

6. エディターの **[アセット]** タブで、 **[新規]** ボタンをもう一度クリックします。

     **[新しい資産の追加]** ダイアログボックスが表示されます。

7. [種類] ボックスの一覧で、 **「** **SharePoint. コマンド. v4**」と入力します。

8. **[ソース]** ボックスの一覧で、**現在のソリューション内のプロジェクト**を選択します。

9. **[プロジェクト]** ボックスの一覧で **[sharepointcommands]** プロジェクトを選択し、 **[OK]** をクリックします。

10. メニューバーで [**ビルド** > **ビルド**] を選択し、ソリューションがエラーなしでビルドされることを確認します。

## <a name="test-the-wizard"></a>ウィザードをテストする
 これで、ウィザードをテストする準備ができました。 まず、Visual Studio の実験用インスタンスで SiteColumnProjectItem ソリューションのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで、Site Column プロジェクトのウィザードをテストします。 最後に、プロジェクトをビルドして実行し、サイト内の列が正常に機能することを確認します。

#### <a name="to-start-debugging-the-solution"></a>ソリューションのデバッグを開始するには

1. 管理者の資格情報で Visual Studio を再起動し、SiteColumnProjectItem ソリューションを開きます。

2. ProjectTemplateWizard プロジェクトで、SiteColumnProjectWizard コード ファイルを開き、`RunStarted` メソッド内のコードの 1 行目にブレークポイントを追加します。

3. メニューバーで、 **[デバッグ]**  >  **[例外]** の順に選択します。

4. **[例外]** ダイアログボックスで、**共通言語ランタイムの例外**の**スロー**されたチェックボックスと**ユーザーが処理しない**チェックボックスがオフになっていることを確認し、 **[OK]** をクリックします。

5. F5 キーを**押す**か、メニューバーで [ > **デバッグ**]、[デバッグの**開始**] の順に選択して、デバッグを開始します。

     Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-wizard-in-visual-studio"></a>Visual Studio でウィザードをテストするには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ファイル** > **新しい** > **プロジェクト**] を選択します。

2. **ビジュアルC#** ノードまたは **[Visual Basic]** ノードを展開します (プロジェクトテンプレートでサポートされている言語によって異なります)。次に、 **[SharePoint]** ノードを展開し、 **[2010]** ノードを選択します。

3. プロジェクトテンプレートの一覧で **[サイト列]** を選択し、プロジェクトに**SiteColumnWizardTest**という名前を指定して、 **[OK]** をクリックします。

4. Visual Studio のもう一方のインスタンスで、先ほど `RunStarted` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

5. F5 キーを**押す**か、メニューバーで [**デバッグ** > **続行**] を選択して、プロジェクトのデバッグを続けます。

6. **SharePoint カスタマイズウィザード**で、デバッグに使用するサイトの URL を入力し、 **[次へ]** をクリックします。

7. **SharePoint カスタマイズウィザード**の2ページ目で、次の選択を行います。

   - **[種類]** ボックスの一覧で **[ブール]** を選択します。

   - **[グループ]** ボックスの一覧で、[**カスタム]、[いいえ]、[列なし**] の順に選択します。

   - **[名前]** ボックスに **「My Yes/No Column**」と入力し、 **[完了]** をクリックします。

     **ソリューションエクスプローラー**に、新しいプロジェクトが表示され、 **Field1**という名前のプロジェクト項目が含まれます。 Visual Studio は、エディターでプロジェクトの*要素 .xml*ファイルを開きます。

8. ウィザードで指定した値が*要素 .xml*に含まれていることを確認します。

#### <a name="to-test-the-site-column-in-sharepoint"></a>SharePoint でサイト内の列をテストするには

1. Visual Studio の実験用インスタンスで、F5 キーを**押し**ます。

     サイト列がパッケージ化され、プロジェクトの **[サイト URL]** プロパティによって指定された SharePoint サイトに配置されます。 Web ブラウザーには、このサイトの既定のページが表示されます。

    > [!NOTE]
    > **[スクリプトデバッグを無効]** にする ダイアログボックスが表示された場合は、 **[はい]** をクリックしてプロジェクトのデバッグを続行します。

2. **[サイトの操作]** メニューで、 **[サイトの設定]** を選択します。

3. サイトの設定 ページの **ギャラリー** で、**サイト列** リンクを選択します。

4. サイト列の一覧で、 **[カスタムの yes/No columns]** グループに " **My Yes/no column**" という名前の列が含まれていることを確認し、web ブラウザーを閉じます。

## <a name="clean-up-the-development-computer"></a>開発用コンピューターのクリーンアップ
 プロジェクト項目のテストが終わったら、プロジェクト テンプレートを Visual Studio の実験用インスタンスから削除します。

#### <a name="to-clean-up-the-development-computer"></a>開発コンピューターをクリーンアップするには

1. Visual Studio の実験用インスタンスのメニューバーで、 **[ツール]** [ > の**拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で **[サイト列]** を選択し、 **[アンインストール]** をクリックします。

3. 表示されるダイアログボックスで、 **[はい]** をクリックして拡張機能をアンインストールすることを確認し、 **[今すぐ再起動]** ボタンをクリックしてアンインストールを完了します。

4. Visual Studio の実験用インスタンスと、CustomActionProjectItem ソリューションが開いているインスタンスの両方を閉じます。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 拡張機能をデプロイする方法の詳細については、「 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクト テンプレートの作成](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [方法: プロジェクト テンプレートでウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
