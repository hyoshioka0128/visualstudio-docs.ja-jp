---
title: メニュー項目を動的に追加する |Microsoft Docs
description: DynamicItemStart コマンドフラグを使用して、実行時にメニュー項目を追加する方法について説明します。 この記事では、Visual Studio ソリューションでスタートアッププロジェクトを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fa85d5b5cf4b99840e181fb24b5913ff72a3fee0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070337"
---
# <a name="dynamically-add-menu-items"></a>メニュー項目を動的に追加する
実行時にメニュー項目を追加するには、 `DynamicItemStart` Visual Studio のコマンドテーブル (*vsct*) ファイルのプレースホルダーボタンの定義に対してコマンドフラグを指定し、(コード内で) コマンドを表示および処理するメニュー項目の数を定義します。 VSPackage が読み込まれると、プレースホルダーは動的メニュー項目に置き換えられます。

 Visual Studio では、最近使用した (MRU) リストに動的なリストが使用 **さ** れます。この一覧には、最近開いたドキュメントの名前と、現在開いているウィンドウの名前が表示される **windows** の一覧が表示されます。   `DynamicItemStart`コマンド定義のフラグは、VSPackage が開かれるまで、コマンドがプレースホルダーであることを指定します。 VSPackage を開くと、プレースホルダーは実行時に作成され、動的リストに追加される0個以上のコマンドに置き換えられます。 VSPackage が開かれるまで、動的なリストが表示されるメニュー上の位置を確認できない場合があります。  動的リストを設定するために、Visual Studio は VSPackage に対して、最初の文字がプレースホルダーの ID と同じであることを示す ID を持つコマンドを検索するように要求します。 一致するコマンドが見つかると、Visual Studio は動的な一覧にコマンドの名前を追加します。 次に、ID を増やし、動的なコマンドがなくなるまで、動的リストに追加する別の一致するコマンドを探します。

 このチュートリアルでは、[ **ソリューションエクスプローラー** ] ツールバーのコマンドを使用して、Visual Studio ソリューションのスタートアッププロジェクトを設定する方法について説明します。 アクティブソリューション内のプロジェクトの動的ドロップダウンリストを持つメニューコントローラーを使用します。 ソリューションが開かれていない場合や、開いているソリューションにプロジェクトが1つしかない場合にこのコマンドが表示されないようにするには、ソリューションに複数のプロジェクトがある場合にのみ、VSPackage を読み込みます。

 *Vsct* ファイルの詳細については、「 [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニューコマンドを使用して拡張機能を作成する

1. という名前の VSIX プロジェクトを作成 `DynamicMenuItems` します。

2. プロジェクトが開いたら、カスタムコマンド項目テンプレートを追加し、 **Dynamicmenu** という名前を指定します。 詳細については、「 [メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

## <a name="setting-up-the-elements-in-the-vsct-file"></a>*Vsct* ファイル内の要素の設定
 ツールバーに動的メニュー項目を含むメニューコントローラーを作成するには、次の要素を指定します。

- 2つのコマンドグループ。1つはメニューコントローラーを格納し、もう1つはドロップダウンリストにメニュー項目を格納します。

- 型の1つのメニュー要素 `MenuController`

- 2つのボタン。メニュー項目のプレースホルダーとして機能し、もう1つは、ツールバーのアイコンとツールヒントを提供します。

1. *DynamicMenuPackage* で、コマンド id を定義します。 シンボルのセクションにアクセスし、 **Guiddynamicmenupackagecmdset** guidsymbol ブロックの idsymbol 要素を置き換えます。 IDSymbol 要素は、メニューコントローラー、プレースホルダーコマンド、およびアンカーコマンドの2つのグループに対して定義する必要があります。

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

2. [グループ] セクションで、既存のグループを削除し、先ほど定義した2つのグループを追加します。

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

     MenuController を追加します。 常に表示されないため、DynamicVisibility コマンドフラグを設定します。 ButtonText は表示されません。

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

3. 2つのボタンを追加します。1つは、動的メニュー項目のプレースホルダーとして、もう1つは MenuController のアンカーとして使用します。

     プレースホルダーボタンの親は **Mymenuコントローラーグループ** です。 DynamicItemStart、DynamicVisibility、および TextChanges の各コマンドフラグをプレースホルダーボタンに追加します。 ButtonText は表示されません。

     アンカーボタンは、アイコンとツールヒントのテキストを保持します。 アンカーボタンの親は、 **Mymenuコントローラーグループ** でもあります。 NoShowOnMenuController コマンドフラグを追加して、ボタンが実際にメニューコントローラーのドロップダウンに表示されないようにします。また、FixMenuController コマンドフラグを使用して、永続的なアンカーにします。

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

4. ( *Resources* フォルダー内の) プロジェクトにアイコンを追加し、そのファイルへの参照を *vsct* ファイルに追加します。 このチュートリアルでは、プロジェクトテンプレートに含まれている矢印アイコンを使用します。

5. VisibilityConstraints セクションを、Symbols セクションの直前の Commands セクションの外側に追加します。 (シンボルの後に追加すると、警告が表示される場合があります)。このセクションでは、複数のプロジェクトを含むソリューションが読み込まれた場合にのみ、メニューコントローラーが表示されるようにします。

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>動的メニューコマンドを実装する
 を継承する動的メニューコマンドクラスを作成し <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> ます。 この実装では、コンストラクターは、照合コマンドに使用する述語を指定します。 この述語を使用して、呼び出すコマンドを識別するプロパティを設定するには、メソッドをオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> ます。

1. *Dynamicitemmenucommand .cs* という名前の新しい C# クラスファイルを作成し、次のようにを継承する **Dynamicitemmenucommand** という名前のクラスを追加し <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> ます。

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

3. 次のように、一致述語を格納するプライベートフィールドを追加します。

    ```csharp
    private Predicate<int> matches;

    ```

4. コンストラクターを継承するコンストラクターを追加 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> し、コマンドハンドラーとハンドラーを指定し <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> ます。 次のコマンドと一致する述語を追加します。

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

5. 一致する <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> 述語を呼び出してプロパティを設定するように、メソッドをオーバーライドし <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> ます。

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

## <a name="add-the-command"></a>コマンドを追加します。
 DynamicMenu コンストラクターは、動的メニューやメニュー項目など、メニューコマンドを設定する場所です。

1. *DynamicMenuPackage* で、コマンドセットの GUID とコマンド ID を追加します。

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. *Dynamicmenu .cs* ファイルで、次の using ディレクティブを追加します。

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. クラスに `DynamicMenu` 、プライベートフィールド **dte2** を追加します。

    ```csharp
    private DTE2 dte2;
    ```

4. プライベート rootItemId フィールドを追加します。

    ```csharp
    private int rootItemId = 0;
    ```

5. DynamicMenu コンストラクターにメニューコマンドを追加します。 次のセクションでは、コマンドハンドラー、 `BeforeQueryStatus` イベントハンドラー、および一致述語を定義します。

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

## <a name="implement-the-handlers"></a>ハンドラーを実装する
 メニューコントローラーに動的メニュー項目を実装するには、動的項目がクリックされたときにコマンドを処理する必要があります。 メニュー項目の状態を設定するロジックを実装する必要もあります。 ハンドラーをクラスに追加し `DynamicMenu` ます。

1. [ **スタートアッププロジェクトの設定** ] コマンドを実装するには、 **OnInvokedDynamicItem** イベントハンドラーを追加します。 このメソッドは、呼び出されたコマンドのテキストと同じ名前を持つプロジェクトを検索し、プロパティの絶対パスを設定することによって、スタートアッププロジェクトとして設定し <xref:EnvDTE.SolutionBuild.StartupProjects%2A> ます。

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

2. `OnBeforeQueryStatusDynamicItem`イベントハンドラーを追加します。 これは、イベントの前に呼び出されるハンドラーです `QueryStatus` 。 このメソッドは、メニュー項目が "実際" の項目 (プレースホルダー項目ではない) であるかどうか、および項目が既にチェックされている (つまり、プロジェクトがスタートアッププロジェクトとして設定されている) かどうかを判断します。

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

## <a name="implement-the-command-id-match-predicate"></a>コマンド ID の一致述語を実装します。

次に、match 述語を実装します。 まず、コマンド ID が有効である (宣言されたコマンド ID 以上である) かどうか、2つ目の方法 (ソリューション内のプロジェクト数よりも小さい) があるかどうかを判断する必要があります。

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>ソリューションに複数のプロジェクトがある場合にのみ VSPackage を読み込むように設定する
 **スタートアッププロジェクトの設定** コマンドは、アクティブなソリューションに複数のプロジェクトが含まれていなければ意味がないため、その場合にのみ、VSPackage を自動読み込みに設定できます。 を <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> UI コンテキストと共に使用し <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects> ます。 *DynamicMenuPackage* ファイルで、次の属性を DynamicMenuPackage クラスに追加します。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>[スタートアッププロジェクトの設定] コマンドをテストする
 これで、コードをテストできるようになりました。

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

2. 実験用インスタンスで、複数のプロジェクトを含むソリューションを開きます。

     **ソリューションエクスプローラー** ツールバーに矢印アイコンが表示されます。 展開すると、ソリューション内の異なるプロジェクトを表すメニュー項目が表示されます。

3. プロジェクトの1つを確認すると、それがスタートアッププロジェクトになります。

4. ソリューションを閉じるか、プロジェクトが1つしかないソリューションを開くと、ツールバーのアイコンが非表示になります。

## <a name="see-also"></a>こちらもご覧ください
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
- [Vspackage のユーザーインターフェイス要素の追加方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
