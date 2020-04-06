---
title: メニュー項目の動的な追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4387c1930e09e49c0ec5c36ccedc1bb83dc273f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712068"
---
# <a name="dynamically-add-menu-items"></a>メニュー項目を動的に追加する
実行時にメニュー項目を追加するには、Visual Studio`DynamicItemStart`のコマンド テーブル *(.vsct)* ファイルのプレースホルダ ボタン定義にコマンド フラグを指定し、表示するメニュー項目の数を (コードで) 定義し、コマンドを処理します。 VSPackage が読み込まれると、プレースホルダーは動的メニュー項目に置き換えられます。

 Visual Studio では、最近開いたドキュメントの名前を表示する **、最近使用**したドキュメントの名前を表示する 、最近開いているウィンドウの名前を表示する**Windows**リストの一覧で、最近使用した最新の一覧 (MRU) の動的な一覧を使用します。   コマンド`DynamicItemStart`定義のフラグは、VSPackage が開かれるまでコマンドがプレースホルダーであることを指定します。 VSPackage を開くと、実行時に作成され、動的な一覧に追加される 0 つ以上のコマンドに置き換えられます。 VSPackage を開くまで、動的な一覧が表示されるメニューの位置を表示できない場合があります。  動的な一覧を作成するには、Visual Studio は、最初の文字がプレースホルダーの ID と同じである ID を持つコマンドを検索する VSPackage を要求します。 Visual Studio は、一致するコマンドを検出すると、動的な一覧にコマンドの名前を追加します。 次に、ID をインクリメントし、動的なコマンドがなくなるまで動的リストに追加する別の一致コマンドを探します。

 このチュートリアルでは、**ソリューション エクスプローラー**のツール バーのコマンドを使用して Visual Studio ソリューションのスタートアップ プロジェクトを設定する方法について説明します。 アクティブなソリューション内のプロジェクトの動的なドロップダウン リストを持つメニュー コント ローラーを使用します。 開いているソリューションがない場合や、開いているソリューションにプロジェクトが 1 つしかない場合にこのコマンドが表示されないようにするには、ソリューションに複数のプロジェクトがある場合にのみ VSPackage が読み込まれます。

 *vsct*ファイルの詳細については、「 [Visual Studio コマンド テーブル (.vsct) ファイル 」](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成する

1. という名前`DynamicMenuItems`の VSIX プロジェクトを作成します。

2. プロジェクトが開いたら、カスタム コマンド項目テンプレートを追加し、その名前を**DynamicMenu に**します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

## <a name="setting-up-the-elements-in-the-vsct-file"></a>*vsct*ファイル内の要素の設定
 ツールバーに動的メニュー項目を持つメニューコントローラを作成するには、次の要素を指定します。

- メニュー コントローラを含むコマンド グループとドロップダウンメニュー項目を含むコマンド グループ

- 型の 1 つのメニュー要素`MenuController`

- 2 つのボタンで、メニュー項目のプレースホルダーとして機能するボタンと、ツール バーにアイコンとツールチップを提供するボタンがあります。

1. で*コマンド*ID を定義します。 シンボル セクションに移動し **、GUID**のブロックの ID シンボル要素を置き換えます。 2 つのグループ、メニュー コント ローラー、プレースホルダー コマンド、およびアンカー コマンドの IDSymbol 要素を定義する必要があります。

    ```xml
    <GuidSymbol name="guidDynamicMenuPackageCmdSet" value="{ your GUID here }">
        <IDSymbol name="MyToolbarItemGroup" value="0x1020" />
        <IDSymbol name="MyMenuControllerGroup" value="0x1025" />
        <IDSymbol name="MyMenuController" value ="0x1030"/>
        <IDSymbol name="cmdidMyAnchorCommand" value="0x0103" />
        <!-- NOTE: The following command expands at run time to some number of ids.
         Try not to place command ids after it (e.g. 0x0105, 0x0106).
         If you must add a command id after it, make the gap very large (e.g. 0x200) -->
        <IDSymbol name="cmdidMyDynamicStartCommand" value="0x0104" />
    </GuidSymbol>
    ```

2. [グループ] セクションで、既存のグループを削除し、定義した 2 つのグループを追加します。

    ```xml
    <Groups>
        <!-- The group that adds the MenuController on the Solution Explorer toolbar.
             The 0x4000 priority adds this group after the group that contains the
             Preview Selected Items button, which is normally at the far right of the toolbar. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" priority="0x4000" >
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN" />
        </Group>
        <!-- The group for the items on the MenuController drop-down. It is added to the MenuController submenu. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" priority="0x4000" >
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" />
        </Group>
    </Groups>
    ```

     メニューコントローラを追加します。 常に表示されないので、DynamicVisibility コマンド フラグを設定します。 ボタンテキストは表示されません。

    ```xml
    <Menus>
        <!-- The MenuController to display on the Solution Explorer toolbar.
             Place it in the ToolbarItemGroup.-->
        <Menu guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" priority="0x1000" type="MenuController">
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" />
            <CommandFlag>DynamicVisibility</CommandFlag>
            <Strings>
               <ButtonText></ButtonText>
           </Strings>
        </Menu>
    </Menus>
    ```

3. 2 つのボタンを追加します。

     プレースホルダ ボタンの親は **、マイメニュー コントローラ グループです**。 プレースホルダー ボタンに [動的アイテムスタート]、[動的表示]、および [テキスト変更] コマンド フラグを追加します。 ボタンテキストは表示されません。

     アンカー ボタンには、アイコンとツールヒントのテキストが表示されます。 アンカー ボタンの親も **、 マイメニュー コント ローラー グループ**です。 ボタンがメニュー コントローラーのドロップダウン に実際に表示されないようにするために NoShowOnMenuController コマンド フラグを追加し、それを永続的なアンカーにする FixMenuController コマンド フラグを追加します。

    ```xml
    <!-- The placeholder for the dynamic items that expand to N items at run time. -->
    <Buttons>
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyDynamicStartCommand" priority="0x1000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <CommandFlag>DynamicItemStart</CommandFlag>
          <CommandFlag>DynamicVisibility</CommandFlag>
          <CommandFlag>TextChanges</CommandFlag>
          <!-- This text does not appear. -->
          <Strings>
            <ButtonText>Project</ButtonText>
          </Strings>
        </Button>

        <!-- The anchor item to supply the icon/tooltip for the MenuController -->
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyAnchorCommand" priority="0x0000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <!-- This is the icon that appears on the Solution Explorer toolbar. -->
          <Icon guid="guidImages" id="bmpPicArrows"/>
          <!-- Do not show on the menu controller's drop down list-->
          <CommandFlag>NoShowOnMenuController</CommandFlag>
          <!-- Become the permanent anchor item for the menu controller -->
          <CommandFlag>FixMenuController</CommandFlag>
          <!-- The text that appears in the tooltip.-->
          <Strings>
            <ButtonText>Set Startup Project</ButtonText>
          </Strings>
        </Button>
    </Buttons>
    ```

4. プロジェクトにアイコンを追加し (*リソース*フォルダー内)、参照を *.vsct*ファイルに追加します。 このチュートリアルでは、プロジェクト テンプレートに含まれている矢印アイコンを使用します。

5. [シンボル] セクションの直前にある [コマンド] セクションの外側に[可視性の制約]セクションを追加します。 (シンボルの後に追加すると警告が表示されることがあります。このセクションでは、複数のプロジェクトを含むソリューションが読み込まれたときにのみメニュー コントローラーが表示されるようにします。

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>動的メニュー コマンドを実装する
 から<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>継承する動的メニュー コマンド クラスを作成します。 この実装では、コンストラクターは、コマンドの一致に使用する述語を指定します。 この述語を<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>使用してプロパティを設定<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>するには、メソッドをオーバーライドする必要があります。

1. *DynamicItemMenuCommand.cs*という名前の新しい C# クラス ファイルを作成し、 から<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>継承する**DynamicItemMenuCommand**という名前のクラスを追加します。

    ```csharp
    class DynamicItemMenuCommand : OleMenuCommand
    {

    }

    ```

2. ディレクティブを使用して以下を追加します。

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    using System.ComponentModel.Design;
    ```

3. 一致述語を格納するプライベート フィールドを追加します。

    ```csharp
    private Predicate<int> matches;

    ```

4. コンストラクターから継承するコンストラクターを<xref:Microsoft.VisualStudio.Shell.OleMenuCommand>追加し、コマンド ハンドラーとハンドラーを<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>指定します。 コマンドに一致する述語を追加します。

    ```csharp
    public DynamicItemMenuCommand(CommandID rootId, Predicate<int> matches, EventHandler invokeHandler, EventHandler beforeQueryStatusHandler)
        : base(invokeHandler, null /*changeHandler*/, beforeQueryStatusHandler, rootId)
    {
        if (matches == null)
        {
            throw new ArgumentNullException("matches");
        }

        this.matches = matches;
    }
    ```

5. 一致<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A>述語を呼び出してプロパティを設定するように<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A>メソッドをオーバーライドします。

    ```csharp
    public override bool DynamicItemMatch(int cmdId)
    {
        // Call the supplied predicate to test whether the given cmdId is a match.
        // If it is, store the command id in MatchedCommandid
        // for use by any BeforeQueryStatus handlers, and then return that it is a match.
        // Otherwise clear any previously stored matched cmdId and return that it is not a match.
        if (this.matches(cmdId))
        {
            this.MatchedCommandId = cmdId;
            return true;
        }

        this.MatchedCommandId = 0;
        return false;
    }
    ```

## <a name="add-the-command"></a>コマンドを追加する
 DynamicMenu コンストラクターは、動的メニューやメニュー項目などのメニュー コマンドを設定する場所です。

1. *DynamicMenuPackage.cs*で、コマンド セットの GUID とコマンド ID を追加します。

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. *DynamicMenu.cs*ファイルに、次の using ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. クラスに`DynamicMenu`、プライベート フィールド**dte2**を追加します。

    ```csharp
    private DTE2 dte2;
    ```

4. プライベートな rootItemId フィールドを追加します。

    ```csharp
    private int rootItemId = 0;
    ```

5. 動的メニューのコンス トラクターで、メニュー コマンドを追加します。 次のセクションでは、コマンド ハンドラー、`BeforeQueryStatus`イベント ハンドラー、および一致述語を定義します。

    ```csharp
    private DynamicMenu(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException(nameof(package));
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            // Add the DynamicItemMenuCommand for the expansion of the root item into N items at run time.
            CommandID dynamicItemRootId = new CommandID(new Guid(DynamicMenuPackageGuids.guidDynamicMenuPackageCmdSet), (int)DynamicMenuPackageGuids.cmdidMyCommand);
            DynamicItemMenuCommand dynamicMenuCommand = new DynamicItemMenuCommand(dynamicItemRootId,
                IsValidDynamicItem,
                OnInvokedDynamicItem,
                OnBeforeQueryStatusDynamicItem);
                commandService.AddCommand(dynamicMenuCommand);
                }

        dte2 = (DTE2)this.ServiceProvider.GetService(typeof(DTE));
    }
    ```

## <a name="implement-the-handlers"></a>ハンドラの実装
 メニュー コントローラに動的メニュー項目を実装するには、動的項目がクリックされたときにコマンドを処理する必要があります。 また、メニュー項目の状態を設定するロジックも実装する必要があります。 クラスにハンドラーを追加`DynamicMenu`します。

1. **[スタートアップ プロジェクトの設定]** コマンドを実装するには、**イベント**ハンドラーを追加します。 呼び出されたコマンドのテキストと同じ名前のプロジェクトを検索し、プロパティの絶対パスを設定することでスタートアップ プロジェクトとして設定します<xref:EnvDTE.SolutionBuild.StartupProjects%2A>。

    ```csharp
    private void OnInvokedDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand invokedCommand = (DynamicItemMenuCommand)sender;
        // If the command is already checked, we don't need to do anything
        if (invokedCommand.Checked)
            return;

        // Find the project that corresponds to the command text and set it as the startup project
        var projects = dte2.Solution.Projects;
        foreach (Project proj in projects)
        {
            if (invokedCommand.Text.Equals(proj.Name))
            {
                dte2.Solution.SolutionBuild.StartupProjects = proj.FullName;
                return;
            }
        }
    }
    ```

2. イベント`OnBeforeQueryStatusDynamicItem`ハンドラーを追加します。 これは、イベントの前に呼`QueryStatus`び出されるハンドラです。 メニュー項目が "実際の" 項目であるかどうか、つまり、プレースホルダー項目ではないかどうか、および項目が既にチェックされているかどうか (プロジェクトが既にスタートアップ プロジェクトとして設定されているかどうかを示す) を決定します。

    ```csharp
    private void OnBeforeQueryStatusDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand matchedCommand = (DynamicItemMenuCommand)sender;
        matchedCommand.Enabled = true;
        matchedCommand.Visible = true;

        // Find out whether the command ID is 0, which is the ID of the root item.
        // If it is the root item, it matches the constructed DynamicItemMenuCommand,
         // and IsValidDynamicItem won't be called.
        bool isRootItem = (matchedCommand.MatchedCommandId == 0);

        // The index is set to 1 rather than 0 because the Solution.Projects collection is 1-based.
        int indexForDisplay = (isRootItem ? 1 : (matchedCommand.MatchedCommandId - (int) DynamicMenuPackageGuids.cmdidMyCommand) + 1);

        matchedCommand.Text = dte2.Solution.Projects.Item(indexForDisplay).Name;

        Array startupProjects = (Array)dte2.Solution.SolutionBuild.StartupProjects;
        string startupProject = System.IO.Path.GetFileNameWithoutExtension((string)startupProjects.GetValue(0));

        // Check the command if it isn't checked already selected
        matchedCommand.Checked = (matchedCommand.Text == startupProject);

        // Clear the ID because we are done with this item.
        matchedCommand.MatchedCommandId = 0;
    }
    ```

## <a name="implement-the-command-id-match-predicate"></a>コマンド ID 一致述部の実装

次に、一致述語を実装します。 まず、コマンド ID が有効かどうか (宣言されたコマンド ID 以上)、もう 1 つは可能なプロジェクトを指定するかどうか (ソリューション内のプロジェクト数より少ない) という 2 つの事項を決定する必要があります。

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>ソリューションに複数のプロジェクトがある場合にのみ読み込むように VSPackage を設定します。
 アクティブなソリューションに複数のプロジェクトがない場合は **、[スタートアップ プロジェクトの設定]** コマンドは意味をなさないため、VSPackage を設定して、その場合にのみ自動的に読み込むことができます。 UI<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>コンテキスト<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects>と共に使用します。 *DynamicMenuPackage.cs*ファイルで、次の属性を追加します。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>スタートアップ プロジェクトの設定コマンドをテストする
 これで、コードをテストできます。

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. 実験用インスタンスで、複数のプロジェクトがあるソリューションを開きます。

     **ソリューション エクスプローラー**のツール バーに矢印アイコンが表示されます。 展開すると、ソリューション内のさまざまなプロジェクトを表すメニュー項目が表示されます。

3. いずれかのプロジェクトをチェックすると、そのプロジェクトがスタートアップ プロジェクトになります。

4. ソリューションを閉じるか、プロジェクトが 1 つしかないソリューションを開くと、ツール バー アイコンが表示されなくなります。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
- [VSPackages がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
