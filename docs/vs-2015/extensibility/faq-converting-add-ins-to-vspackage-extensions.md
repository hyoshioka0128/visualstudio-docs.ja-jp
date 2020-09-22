---
title: 'FAQ: アドインを VSPackage Extensions | に変換するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3a01d333-6e31-423f-ae06-5091a4fcb7a9
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc6ed31f96fc2021d0d9e104692f0440cfb78a5e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842053"
---
# <a name="faq-converting-add-ins-to-vspackage-extensions"></a>FAQ: アドインを VSPackage 拡張に変換する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

現在、アドインは非推奨とされます。 新しい Visual Studio 拡張機能を作成するには、VSIX 拡張機能を作成する必要があります。 ここでは、Visual Studio アドインを VSIX 拡張機能に変換する方法に関してよく寄せられる質問に対する回答を示します。  
  
> [!WARNING]
> Visual Studio 2015 以降では、C# および Visual Basic プロジェクトの場合、VSIX プロジェクトを使用し、メニューコマンド、ツールウィンドウ、および Vspackage の項目テンプレートを追加できます。 詳細については、「 [Visual Studio 2015 SDK の新機能](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md)」を参照してください。  
  
> [!IMPORTANT]
> 多くの場合、VSPackage プロジェクト項目を含む VSIX プロジェクトにアドインコードを簡単に転送できます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> メソッドで <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> を呼び出すことで、DTE オートメーション オブジェクトを取得できます。  
>   
> `DTE2 dte = (DTE2)GetService(typeof(DTE));`  
>   
> 詳細については、以下の「 [VSPackage でアドインコードを実行する方法](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_RunAddin) 」を参照してください。  
  
## <a name="what-software-do-i-need-to-develop-vsix-extensions"></a>VSIX 拡張機能を開発するために必要なソフトウェア  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="wheres-the-extension-documentation"></a>拡張機能のドキュメントはどこにありますか。  
 まず、 [Visual Studio 拡張機能の開発を開始](../extensibility/starting-to-develop-visual-studio-extensions.md)します。 ここでは、MSDN での VSSDK 拡張機能の開発に関するその他の記事について説明します。  
  
## <a name="can-i-convert-my-add-in-project-to-a-vsix-project"></a>アドインプロジェクトを VSIX プロジェクトに変換することはできますか。  
 VSIX プロジェクトで使用されているメカニズムがアドインプロジェクトのものと同じではないため、アドインプロジェクトを直接 VSIX プロジェクトに変換することはできません。 VSIX プロジェクトテンプレートに加えて、適切なプロジェクト項目テンプレートには、VSIX 拡張機能として簡単に起動して実行できるコードが多数あります。  
  
## <a name="how-do-i-start-developing-vsix-extensions"></a><a name="BKMK_StartDeveloping"></a> VSIX 拡張機能の開発を開始操作方法  
 メニューコマンドを含む VSIX を作成する方法を次に示します。  
  
#### <a name="to-make-a-vsix-extension-that-has-a-menu-command"></a>メニューコマンドを持つ VSIX 拡張機能を作成するには  
  
