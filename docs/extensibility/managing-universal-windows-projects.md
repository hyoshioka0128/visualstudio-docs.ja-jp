---
title: ユニバーサル Windows プロジェクトの管理 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 47926aa1-3b41-410d-bca8-f77fc950cbe7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fbbf9b6aaf983bb36291611a7b9b50f7886915b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702683"
---
# <a name="manage-universal-windows-projects"></a>ユニバーサル Windows プロジェクトの管理

ユニバーサル Windows アプリは、Windows 8.1 と Windows Phone 8.1 の両方を対象とするアプリであり、開発者は両方のプラットフォームでコードやその他の資産を使用できます。 共有コードと共有リソースは共有プロジェクトに保持され、プラットフォーム固有のコードとリソースは Windows 用と Windows Phone 用のプロジェクトに個別に保持されます。 ユニバーサル Windows アプリの詳細については、「[ユニバーサル Windows アプリ](https://msdn.microsoft.com/library/windows/apps/dn609832.aspx)」を参照してください。 プロジェクトを管理する Visual Studio 拡張機能は、ユニバーサル Windows アプリ プロジェクトには、単一プラットフォーム アプリとは異なる構造を持つことを認識する必要があります。 このチュートリアルでは、共有プロジェクトをナビゲートし、共有アイテムを管理する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="navigate-the-shared-project"></a>共有プロジェクトのナビゲート

1. という名前の C# VSIX プロジェクト**を作成します**。 (**ファイル** > **の新しい** > **プロジェクト**と**C#** > **拡張機能** > Visual Studio**パッケージ**) 。 カスタム**コマンド**プロジェクト項目テンプレートを追加します (**ソリューション エクスプローラ**でプロジェクト ノードを右クリックし、[**新しい項目**の**追加** > ] を選択して、[**機能拡張**] に移動します)。 ファイルに名前を付**けます。**

2. への*参照を追加*します。 *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* **Extensions**

3. *TestUniversalProject.cs*開き、次`using`のディレクティブを追加します。

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

4. クラスに`TestUniversalProject`**、出力**ウィンドウを指すプライベートフィールドを追加します。

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

6. メソッドから既存のコードを`ShowMessageBox`削除します。

    ```csharp
    private void ShowMessageBox(object sender, EventArgs e)
    {
    }
    ```

7. このチュートリアルでは、いくつかの異なる目的で使用する DTE オブジェクトを取得します。 また、メニュー ボタンがクリックされたときにソリューションが読み込まれるようにします。

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

8. 共有プロジェクトを検索します。 共有プロジェクトは純粋なコンテナです。出力はビルドまたは生成されません。 次のメソッドは、共有プロジェクト機能を持つオブジェクトを検索して<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>、ソリューション内の最初の共有プロジェクトを検索します。

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

9. メソッドで`ShowMessageBox`、共有プロジェクトのキャプション (**ソリューション エクスプローラー**に表示されるプロジェクト名) を出力します。

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

10. アクティブなプラットフォーム プロジェクトを取得します。 プラットフォーム プロジェクトは、プラットフォーム固有のコードとリソースを含むプロジェクトです。 次のメソッドは、新しい<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy>フィールドを使用して、アクティブなプラットフォーム プロジェクトを取得します。

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

11. メソッドで`ShowMessageBox`、アクティブなプラットフォーム プロジェクトのキャプションを出力します。

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
    }
    ```

12. プラットフォーム プロジェクトを反復処理します。 次のメソッドは、共有プロジェクトからすべてのインポート (プラットフォーム) プロジェクトを取得します。

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
    > ユーザーが実験用インスタンスで C++ ユニバーサル Windows アプリ プロジェクトを開いた場合、上記のコードは例外をスローします。 これは既知の問題です。 この例外を回避するには、上記`foreach`のブロックを次のように置き換えます。

    ```csharp
    var importingProjects = sharedAssetsProject.EnumImportingProjects();
    for (int i = 0; i < importingProjects.Count; ++i)
    {
        yield return importingProjects[i];
    }
    ```

13. メソッドでは`ShowMessageBox`、各プラットフォーム プロジェクトのキャプションを出力します。 アクティブなプラットフォーム プロジェクトのキャプションを出力する行の後に次のコードを挿入します。 この一覧には、読み込まれたプラットフォーム プロジェクトのみが表示されます。

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

14. アクティブなプラットフォーム プロジェクトを変更します。 次のメソッドは、 を使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.SetProperty%2A>してアクティブなプロジェクトを設定します。

    ```csharp
    private int SetActiveProjectContext(IVsHierarchy hierarchy, IVsHierarchy activeProjectContext)
    {
        return hierarchy.SetProperty((uint)VSConstants.VSITEMID.Root, (int)__VSHPROPID7.VSHPROPID_SharedItemContextHierarchy, activeProjectContext);
    }
    ```

15. メソッドで`ShowMessageBox`、アクティブなプラットフォーム プロジェクトを変更します。 このコードをブロック内`foreach`に挿入します。

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

16. 今それを試してみてください。F5 キーを押して、実験用インスタンスを起動します。 実験用インスタンスに C# ユニバーサル ハブ アプリ プロジェクトを作成します ([**新しいプロジェクト**] ダイアログ ボックスの**Visual C#** > **Windows** > **8** > **ユニバーサル** > ハブ**アプリ**)。 ソリューションが読み込まれたら、[**ツール**] メニューの **[TestUniversalProject の呼び出**し] をクリックし、**出力**ペインでテキストを確認します。 次のように表示されます。

    ```
    Found shared project: HubApp.Shared
    The active platform project: HubApp.Windows
    Platform projects:
     * HubApp.Windows
     * HubApp.WindowsPhone
    set active project: HubApp.WindowsPhone
    ```

### <a name="manage-the-shared-items-in-the-platform-project"></a>プラットフォーム プロジェクトの共有アイテムを管理する

1. プラットフォーム プロジェクト内の共有アイテムを検索します。 共有プロジェクトの項目は、プラットフォーム プロジェクトに共有アイテムとして表示されます。 **ソリューション エクスプローラー**では表示できませんが、プロジェクト階層を参照して見つけることができます。 次のメソッドは、階層を走査し、すべての共有アイテムを収集します。 オプションで各項目のキャプションを出力します。 共有アイテムは、新しいプロパティ<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID7.VSHPROPID_IsSharedItem>によって識別されます。

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

2. メソッドで`ShowMessageBox`、プラットフォーム プロジェクト階層項目をウォークする次のコードを追加します。 ブロック内に挿入`foreach`します。

    ```csharp
    output.OutputStringThreadSafe("Walk the active platform project:\n");
    var sharedItemIds = new List<uint>();
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ```

3. 共有アイテムを読み取ります。 共有アイテムは、プラットフォーム プロジェクトに隠しリンク ファイルとして表示され、すべてのプロパティを通常のリンク ファイルとして読み取ることができます。 次のコードは、最初の共有アイテムの完全パスを読み取ります。

    ```csharp
    var sharedItemId = sharedItemIds[0];
    string fullPath;
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared item full path: {0}\n", fullPath));
    ```

4. 今それを試してみてください。**F5 キー**を押して、実験用インスタンスを起動します。 実験用インスタンス **([新しいプロジェクト**] ダイアログ ボックスの**Visual C#** > **Windows** > **8** > **ユニバーサル** > ハブ アプリ) で C# ユニバーサル ハブ**アプリ**プロジェクトを作成し、[**ツール**] メニューをクリックし **、[TestUniversalProject の呼び出**し] をクリックして **、出力**ウィンドウでテキストを確認します。 次のように表示されます。

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

### <a name="detect-changes-in-platform-projects-and-shared-projects"></a>プラットフォーム プロジェクトおよび共有プロジェクトの変更を検出する

1. 階層イベントとプロジェクトイベントを使用して、プラットフォームプロジェクトの場合と同様に、共有プロジェクトの変更を検出できます。 ただし、共有プロジェクト内のプロジェクト項目は表示されず、共有プロジェクト項目が変更されたときに特定のイベントが発生しないことを意味します。

    プロジェクト内のファイルの名前を変更する場合のイベントのシーケンスを考慮してください。

   1. ディスク上でファイル名が変更されます。

   2. プロジェクト ファイルが更新され、ファイルの新しい名前が含まれます。

      階層イベント ( たとえば<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>) は、通常、**ソリューション エクスプローラ**のように、UI に表示される変更を追跡します。 階層イベントは、ファイルの名前変更操作をファイルの削除とファイルの追加で構成することを考慮します。 ただし、非表示の項目が変更されると、階層イベント システムは<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>イベントを発生させます<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>が、イベントは発生しません。 したがって、プラットフォーム プロジェクトのファイルの名前を変更すると、 と<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>の両方が表示されますが、共有プロジェクトのファイル名を変更した場合<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>は、 のみが取得されます。

      プロジェクト項目の変更を追跡するには、DTE プロジェクト項目イベント (で<xref:EnvDTE.ProjectItemsEventsClass>見つかったイベント) を処理できます。 ただし、多数のイベントを処理する場合は、 の<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>イベントを処理するパフォーマンスが向上します。 このチュートリアルでは、階層イベントと DTE イベントのみを示します。 この手順では、共有プロジェクトとプラットフォーム プロジェクトにイベント リスナーを追加します。 共有プロジェクト内の 1 つのファイルとプラットフォーム プロジェクト内の別のファイルの名前を変更すると、名前の変更操作ごとに発生するイベントを確認できます。

      この手順では、共有プロジェクトとプラットフォーム プロジェクトにイベント リスナーを追加します。 共有プロジェクト内の 1 つのファイルとプラットフォーム プロジェクト内の別のファイルの名前を変更すると、名前の変更操作ごとに発生するイベントを確認できます。

2. イベントリスナーを追加します。 新しいクラス ファイルをプロジェクトに追加し、それを*HierarchyEventListener.cs*呼び出します。

3. *HierarchyEventListener.cs*ファイルを開き、次の using ディレクティブを追加します。

   ```csharp
   using Microsoft.VisualStudio.Shell.Interop;
   using Microsoft.VisualStudio;
   using System.IO;
   ```

4. クラスに`HierarchyEventListener`実装を<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>持っています:

   ```csharp
   class HierarchyEventListener : IVsHierarchyEvents
   { }
   ```

5. のメンバー<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents>を実装します。

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

6. 同じクラスで、プロジェクト項目の名前が変更されるたびに発生<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>する DTE イベントに対して、別のイベント ハンドラーを追加します。

   ```csharp
   public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)
   {
       output.OutputStringThreadSafe(string.Format("[Event] Renamed {0} to {1} in project {2}\n",
            oldName, Path.GetFileName(projItem.get_FileNames(1)), projItem.ContainingProject.Name));
   }
   ```

7. 階層イベントにサインアップします。 追跡しているプロジェクトごとに個別にサインアップする必要があります。 次のコードを、`ShowMessageBox`に共有プロジェクト用に、もう 1 つはプラットフォーム プロジェクトの 1 つに追加します。

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

8. DTE プロジェクト項目イベント<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>にサインアップします。 2 番目のリスナーをフックした後、次のコードを追加します。

   ```csharp
   // hook up DTE events for project items
   Events2 dteEvents = (Events2)dte.Events;
   dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;
   ```

9. 共有アイテムを変更します。 プラットフォーム プロジェクトの共有アイテムは変更できません。代わりに、これらのアイテムの実際の所有者である共有プロジェクトで変更する必要があります。 共有プロジェクトの対応する項目 ID を 取得<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A>するには、 を使用して共有アイテムの完全パスを指定します。 共有アイテムを変更できます。 変更はプラットフォーム プロジェクトに反映されます。

    > [!IMPORTANT]
    > プロジェクトアイテムが共有アイテムであるかどうかを確認してから、変更してください。

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

10. このメソッドは、他のすべてのコードの後`ShowMessageBox`に呼び出して、共有プロジェクト内の項目のファイル名を変更します。 共有プロジェクト内の項目の完全パスを取得するコードの後に挿入します。

    ```csharp
    // change the file name of an item in a shared project
    this.InspectHierarchyItems(activePlatformHier, (uint)VSConstants.VSITEMID.Root, 1, sharedItemIds, true, true);
    ErrorHandler.ThrowOnFailure(((IVsProject)activePlatformHier).GetMkDocument(sharedItemId, out fullPath));
    output.OutputStringThreadSafe(string.Format("Shared project item ID = {0}, full path = {1}\n", sharedItemId, fullPath));
    this.ModifyFileNameInProject(sharedHier, fullPath);
    ```

11. プロジェクトをビルドして実行します。 実験用インスタンスで C# ユニバーサル ハブ アプリを作成し、[**ツール**] メニューの **[TestUniversalProject の呼び出し**] をクリックして、一般的な出力ウィンドウでテキストを確認します。 共有プロジェクトの最初の項目の名前 *(App.xaml*ファイルであることを想定しています) を変更する必要があり、イベントが発生したことを確認する<xref:EnvDTE.ProjectItemsEventsClass.ItemRenamed>必要があります。 この場合 *、App.xaml*の名前を変更すると*App.xaml.cs*も名前が変更されるため、4 つのイベント (プラットフォーム プロジェクトごとに 2 つ) が表示されます。 (DTE イベントは、共有プロジェクト内の項目を追跡しません)。2 つの<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>イベント (プラットフォーム プロジェクトごとに 1 つ)<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>が表示されますが、イベントは表示されません。

12. プラットフォームプロジェクトでファイルの名前を変更すると、発生するイベントの違いを確認できます。 への呼び出し`ShowMessageBox`の後に次`ModifyFileName`のコードを追加します。

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

13. プロジェクトをビルドして実行します。 実験用インスタンスで C# ユニバーサル プロジェクトを作成し、[**ツール**] メニューの **[TestUniversalProject の呼び出し**] をクリックして、一般出力ペインでテキストを確認します。 プラットフォーム プロジェクトのファイルの名前を変更すると、イベントとイベントの<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemAdded%2A>両方が表示<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyEvents.OnItemDeleted%2A>されます。 ファイルを変更すると他のファイルは変更されず、プラットフォーム プロジェクト内の項目に対する変更はどこにも反映されないので、これらのイベントは 1 つしかありません。
