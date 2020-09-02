---
title: ユニバーサル Windows プロジェクトの管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08d88ce08c6c91cbf46bcc6d15cbf098d61e604d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65679927"
---
# <a name="managing-universal-windows-projects"></a>ユニバーサル Windows プロジェクトの管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユニバーサル Windows アプリは、Windows 8.1 と Windows Phone 8.1 の両方を対象とするアプリで、開発者は両方のプラットフォームでコードとその他の資産を使用できます。 共有コードとリソースは共有プロジェクトに保持されます。一方、プラットフォーム固有のコードとリソースは、Windows 用と Windows Phone 用の別々のプロジェクトに保持されます。 ユニバーサル Windows アプリの詳細については、「 [ユニバーサル Windows アプリ](https://msdn.microsoft.com/library/windows/apps/dn609832.aspx)」を参照してください。 プロジェクトを管理する Visual Studio 拡張機能では、ユニバーサル Windows アプリプロジェクトの構造が1つのプラットフォームアプリとは異なることに注意してください。 このチュートリアルでは、共有プロジェクト内を移動し、共有項目を管理する方法について説明します。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
### <a name="navigate-the-shared-project"></a>共有プロジェクト内を移動する  
  
1. **TestUniversalProject**という名前の C# VSIX プロジェクトを作成します。 ([**ファイル]、[新規作成]、[プロジェクト** ]、[ **C#]、[拡張機能]、[Visual Studio パッケージ]**)。 **カスタムコマンド**プロジェクト項目テンプレートを追加します (ソリューションエクスプローラーで、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択し、[**拡張機能**] にアクセスします)。 ファイルに **TestUniversalProject**という名前を指定します。  
  
2. Microsoft.VisualStudio.Shell.Interop.12.1.DesignTime.dll と Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll への参照を追加します (「 **Extensions** 」セクション)。  
  
3. TestUniversalProject.cs を開き、次のステートメントを追加し `using` ます。  
  
    ```csharp  
    using EnvDTE;  
    using EnvDTE80;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.PlatformUI;  
    using Microsoft.Internal.VisualStudio.PlatformUI;   
    using System.Collections.Generic;   
    using System.IO;  
    using System.Windows.Forms;  
    ```  
  
4. TestUniversalProject クラスで、 **出力** ウィンドウを指すプライベートフィールドを追加します。  
  
    ```csharp  
    public sealed class TestUniversalProject   
    {  
        IVsOutputWindowPane output;  
    . . .  
    }  
    ```  
  
5. TestUniversalProject コンストラクター内の出力ペインへの参照を設定します。  
  
    ```csharp  
    private TestUniversalProject(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException("package");  
        }  
  
        this.package = package;  
  
        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
            EventHandler eventHandler = this.ShowMessageBox;  
            MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);  
            commandService.AddCommand(menuItem);  
        }  
        // get a reference to the Output window  
                    output = (IVsOutputWindowPane)ServiceProvider.GetService(typeof(SVsGeneralOutputWindowPane));  
    }  
    ```  
  
6. メソッドから既存のコードを削除し `ShowMessageBox` ます。  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)   
    {  
    }  
    ```  
  
7. このチュートリアルでいくつかの目的で使用する DTE オブジェクトを取得します。 また、メニューボタンがクリックされたときに、ソリューションが読み込まれることを確認してください。  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {   
        var dte = (EnvDTE.DTE)this.ServiceProvider.GetService(typeof(EnvDTE.DTE));  
        if (dte.Solution != null)   
        {  
            . . .  
        }  
        else   
        {  
            MessageBox.Show("No solution is open");  
            return;   
        }  
    }  
    ```  
  
8. 共有プロジェクトを検索します。 共有プロジェクトは純粋なコンテナーです。出力はビルドまたは生成されません。 次のメソッドは、共有プロジェクト機能を持つオブジェクトを検索することによって、ソリューション内の最初の共有プロジェクトを検索し <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。  
  
    ```csharp  
    private IVsHierarchy FindSharedProject()  
    {  
        var sln = (IVsSolution)this.ServiceProvider.GetService(typeof(SVsSolution));  
        Guid empty = Guid.Empty;  
        IEnumHierarchies enumHiers;  
  
        //get all the projects in the solution  
        ErrorHandler.ThrowOnFailure(sln.GetProjectEnum((uint)__VSENUMPROJFLAGS.EPF_LOADEDINSOLUTION, ref empty, out enumHiers));  
        foreach (IVsHierarchy hier in ComUtilities.EnumerableFrom(enumHiers))  
        {  
            if (PackageUtilities.IsCapabilityMatch(hier, "SharedAssetsProject"))  
            {  
                return hier;  
            }  
        }  
        return null;  
    }  
    ```  
  
