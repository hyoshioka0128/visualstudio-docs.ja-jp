---
title: プロジェクトのプロパティを取得する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d0557d08c318eda47853ec69c6204739cbece560
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204325"
---
# <a name="getting-project-properties"></a>プロジェクト プロパティの取得
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、ツールウィンドウでプロジェクトのプロパティを表示する方法について説明します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>VSIX プロジェクトを作成してツールウィンドウを追加するには  
  
1. すべての Visual Studio 拡張機能は、拡張機能アセットを含む VSIX デプロイプロジェクトから開始されます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]という名前の VSIX プロジェクトを作成 `ProjectPropertiesExtension` します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. という名前のカスタムツールウィンドウ項目テンプレートを追加して、ツールウィンドウを追加し `ProjectPropertiesToolWindow` ます。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加] ダイアログ**で、[ **Visual C# の項目/機能拡張** ] にアクセスし、[ **カスタムツールウィンドウ**] を選択します。 ダイアログの下部にある [ **名前** ] フィールドで、ファイル名をに変更 `ProjectPropertiesToolWindow.cs` します。 カスタムツールウィンドウを作成する方法の詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。  
  
3. ソリューションをビルドし、エラーが発生することなくソリューションがコンパイルされることを確認します。  
  
### <a name="to-display-project-properties-in-a-tool-window"></a>ツールウィンドウにプロジェクトのプロパティを表示するには  
  
1. ProjectPropertiesToolWindowCommand.cs ファイルで、次の using ステートメントを追加します。  
  
    ```csharp  
    using EnvDTE;  
    using System.Windows.Controls;  
  
    ```  
  
2. ProjectPropertiesToolWindowControl で、既存のボタンを削除し、ツールボックスから TreeView を追加します。 また、ProjectPropertiesToolWindowControl.xaml.cs ファイルから click イベントハンドラーを削除することもできます。  
  
3. ProjectPropertiesToolWindowCommand.cs で、ShowToolWindow () メソッドを使用してプロジェクトを開き、そのプロパティを読み取り、プロパティを TreeView に追加します。 ShowToolWindow のコードは次のようになります。  
  
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
  
5. 実験用インスタンスでプロジェクトを開きます。  
  
6. **ビューまたはその他のウィンドウ**で、[ **ProjectPropertiesToolWindow**] をクリックします。  
  
     ツールウィンドウにツリーコントロールが表示され、最初のプロジェクトとそのすべてのプロジェクトプロパティの名前が表示されます。