1. VSIX プロジェクトを作成する。 ([**クイック起動**] ウィンドウの [**ファイル**]、[**新規作成**]、[**プロジェクト**]、または [種類の**プロジェクト**])。 [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#]/[拡張機能** ] または [ **Visual Basic/機能拡張** ] を展開し、[ **VSIX プロジェクト**] を選択します。プロジェクトに **Testextension** という名前を設定し、その場所を指定します。  
  
2. **カスタムコマンド**プロジェクト項目テンプレートを追加します。 ( **ソリューションエクスプローラー** でプロジェクトノードを右クリックし、[追加]、[ **新しい項目**] の順に選択します。 Visual C# または Visual Basic の [ **新しいプロジェクト** ] ダイアログで、 **機能拡張** ノードを選択し、[ **カスタムコマンド**] を選択します)。  
  
3. F5 キーを押して、プロジェクトをデバッグ モードでビルドおよび実行します。  
  
     Visual Studio の 2 番目のインスタンスが表示されます。 この 2 番目のインスタンスは実験用インスタンスと呼ばれます。コードの記述に使用する Visual Studio のインスタンスとは設定が異なることがあります。 実験用インスタンスを初めて実行するときには、VS Online にサインインしてテーマとプロファイルを指定するよう求められます。  
  
     (実験用インスタンスの) [ **ツール** ] メニューで、 **[My Command name**] という名前のボタンが表示されます。 このボタンを選択すると、 **内部と () 内**にメッセージが表示されます。  
  
## <a name="how-can-i-run-my-add-in-code-in-a-vspackage"></a><a name="BKMK_RunAddin"></a> VSPackage でアドインコードを実行するにはどうすればよいですか。  
 通常、アドイン コードは次の 2 つの方法のどちらかで実行します。  
  
- メニュー コマンドによるトリガー (コードは `IDTCommandTarget.Exec` メソッド内にあります)  
  
- 起動時に自動的に実行 (コードは `OnConnection` イベント ハンドラー内にあります)。  
  
  VSPackage でも同じ操作を実行できます。 コールバック メソッドにアドイン コードを追加する方法を次に示します。  
  
#### <a name="to-implement-a-menu-command-in-a-vspackage"></a>VSPackage にメニュー コマンドを実装するには  
  
1. メニュー コマンドを含む VSPackage を作成します。 (詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください)。  
  
2. VSPackage の定義が含まれているファイルを開きます。 (C# プロジェクトでは、 <em>\<your project name></em>Package.cs)  
  
3. 次の `using` ステートメントをファイルに追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. `MenuItemCallback` メソッドを見つけます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトを取得するため、<xref:EnvDTE80.DTE2> の呼び出しを追加します。  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. アドインのコードを `IDTCommandTarget.Exec` メソッドに追加します。 たとえば、次のコードでは、[ **出力** ] ウィンドウに新しいペインを追加し、新しいペインに "一部のテキスト" を出力します。  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));  
       OutputWindow outputWindow = dte.ToolWindows.OutputWindow;  
  
       OutputWindowPane outputWindowPane = outputWindow.OutputWindowPanes.Add("A New Pane");  
       outputWindowPane.OutputString("Some Text");  
   }  
  
   ```  
  
6. このプロジェクトをビルドして実行します。 F5 キーを押すか、[**デバッグ**] ツールバーの [**開始**] を選択します。 Visual Studio の実験用インスタンスでは、[ **ツール** ] メニューに **[My Command name**] という名前のボタンが表示されます。 このボタンを選択すると、 **テキストの一部** が **出力** ウィンドウペインに表示されます。 ([ **出力** ] ウィンドウを開く必要がある場合があります)。  
  
   起動時にコードを実行することもできます。 ただし、VSPackage 拡張機能では通常、この方法はお勧めできません。 Visual Studio の起動時に読み込まれる拡張機能が多すぎると、起動にかかる時間がかなり長くなることがあります。 何らかの条件 (ソリューションが開いているなど) に一致した場合にのみ VSPackage を自動的に読み込むようにしておくことをお勧めします。  
  
   この手順では、ソリューションが開いているときに自動的に読み込まれる VSPackage のアドイン コードを実行する方法を示します。  
  
#### <a name="to-autoload-a-vspackage"></a>VSPackage を自動読み込みさせるには  
  
1. Visual Studio パッケージプロジェクト項目を使用して VSIX プロジェクトを作成します。 (これを行う手順については、「 [VSIX 拡張機能の開発を開始する操作方法](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping)」を参照してください。 代わりに、 **Visual Studio パッケージ** プロジェクト項目を追加してください)。VSIX プロジェクトの **testautoload**読み込みの名前を指定します。  
  
2. TestAutoloadPackage.cs を開きます。 パッケージ クラスが宣言されている行を見つけます。  
  
   ```csharp  
   public sealed class <name of your package>Package : Package  
   ```  
  
3. この行の上に、一連の属性が記述されています。 次の属性を追加します。  
  
   ```csharp  
   [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
   ```  
  
4. `Initialize()` メソッド内にブレークポイントを設定し、デバッグを開始します (F5)。  
  
5. この実験用インスタンスで、プロジェクトを開きます。 VSPackage が読み込まれ、ブレークポイントにヒットします。  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> のフィールドを使用して、VSPackage を読み込む他のコンテキストを指定できます。 詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。  
  
## <a name="how-can-i-get-the-dte-object"></a>DTE オブジェクトは入手するにはどうしたらよいですか?  
 アドインが UI (メニュー コマンド、ツールバー ボタン、ツール ウィンドウなど) を表示しない場合、VSPackage から DTE オートメーション オブジェクトを入手できる限り、コードを変更せずにそのまま使用できます。 次にその方法を示します。  
  
#### <a name="to-get-the-dte-object-from-a-vspackage"></a>VSPackage から DTE オブジェクトを取得するには  
  
1. Visual Studio パッケージ項目テンプレートを含む VSIX プロジェクトで、Package.cs ファイルを探し <em>\<project name></em> ます。 これは <xref:Microsoft.VisualStudio.Shell.Package> から派生するクラスで、Visual Studio の操作に役立ちます。 この場合、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> を使用して <xref:EnvDTE80.DTE2> オブジェクトを取得します。  
  
2. 次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
3. `Initialize` メソッドを見つけます。 このメソッドは、パッケージ ウィザードで指定したコマンドを処理します。 DTE オブジェクトを取得するため、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> の呼び出しを追加します。  
  
   ```csharp  
   DTE dte = (DTE)GetService(typeof(DTE));  
   ```  
  
   <xref:EnvDTE.DTE> オートメーション オブジェクトを取得したら、プロジェクトに残りのアドイン コードを追加できます。 <xref:EnvDTE80.DTE2> オブジェクトが必要な場合は、同じ操作を実行できます。  
  
## <a name="how-do-i-change-menu-commands-and-toolbar-buttons-in-my-add-in-to-the-vspackage-style"></a>アドインのメニュー コマンドとツールバー ボタンを VSPackage スタイルで変更するにはどうしたらよいですか?  
 VSPackage 拡張機能は、ほとんどのメニュー コマンド、ツールバー、ツールバー ボタン、その他の UI を作成するときに .vsct ファイルを使用します。 **カスタムコマンド**プロジェクト項目テンプレートでは、[**ツール**] メニューにコマンドを作成するためのオプションが用意されています。 詳細については、「 [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。  
  
 Vsct ファイルの詳細については、「 [How Vspackage Add User Interface Elements](../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。 Vsct ファイルを使用してメニュー項目、ツールバー、およびツールバーボタンを追加する方法を示すチュートリアルについては、「 [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)」を参照してください。  
  
## <a name="how-do-i-add-custom-tool-windows-in-the-vspackage-way"></a>VSPackage を使用してカスタム ツールウィンドウを追加するにはどうしたらよいですか?  
 [カスタムツールウィンドウ] プロジェクト項目テンプレートを使用すると、ツールウィンドウを作成できます。 このプロジェクト項目テンプレートの詳細については、「 [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)」を参照してください。 ツールウィンドウの詳細については、「ツールウィンドウの [拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md) 」および「ツール [ウィンドウの追加](../extensibility/adding-a-tool-window.md)」を参照してください。  
  
## <a name="how-do-i-manage-visual-studio-windows-in-the-vspackage-way"></a>VSPackage を使用して Visual Studio ウィンドウを管理するにはどうしたらよいですか?  
 Visual Studio ウィンドウを管理するアドインの場合、そのアドイン コードは VSPackage で機能します。 たとえば、この手順では、 **タスク一覧** を管理するコードを VSPackage のメソッドに追加する方法を示し `MenuItemCallback` ます。  
  
#### <a name="to-insert-window-management-code-from-an-add-in-into-a-vspackage"></a>アドインのウィンドウ管理コードを VSPackage に挿入するには  
  
1. 「 [VSIX 拡張機能の開発を開始する操作方法](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping) 」の手順に従って、メニューコマンドを持つ VSPackage を作成します。  
  
2. VSPackage の定義が含まれているファイルを開きます。 (C# プロジェクトでは、 <em>\<your project name></em>Package.cs)  
  
3. 次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. `MenuItemCallback` メソッドを見つけます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトを取得するため、<xref:EnvDTE80.DTE2> の呼び出しを追加します。  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. アドインのコードを追加します。 たとえば、 **タスク一覧**に新しいタスクを追加し、タスクの数を一覧表示して、1つのタスクを削除するコードを次に示します。  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)   
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       TaskList tl = (TaskList)dte.ToolWindows.TaskList;   
       askItem tlItem;   
  
       // Add a couple of tasks to the Task List.   
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 1.",    
           vsTaskPriority.vsTaskPriorityHigh, vsTaskIcon.vsTaskIconUser,   
           true, "", 10, true, true);  
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 2.",   
           vsTaskPriority.vsTaskPriorityLow, vsTaskIcon.vsTaskIconComment, true, "", 20, true,true);  
  
       // List the total number of task list items after adding the new task items.  
       System.Windows.Forms.MessageBox.Show("Task Item 1 description: "+tl.TaskItems.Item(2).Description);  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
  
       // Remove the second task item. The items list in reverse numeric order.   
       System.Windows.Forms.MessageBox.Show("Deleting the second task item");  
       tl.TaskItems.Item(2).Delete();  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
   }  
   ```  
  
## <a name="how-do-i-manage-projects-and-solutions-in-a-vspackage"></a>VSPackage でプロジェクトとソリューションを管理するにはどうしたらよいですか?  
 プロジェクトとソリューションを管理するアドインの場合、そのアドイン コードは VSPackage で機能します。 たとえば、スタートアップ プロジェクトを取得するコードを追加する手順を次に示します。  
  
1. 「 [VSIX 拡張機能の開発を開始する操作方法](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping) 」の手順に従って、メニューコマンドを持つ VSPackage を作成します。  
  
2. VSPackage の定義が含まれているファイルを開きます。 (C# プロジェクトでは、 <em>\<your project name></em>Package.cs)  
  
3. 次の `using` ステートメントを追加します。  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. `MenuItemCallback` メソッドを見つけます。 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> オブジェクトを取得するため、<xref:EnvDTE80.DTE2> の呼び出しを追加します。  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. アドインのコードを追加します。 たとえば、次のコードはソリューション内のスタートアップ プロジェクトの名前を取得します。 (このパッケージを実行するときには、マルチプロジェクト ソリューションが開いている必要があります。)  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       SolutionBuild2 sb = (SolutionBuild2)dte.Solution.SolutionBuild;   
       Project startupProj;   
       string msg = "";  
  
       foreach (String item in (Array)sb.StartupProjects)   
       {  
           msg += item;   
       }  
       System.Windows.Forms.MessageBox.Show("Solution startup Project: "+msg);   
       startupProj = dte.Solution.Item(msg);   
       System.Windows.Forms.MessageBox.Show("Full name of solution's startup project: "+"/n"+startupProj.FullName);   
   }  
   ```  
  
## <a name="how-do-i-set-keyboard-shortcuts-in-a-vspackage"></a>VSPackage でキーボード ショートカットを設定するにはどうしたらよいですか?  
 .vsct ファイルの `<KeyBindings>` 要素を使用します。 次の例では、`idCommand1` コマンドのキーボード ショートカットは Alt+A、`idCommand2` コマンドのキーボード ショートカットは Alt+Ctrl+A です。 キー名の構文に注意してください。  
  
```xml  
<KeyBindings>  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand1" editor="guidVSStd97" key1="A" mod1="ALT" />  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand2" editor="guidVSStd97" key1="A" mod1="CONTROL" mod2="ALT" />  
</KeyBindings>  
```  
  
## <a name="how-do-i-handle-automation-events-in-a-vspackage"></a>VSPackage でオートメーション イベントを処理するにはどうしたらよいですか?  
 VSPackage では、アドインと同様の方法でオートメーション イベントを処理します。 `OnItemRenamed` イベントを処理する方法を次のコードに示します。 (この例は、DTE オブジェクトを既に取得していることを前提としています。)  
  
```csharp  
Events2 dteEvents = (Events2)dte.Events;  
dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;   
. . .  
public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)   
{  
    string s = "[Event] Renamed " + oldName + " to " + Path.GetFileName(projItem.get_FileNames(1) + " in project " + projItem.ContainingProject.Name;   
}  
```
