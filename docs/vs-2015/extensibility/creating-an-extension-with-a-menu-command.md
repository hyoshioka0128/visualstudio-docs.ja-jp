---
title: メニューコマンドを使用して拡張機能を作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
caps.latest.revision: 57
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e3bbf6b3b1ed2565d5e58806bd0935f713ba5bfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62572888"
---
# <a name="creating-an-extension-with-a-menu-command"></a>メニュー コマンドを使用した拡張機能の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、メモ帳を起動するメニューコマンドを使用して拡張機能を作成する方法について説明します。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-menu-command"></a>メニューコマンドの作成  
  
1. **Firstmenucommand**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#]/[拡張機能**] で見つけることができます。  
  
2. プロジェクトが開いたら、 **Firstcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 [ **新しい項目の追加** ] ダイアログで、[ **Visual C#]/[拡張機能** ] にアクセスし、[ **カスタムコマンド**] を選択します。 ウィンドウの下部にある [ **名前** ] フィールドで、[コマンドファイル名] を **FirstCommand.cs**に変更します。  
  
3. プロジェクトをビルドし、デバッグを開始します。  
  
     Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。  
  
4. 実験用インスタンスで、[ツール]、[  **拡張機能と更新プログラム** ] ウィンドウの順に開きます。 **Firstmenucommand**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで **拡張機能と更新プログラム** を開いた場合、 **firstmenucommand**は表示されません)。  
  
     次に、実験用インスタンスの [ **ツール** ] メニューにアクセスします。 **呼び出し FirstCommand**コマンドが表示できます。 この時点で、"FirstCommandPackage in Firstcommandpackage. MenuItemCallback ()" というメッセージボックスが表示されます。 次のセクションでは、このコマンドからメモ帳を実際に起動する方法について説明します。  
  
## <a name="changing-the-menu-command-handler"></a>メニューコマンドハンドラーの変更  
 次に、コマンドハンドラーを更新してメモ帳を起動してみましょう。  
  
1. デバッグを停止し、Visual Studio の作業インスタンスに戻ります。 FirstCommand.cs ファイルを開き、次の using ステートメントを追加します。  
  
    ```csharp  
    using System.Diagnostics;  
    ```  
  
2. プライベート FirstCommand コンストラクターを検索します。 コマンドがコマンドサービスにフックされ、コマンドハンドラーが指定されている場合は、次のようになります。 次のように、コマンドハンドラーの名前を「StartNotepad」に変更します。  
  
    ```csharp  
    private FirstCommand(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
         OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(CommandSet, CommandId);  
            // Change to StartNotepad handler.  
            MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
3. MenuItemCallback メソッドを削除し、メモ帳を開始するための StartNotepad メソッドを追加します。  
  
    ```csharp  
    private void StartNotepad(object sender, EventArgs e)  
    {  
        Process proc = new Process();  
        proc.StartInfo.FileName = "notepad.exe";  
        proc.Start();  
    }  
    ```  
  
4. では、試してみましょう。プロジェクトのデバッグを開始し、[ツール]、[ **FirstCommand の呼び出し**] の順にクリックすると、メモ帳のインスタンスが表示されます。  
  
     クラスのインスタンスを使用して <xref:System.Diagnostics.Process> 、メモ帳だけでなく、任意の実行可能ファイルを実行できます。 たとえば、calc.exe で試してみてください。  
  
## <a name="cleaning-up-the-experimental-environment"></a>実験環境のクリーンアップ  
 複数の拡張機能を開発している場合、または異なるバージョンの拡張コードを使用して結果を調査している場合は、実験環境が動作しなくなる可能性があります。 この場合は、リセットスクリプトを実行する必要があります。 これは、 **Visual studio 2015 の実験用インスタンスのリセット**と呼ばれ、VISUAL studio SDK の一部として出荷されます。 このスクリプトは、拡張機能へのすべての参照を実験環境から削除するので、最初から開始できます。  
  
 このスクリプトは、次の2つの方法のいずれかで取得できます。  
  
1. デスクトップから、 **Visual Studio 2015 の実験的なインスタンスのリセット**を探します。  
  
2. コマンド ラインから次を実行します。  
  
    ```  
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=14.0 /RootSuffix=Exp && PAUSE  
  
    ```  
  
## <a name="deploying-your-extension"></a>拡張機能のデプロイ  
 ツール拡張機能を希望どおりに実行できるようになったので、友人や同僚との共有について考えてみましょう。 これは、Visual Studio 2015 がインストールされている限り、簡単です。 作成した .vsix ファイルを送信するだけで済みます。 (リリースモードでビルドするようにしてください)。  
  
 この拡張機能の .vsix ファイルは、FirstMenuCommand bin ディレクトリにあります。 具体的には、リリース構成をビルドしたことを前提として、次のようになります。  
  
 **\<code directory>\FirstMenuCommand\FirstMenuCommand\bin\Release\ FirstMenuCommand .vsix**  
  
 拡張機能をインストールするには、フレンドが開いている Visual Studio のインスタンスをすべて閉じ、.vsix ファイルをダブルクリックする必要があります。これにより、 **Vsix インストーラー**が表示されます。 ファイルは **%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions** ディレクトリにコピーされます。  
  
 友人が Visual Studio を再度起動すると、[ツール]、[ **拡張機能と更新プログラム**] で FirstMenuCommand 拡張機能を見つけることができます。 拡張機能 **と更新プログラム** にアクセスして、拡張機能をアンインストールまたは無効にすることができます。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルでは、Visual Studio 拡張機能で実行できることのほんの一部のみを示しました。 Visual Studio 拡張機能で実行できるその他の (非常に簡単な) 項目を次に示します。  
  
1. 単純なメニューコマンドを使用して、さらに多くのことを行うことができます。  
  
   1. 独自のアイコンを追加 [する: メニューコマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)  
  
   2. メニューコマンドのテキストを変更する:[メニューコマンドのテキスト](../extensibility/changing-the-text-of-a-menu-command.md)を変更する  
  
   3. コマンドにメニューショートカットを追加する: [キーボードショートカットをメニュー項目にバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
  
2. さまざまな種類のコマンド、メニュー、およびツールバーを追加する: [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)  
  
3. ツールウィンドウを追加し、組み込みの Visual Studio ツールウィンドウを拡張する: [ツールウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)  
  
4. IntelliSense、コード候補、およびその他の機能を既存のコードエディターに追加する: [エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)  
  
5. 拡張機能へのオプション、プロパティページ、およびユーザー設定の追加: [プロパティとプロパティウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md) と [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)  
  
   その他の種類の拡張機能には、新しい種類のプロジェクトの作成 (プロジェクトの[拡張](../extensibility/extending-projects.md))、新しい種類のエディターの作成 ([カスタムエディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md))、分離シェルでの拡張機能の実装 ( [Visual Studio 分離シェル](../extensibility/visual-studio-isolated-shell.md)) など、さらに多くの作業が必要です。
