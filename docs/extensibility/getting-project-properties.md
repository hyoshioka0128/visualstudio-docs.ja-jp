---
title: プロジェクトプロパティの取得 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711407"
---
# <a name="get-project-properties"></a>プロジェクト プロパティの取得

このチュートリアルでは、ツール ウィンドウにプロジェクト プロパティを表示する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>VSIX プロジェクトを作成し、ツール ウィンドウを追加するには

1. すべての Visual Studio 拡張機能は、拡張機能の資産を含む VSIX 配置プロジェクトで開始します。 という名前[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]`ProjectPropertiesExtension`の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. という名前のカスタム ツール ウィンドウ項目テンプレートを追加して`ProjectPropertiesToolWindow`、ツール ウィンドウを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加**] ダイアログ で **、[Visual C# アイテム** > **の機能拡張**] に移動し、[**カスタム ツール ウィンドウ**] を選択します。 ダイアログの下部にある [**名前]** フィールドで、ファイル名を`ProjectPropertiesToolWindow.cs`に変更します。 カスタム ツール ウィンドウを作成する方法の詳細については、「[ツール ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。

3. ソリューションをビルドし、エラーが発生することなくソリューションがコンパイルされることを確認します。

### <a name="to-display-project-properties-in-a-tool-window"></a>ツール ウィンドウにプロジェクト プロパティを表示するには

1. ProjectPropertiesToolWindowCommand.cs ファイルに、次の using ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using System.Windows.Controls;

    ```

2. [*ツールボックス] から*既存のボタンを削除し、ツリー ビューを追加します。 ProjectPropertiesToolWindowControl.xaml.cs*ファイルから*クリック イベント ハンドラーを削除することもできます。

3. *ProjectPropertiesToolWindowCommand.cs*で、メソッドを`ShowToolWindow()`使用してプロジェクトを開き、そのプロパティを読み取り、プロパティを TreeView に追加します。 次のようなコードを表示します。

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

6. **[他のウィンドウ**の**表示** > ]**で、[プロジェクトのプロパティ] ツール ウィンドウをクリックします**。

  ツール ウィンドウにツリー コントロールが表示され、最初のプロジェクトとそのすべてのプロジェクト プロパティの名前が表示されます。