9. メソッドで `ShowMessageBox` 、共有プロジェクトのキャプション ( **ソリューションエクスプローラー**に表示されるプロジェクト名) を出力します。  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));  
  
        if (dte.Solution != null)  
        {  
            var sharedHier = this.FindSharedProject();  
            if (sharedHier != null)  
            {  
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,  
                     (int)__VSHPROPID.VSHPROPID_Caption);  
                output.OutputStringThreadSafe(string.Format("Found shared project: {0}\n", sharedCaption));  
            }  
            else  
            {  
                MessageBox.Show("Solution has no shared project");  
                return;  
            }  
                }  
        else  
        {  
            MessageBox.Show("No solution is open");  
            return;  
        }  
    }  
    ```  
  
10. アクティブなプラットフォームプロジェクトを取得します。 プラットフォームプロジェクトは、プラットフォーム固有のコードとリソースを含むプロジェクトです。 次のメソッドでは、新しいフィールドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7> アクティブなプラットフォームプロジェクトを取得します。  
  
    ```csharp  
    private IVsHierarchy GetActiveProjectContext(IVsHierarchy hierarchy)  
    {  
        IVsHierarchy activeProjectContext;  
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,  
             (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, out activeProjectContext))  
        {  
            return activeProjectContext;  
        }  
        else  
        {  
            return null;  
        }  
    }  
    ```  
  
11. メソッドで `ShowMessageBox` 、アクティブなプラットフォームプロジェクトのキャプションを出力します。  
  
    ```csharp  
    private void ShowMessageBox(object sender, EventArgs e)  
    {  
        var dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));  
  
        if (dte.Solution != null)  
        {  
            var sharedHier = this.FindSharedProject();  
            if (sharedHier != null)  
            {  
                string sharedCaption = HierarchyUtilities.GetHierarchyProperty<string>(sharedHier, (uint)VSConstants.VSITEMID.Root,  
                     (int)__VSHPROPID.VSHPROPID_Caption);  
                output.OutputStringThreadSafe(string.Format("Shared project: {0}\n", sharedCaption));  
  
                var activePlatformHier = this.GetActiveProjectContext(sharedHier);  
                if (activePlatformHier != null)  
                {  
                    string activeCaption = HierarchyUtilities.GetHierarchyProperty<string>(activePlatformHier,  
                         (uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID.VSHPROPID_Caption);  
                    output.OutputStringThreadSafe(string.Format("Active platform project: {0}\n", activeCaption));  
                }  
                else  
                {  
                MessageBox.Show("Shared project has no active platform project");  
                }  
            }  
            else  
            {  
                MessageBox.Show("Solution has no shared project");  
                return;  
            }  
        }  
        else  
            {  
                MessageBox.Show("No solution is open");  
                return;  
            }  
        }  
  
    ```  
  
12. プラットフォームプロジェクトを反復処理します。 次のメソッドは、共有プロジェクトからすべてのインポート (platform) プロジェクトを取得します。  
  
    ```csharp  
    private IEnumerable<IVsHierarchy> EnumImportingProjects(IVsHierarchy hierarchy)  
    {  
        IVsSharedAssetsProject sharedAssetsProject;  
        if (HierarchyUtilities.TryGetHierarchyProperty(hierarchy, (uint)VSConstants.VSITEMID.Root,  
            (int)__VSHPROPID7.VSHPROPID_SharedAssetsProject, out sharedAssetsProject)  
            && sharedAssetsProject != null)  
        {  
            foreach (IVsHierarchy importingProject in sharedAssetsProject.EnumImportingProjects())  
            {  
                yield return importingProject;  
            }  
        }  
    }  
    ```  
  
    > [!IMPORTANT]
    > ユーザーが実験用インスタンスで C++ ユニバーサル Windows アプリプロジェクトを開いている場合、上記のコードは例外をスローします。 これは既知の問題です。 例外を回避するには、 `foreach` 上のブロックを次のように置き換えます。  
  
    ```csharp  
    var importingProjects = sharedAssetsProject.EnumImportingProjects();  
    for (int i = 0; i < importingProjects.Count; ++i)  
    {  
        yield return importingProjects[i];  
    }   
    ```  
  
13. メソッドで `ShowMessageBox` 、各プラットフォームプロジェクトのキャプションを出力します。 アクティブなプラットフォームプロジェクトのキャプションを出力する行の後に、次のコードを挿入します。 この一覧には、読み込まれているプラットフォームプロジェクトのみが表示されます。  
  
    ```csharp  
    output.OutputStringThreadSafe("Platform projects:\n");  
  
    IEnumerable<IVsHierarchy> projects = this.EnumImportingProjects(sharedHier);  
  
    bool isActiveProjectSet = false;  
    foreach (IVsHierarchy platformHier in projects)  
    {  
        string platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,  
            (int)__VSHPROPID.VSHPROPID_Caption);  
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));  
    }  
    ```  
  
14. アクティブなプラットフォームプロジェクトを変更します。 次のメソッドは、を使用してアクティブなプロジェクトを設定し <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A> ます。  
  
    ```csharp  
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)  
    {  
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);  
    }  
    ```  
  
15. メソッドで `ShowMessageBox` 、アクティブなプラットフォームプロジェクトを変更します。 このコードをブロック内に挿入 `foreach` します。  
  
    ```csharp  
    bool isActiveProjectSet = false;  
    string platformCaption = null;  
    foreach (IVsHierarchy platformHier in projects)  
    {  
        platformCaption = HierarchyUtilities.GetHierarchyProperty<string>(platformHier, (uint)VSConstants.VSITEMID.Root,  
             (int)__VSHPROPID.VSHPROPID_Caption);  
        output.OutputStringThreadSafe(string.Format(" * {0}\n", platformCaption));  
  
        // if this project is neither the shared project nor the current active platform project,   
        // set it to be the active project  
        if (!isActiveProjectSet && platformHier != activePlatformHier)  
        {  
            this.SetActiveProjectContext(sharedHier, platformHier);  
            activePlatformHier = platformHier;  
            isActiveProjectSet = true;  
        }  
    }  
    output.OutputStringThreadSafe("set active project: " + platformCaption +'\n');  
    ```  
  
16. では、試してみましょう。F5 キーを押して実験用インスタンスを起動します。 実験用インスタンス ([ **新しいプロジェクト** ] ダイアログボックスの [Visual C#]/[windows]/[ **Windows 8/ユニバーサル/ハブアプリ**]) で、C# ユニバーサルハブアプリプロジェクトを作成します。 ソリューションが読み込まれたら、[ **ツール** ] メニューにアクセスし、[ **TestUniversalProject の呼び出し**] をクリックして、 **出力** ウィンドウのテキストを確認します。 次のように表示されます。  
  
    ```  
    Found shared project: HubApp.Shared  
    The active platform project: HubApp.Windows  
    Platform projects:  
     * HubApp.Windows  
     * HubApp.WindowsPhone  
    set active project: HubApp.WindowsPhone  
    ```  
  
### <a name="manage-the-shared-items-in-the-platform-project"></a>プラットフォームプロジェクトで共有項目を管理する  
  
1. プラットフォームプロジェクトで共有項目を検索します。 共有プロジェクト内の項目は、共有項目としてプラットフォームプロジェクトに表示されます。 **ソリューションエクスプローラー**に表示されることはありませんが、プロジェクト階層で検索することができます。 次のメソッドは、階層をウォークし、すべての共有項目を収集します。 必要に応じて、各項目のキャプションを出力します。 共有項目は、新しいプロパティによって識別され <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7> ます。  
  
    ```csharp  
    private void InspectHierarchyItems(IVsHierarchy hier, uint itemid, int level, List<uint> itemIds, bool getSharedItems, bool printItems)  
    {  
        string caption = HierarchyUtilities.GetHierarchyProperty<string>(hier, itemid, (int)__VSHPROPID.VSHPROPID_Caption);  
        if (printItems)  
            output.OutputStringThreadSafe(string.Format("{0}{1}\n", new string('\t', level), caption));  
  
        // if getSharedItems is true, inspect only shared items; if it's false, inspect only unshared items  
        bool isSharedItem;  
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID7.VSHPROPID_IsSharedItem, out isSharedItem)  
            && (isSharedItem == getSharedItems))  
        {  
            itemIds.Add(itemid);  
        }  
  
        uint child;  
        if (HierarchyUtilities.TryGetHierarchyProperty(hier, itemid, (int)__VSHPROPID.VSHPROPID_FirstChild, Unbox.AsUInt32, out child)  
            && child != (uint)VSConstants.VSITEMID.Nil)  
        {  
            this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);  
  
            while (HierarchyUtilities.TryGetHierarchyProperty(hier, child, (int)__VSHPROPID.VSHPROPID_NextSibling, Unbox.AsUInt32, out child)  
                && child != (uint)VSConstants.VSITEMID.Nil)  
            {  
                this.InspectHierarchyItems(hier, child, level + 1, itemIds, isSharedItem, printItems);  
            }  
                    }  
    }  
    ```  
  
2. メソッドで `ShowMessageBox` 、次のコードを追加して、プラットフォームプロジェクト階層の項目をウォークします。 ブロック内に挿入 `foreach` します。  
  
    ```csharp  
    output.OutputStringThreadSafe("Walk the active platform project:\n");  
    var sharedItemIds = new List<uint>();  
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);  
    ```  
  
3. 共有アイテムを読み取ります。 共有項目は、プラットフォームプロジェクトに非表示のリンクファイルとして表示され、すべてのプロパティを通常のリンクファイルとして読み取ることができます。 次のコードは、最初の共有項目の完全パスを読み取ります。  
  
    ```csharp  
    var sharedItemId = sharedItemIds[0];  
    string fullPath;  
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));  
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));  
    ```  
  
4. では、試してみましょう。F5 キーを押して実験用インスタンスを起動します。 実験用インスタンスで C# ユニバーサルハブアプリプロジェクトを作成します ([ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/windows/Windows 8/Universal/hub アプリ**)。 [ **ツール** ] メニューにアクセスし、[ **TestUniversalProject の呼び出し**] をクリックして、 **出力** ウィンドウのテキストを確認します。 次のように表示されます。  
  
    ```  
    Found shared project: HubApp.Shared  
    The active platform project: HubApp.Windows  
    Platform projects:  
     * HubApp.Windows  
     * HubApp.WindowsPhone  
    set active project: HubApp.WindowsPhone  
    Walk the active platform project:  
        HubApp.WindowsPhone  
            <HubApp.Shared>  
                App.xaml  
                    App.xaml.cs  
                Assets  
                    DarkGray.png  
                    LightGray.png  
                    MediumGray.png  
                Common  
                    NavigationHelper.cs  
                    ObservableDictionary.cs  
                    RelayCommand.cs  
                    SuspensionManager.cs  
                DataModel  
                    SampleData.json  
                    SampleDataSource.cs  
                HubApp.Shared.projitems  
                Strings  
                    en-US  
                        Resources.resw  
            Assets  
                HubBackground.theme-dark.png  
                HubBackground.theme-light.png  
                Logo.scale-240.png  
                SmallLogo.scale-240.png  
                SplashScreen.scale-240.png  
                Square71x71Logo.scale-240.png  
                StoreLogo.scale-240.png  
                WideLogo.scale-240.png  
            HubPage.xaml  
                HubPage.xaml.cs  
            ItemPage.xaml  
                ItemPage.xaml.cs  
            Package.appxmanifest  
            Properties  
                AssemblyInfo.cs  
            References  
                .NET for Windows Store apps  
                HubApp.Shared  
                Windows Phone 8.1  
            SectionPage.xaml  
                SectionPage.xaml.cs  
    ```  
  
### <a name="detecting-changes-in-platform-projects-and-shared-projects"></a>プラットフォームプロジェクトと共有プロジェクトの変更の検出  
  
1. 階層とプロジェクトイベントを使用して、プラットフォームプロジェクトの場合と同様に、共有プロジェクトの変更を検出できます。 ただし、共有プロジェクト内のプロジェクトアイテムは表示されません。これは、共有プロジェクトアイテムが変更されたときに特定のイベントが発生しないことを意味します。  
  
    プロジェクト内のファイルの名前が変更されたときの一連のイベントを考えてみましょう。  
  
   1. ファイル名はディスク上で変更されています。  
  
   2. プロジェクトファイルが更新され、ファイルの新しい名前が含められます。  
  
      階層イベント (たとえば、) は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> 通常、 **ソリューションエクスプローラー**のように、UI に表示される変更を追跡します。 階層イベントは、ファイルの名前変更操作をファイルの削除によって構成し、ファイルを追加することを検討します。 ただし、非表示の項目が変更された場合、階層のイベントシステムはイベントを発生さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> せますが、イベントは発生しません <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 。 したがって、プラットフォームプロジェクト内のファイルの名前を変更すると、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> の両方が取得されますが、共有プロジェクト内のファイルの名前を変更すると、のみが取得さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> れます。  
  
      プロジェクト項目の変更を追跡するには、DTE プロジェクト項目イベント (で見つかったもの) を処理し <xref:EnvDTE.ProjectItemsEventsClass> ます。 ただし、大量のイベントを処理する場合は、のイベントを処理するパフォーマンスを向上させることができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> ます。 このチュートリアルでは、階層イベントと DTE イベントのみを示します。 この手順では、共有プロジェクトとプラットフォームプロジェクトにイベントリスナーを追加します。 次に、共有プロジェクト内の1つのファイルの名前を変更し、プラットフォームプロジェクト内の別のファイルを変更すると、各名前変更操作に対して発生したイベントを確認できます。  
  
      この手順では、共有プロジェクトとプラットフォームプロジェクトにイベントリスナーを追加します。 次に、共有プロジェクト内の1つのファイルの名前を変更し、プラットフォームプロジェクト内の別のファイルを変更すると、各名前変更操作に対して発生したイベントを確認できます。  
  
2. イベントリスナーを追加します。 新しいクラスファイルをプロジェクトに追加し、HierarchyEventListener.cs を呼び出します。  
  
3. HierarchyEventListener.cs ファイルを開き、次の using ステートメントを追加します。  
  
   ```csharp  
   using Microsoft.VisualStudio.Shell.Interop;  
   using Microsoft.VisualStudio;  
   using System.IO;  
  
   ```  
  
4. 次の `HierarchyEventListener` ようにクラスを実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ます。  
  
   ```csharp  
   class HierarchyEventListener : IVsHierarchyEvents  
   { }  
  
   ```  
  
5. 次のコードの <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents> ように、のメンバーを実装します。  
  
   ```csharp  
   class HierarchyEventListener : IVsHierarchyEvents  
   {  
       private IVsHierarchy hierarchy;  
       IVsOutputWindowPane output;   
  
       internal HierarchyEventListener(IVsHierarchy hierarchy, IVsOutputWindowPane outputWindow) {  
            this.hierarchy = hierarchy;  
            this.output = outputWindow;  
       }  
  
       int IVsHierarchyEvents.OnInvalidateIcon(IntPtr hIcon) {  
           return VSConstants.S_OK;  
       }  
  
       int IVsHierarchyEvents.OnInvalidateItems(uint itemIDParent) {  
           return VSConstants.S_OK;  
       }  
  
       int IVsHierarchyEvents.OnItemAdded(uint itemIDParent, uint itemIDSiblingPrev, uint itemIDAdded) {  
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemAdded: " + itemIDAdded + "\n");  
           return VSConstants.S_OK;  
       }  
  
       int IVsHierarchyEvents.OnItemDeleted(uint itemID) {  
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemDeleted: " + itemID + "\n");  
           return VSConstants.S_OK;  
       }  
  
       int IVsHierarchyEvents.OnItemsAppended(uint itemIDParent) {  
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnItemsAppended\n");  
           return VSConstants.S_OK;  
       }  
  
       int IVsHierarchyEvents.OnPropertyChanged(uint itemID, int propID, uint flags) {  
           output.OutputStringThreadSafe("IVsHierarchyEvents.OnPropertyChanged: item ID " + itemID + "\n");  
           return VSConstants.S_OK;  
       }  
   }  
  
   ```  
  
6. 同じクラスで、DTE イベントの別のイベントハンドラー <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> を追加します。これは、プロジェクト項目の名前が変更されるたびに発生します。  
  
   ```csharp  
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)  
   {  
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",  
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));  
   }  
   ```  
  
7. 階層イベントにサインアップします。 追跡するプロジェクトごとに個別にサインアップする必要があります。 に次のコードを追加し `ShowMessageBox` ます。1つは共有プロジェクト用で、もう1つはプラットフォームプロジェクトの1つです。  
  
   ```csharp  
   // hook up the event listener for hierarchy events on the shared project  
   HierarchyEventListener listener1 = new HierarchyEventListener(sharedHier, output);  
   uint cookie1;  
   sharedHier.AdviseHierarchyEvents(listener1, out cookie1);  
  
   // hook up the event listener for hierarchy events on the   
   active project  
   HierarchyEventListener listener2 = new HierarchyEventListener(activePlatformHier, output);  
   uint cookie2;  
   activePlatformHier.AdviseHierarchyEvents(listener2, out cookie2);  
   ```  
  
8. DTE プロジェクト項目イベントにサインアップ <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> します。 2番目のリスナーをフックした後、次のコードを追加します。  
  
   ```csharp  
   // hook up DTE events for project items  
   Events2 dteEvents = (Events2)dte.Events;  
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;  
  
   ```  
  
9. 共有項目を変更します。 プラットフォームプロジェクトで共有項目を変更することはできません。代わりに、これらの項目の実際の所有者である共有プロジェクトで変更する必要があります。 共有プロジェクト内の対応する項目 ID を取得するには <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> 、共有項目の完全パスを指定します。 その後、共有項目を変更できます。 変更はプラットフォームプロジェクトに反映されます。  
  
    > [!IMPORTANT]
    > プロジェクト項目を変更する前に、その項目が共有項目であるかどうかを確認する必要があります。  
  
     次のメソッドは、プロジェクト項目ファイルの名前を変更します。  
  
    ```csharp  
    private void ModifyFileNameInProject(IVsHierarchy project, string path)  
    {    
        int found;  
        uint projectItemID;  
        VSDOCUMENTPRIORITY[] priority = new VSDOCUMENTPRIORITY[1];  
        if (ErrorHandler.Succeeded(((IVsProject)project).IsDocumentInProject(path, out found, priority, out projectItemID))  
            && found != 0)  
        {  
            var name = DateTime.Now.Ticks.ToString() + Path.GetExtension(path);  
            project.SetProperty(projectItemID, (int)__VSHPROPID.VSHPROPID_EditLabel, name);  
            output.OutputStringThreadSafe(string.Format("Renamed {0} to {1}\n", path,name));  
        }  
    }  
    ```  
  
10. 内の他のすべてのコードの後 `ShowMessageBox` に、共有プロジェクト内の項目のファイル名を変更するには、このメソッドを呼び出します。 共有プロジェクト内の項目の完全パスを取得するコードの後に、これを挿入します。  
  
    ```csharp  
    // change the file name of an item in a shared project  
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);  
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));   
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));  
    this.ModifyFileNameInProject(sharedHier, fullPath);  
    ```  
  
11. プロジェクトをビルドして実行します。 実験用インスタンスで C# ユニバーサルハブアプリを作成し、[ **ツール** ] メニューにアクセスし、[ **TestUniversalProject の呼び出し**] をクリックして、[全般出力] ウィンドウのテキストを確認します。 共有プロジェクトの最初の項目の名前 (app.xaml ファイルであることが予想されます) は変更する必要があり、イベントが発生したことを確認する必要があり <xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed> ます。 この場合、app.xaml の名前を変更すると App.xaml.cs の名前も変更されるため、4つのイベント (プラットフォームプロジェクトごとに2つ) が表示されます。 (DTE イベントは、共有プロジェクト内の項目を追跡しません)。2つ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> のイベント (プラットフォームプロジェクトごとに1つ) が表示しますが、イベントはありません <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> 。  
  
12. ここで、プラットフォームプロジェクト内のファイルの名前を変更しようとすると、発生したイベントの違いを確認できます。 の呼び出しの後に、次のコードを追加し `ShowMessageBox` `ModifyFileName` ます。  
  
    ```csharp  
    // change the file name of an item in a platform project  
    var unsharedItemIds = new List<uint>();  
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, unsharedItemIds, false, false);  
  
    var unsharedItemId = unsharedItemIds[0];  
    string unsharedPath;  
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(unsharedItemId, out unsharedPath));  
    output.OutputStringThreadSafe(string.Format("Platform project item ID = {0}, full path = {1}\n", unsharedItemId, unsharedPath));  
  
    this.ModifyFileNameInProject(activePlatformHier, unsharedPath);  
    ```  
  
13. プロジェクトをビルドして実行します。 実験用インスタンスで C# ユニバーサルプロジェクトを作成し、[ **ツール** ] メニューにアクセスして [ **TestUniversalProject の呼び出し**] をクリックし、[全般出力] ウィンドウのテキストを確認します。 プラットフォームプロジェクト内のファイルの名前を変更すると、イベントとイベントの両方が表示さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A> れます。 ファイルの変更によって他のファイルが変更されることはないため、プラットフォームプロジェクト内の項目に対する変更はどこにも反映されないため、これらのイベントが1つだけ存在します。
