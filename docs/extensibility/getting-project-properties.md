---
title: プロジェクトのプロパティを取得する |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ddfd48827bc762c9189f9b7600cfe9200e5c866
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80711407"
---
# <a name="get-project-properties"></a>プロジェクトのプロパティを取得する

このチュートリアルでは、ツールウィンドウでプロジェクトのプロパティを表示する方法について説明します。

## <a name="prerequisites"></a>前提条件

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>VSIX プロジェクトを作成してツールウィンドウを追加するには

1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]という名前の VSIX プロジェクトを作成 `ProjectPropertiesExtension` します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[ **新しいプロジェクト** ] ダイアログで見つけることができます。

2. という名前のカスタムツールウィンドウ項目テンプレートを追加して、ツールウィンドウを追加し `ProjectPropertiesToolWindow` ます。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加] ダイアログ**で、[ **Visual C# 項目**の機能拡張] にアクセスし、  >  **Extensibility** [**カスタムツールウィンドウ**] を選択します。 ダイアログの下部にある [ **名前** ] フィールドで、ファイル名をに変更 `ProjectPropertiesToolWindow.cs` します。 カスタムツールウィンドウを作成する方法の詳細については、「 [ツールウィンドウで拡張機能を作成](../extensibility/creating-an-extension-with-a-tool-window.md)する」を参照してください。

3. ソリューションをビルドし、エラーが発生することなくソリューションがコンパイルされることを確認します。

### <a name="to-display-project-properties-in-a-tool-window"></a>ツールウィンドウにプロジェクトのプロパティを表示するには

1. ProjectPropertiesToolWindowCommand.cs ファイルで、次の using ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using System.Windows.Controls;

    ```

2. *ProjectPropertiesToolWindowControl*で、既存のボタンを削除し、ツールボックスから TreeView を追加します。 また、 *ProjectPropertiesToolWindowControl.xaml.cs* ファイルから click イベントハンドラーを削除することもできます。

3. *ProjectPropertiesToolWindowCommand.cs*で、メソッドを使用して `ShowToolWindow()` プロジェクトを開き、そのプロパティを読み取り、プロパティを TreeView に追加します。 ShowToolWindow のコードは次のようになります。

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        ToolWindowPane window = this.package.FindToolWindow(typeof(ProjectPropertiesToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create window.");
        }
        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        // Get the tree view and populate it if there is a project open.
        ProjectPropertiesToolWindowControl control = (ProjectPropertiesToolWindowControl)window.Content;
        TreeView treeView = control.treeView;

        // Reset the TreeView to 0 items.
        treeView.Items.Clear();

        DTE dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));
        Projects projects = dte.Solution.Projects;
        if (projects.Count == 0)   // no project is open
        {
            TreeViewItem item = new TreeViewItem();
            item.Name = "Projects";
            item.ItemsSource = new string[]{ "no projects are open." };
            item.IsExpanded = true;
            treeView.Items.Add(item);
            return;
        }

        Project project = projects.Item(1);
        TreeViewItem item1 = new TreeViewItem();
        item1.Header = project.Name + "Properties";
        treeView.Items.Add(item1);

        foreach (Property property in project.Properties)
        {
            TreeViewItem item = new TreeViewItem();
            item.ItemsSource = new string[] { property.Name };
            item.IsExpanded = true;
            treeView.Items.Add(item);
        }
    }
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. この実験用インスタンスで、プロジェクトを開きます。

6. **View**  >  [**その他の**ビュー] ウィンドウで、[ **ProjectPropertiesToolWindow**] をクリックします。

  ツールウィンドウにツリーコントロールが表示され、最初のプロジェクトとそのすべてのプロジェクトプロパティの名前が表示されます。
