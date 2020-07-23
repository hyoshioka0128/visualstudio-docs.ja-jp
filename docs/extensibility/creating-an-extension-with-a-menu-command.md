---
title: メニューコマンドを使用して拡張機能を作成する |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7c8639ede4a01157718f0ab1a1514927e620fa8d
ms.sourcegitcommit: cb0c6e55ae560960a493df9ab56e3e9d9bc50100
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86972336"
---
# <a name="create-an-extension-with-a-menu-command"></a>メニューコマンドを使用して拡張機能を作成する

このチュートリアルでは、メモ帳を起動するメニューコマンドを使用して拡張機能を作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-menu-command"></a>メニューコマンドを作成する

1. **Firstmenucommand**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[**新しいプロジェクト**] ダイアログで見つけることができます。

::: moniker range="vs-2017"

2. プロジェクトが開いたら、 **Firstcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の  >  **機能拡張**] にアクセスし、[**カスタムコマンド**] を選択します。 ウィンドウの下部にある [**名前**] フィールドで、[コマンドファイル名] を*FirstCommand.cs*に変更します。

::: moniker-end

::: moniker range=">=vs-2019"

2. プロジェクトが開いたら、 **Firstcommand**という名前のカスタムコマンド項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の機能拡張] にアクセスし、  >  **Extensibility** [**コマンド**] を選択します。 ウィンドウの下部にある [**名前**] フィールドで、[コマンドファイル名] を*FirstCommand.cs*に変更します。

::: moniker-end

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、[実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

::: moniker range="vs-2017"

4. 実験用インスタンスで、[**ツール**  >  ] [**拡張機能と更新プログラム**] ウィンドウを開きます。 **Firstmenucommand**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで**拡張機能と更新プログラム**を開いた場合、 **firstmenucommand**は表示されません)。

::: moniker-end

::: moniker range=">=vs-2019"

4. 実験用インスタンスで、[**拡張**  >  **機能の管理**] ウィンドウを開きます。 **Firstmenucommand**拡張機能がここに表示されます。 (Visual Studio の作業インスタンスで [**拡張機能の管理**] を開いた場合、 **firstmenucommand**は表示されません)。

::: moniker-end

次に、実験用インスタンスの [**ツール**] メニューにアクセスします。 **呼び出し FirstCommand**コマンドが表示できます。 この時点で、コマンドを実行すると、 **Firstmenuin firstcommand. MenuItemCallback () の中に Firstcommand**というメッセージボックスが表示されます。 次のセクションでは、このコマンドからメモ帳を実際に起動する方法について説明します。

## <a name="change-the-menu-command-handler"></a>メニューコマンドハンドラーの変更

次に、コマンドハンドラーを更新してメモ帳を起動してみましょう。

1. デバッグを停止し、Visual Studio の作業インスタンスに戻ります。 *FirstCommand.cs*ファイルを開き、次の using ステートメントを追加します。

    ```csharp
    using System.Diagnostics;
    ```

2. プライベート FirstCommand コンストラクターを検索します。 コマンドがコマンドサービスにフックされ、コマンドハンドラーが指定されている場合は、次のようになります。 次のように、コマンドハンドラーの名前を「StartNotepad」に変更します。

    ```csharp
    private FirstCommand(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        CommandID menuCommandID = new CommandID(CommandSet, CommandId);
        // Change to StartNotepad handler.
        MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

3. メソッドを削除 `Execute` し、メソッドを追加し `StartNotepad` ます。これにより、メモ帳が開始されます。

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();

        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. では、試してみましょう。プロジェクトのデバッグを開始し、[**ツール**] [firstcommand] の順にクリックすると  >  **Invoke FirstCommand**、メモ帳のインスタンスが表示されます。

    クラスのインスタンスを使用して <xref:System.Diagnostics.Process> 、メモ帳だけでなく、任意の実行可能ファイルを実行できます。 たとえば、を使用して試してみてください `calc.exe` 。

## <a name="clean-up-the-experimental-environment"></a>実験環境のクリーンアップ

複数の拡張機能を開発している場合、または異なるバージョンの拡張コードを使用して結果を調査している場合は、実験環境が動作しなくなる可能性があります。 この場合は、リセットスクリプトを実行する必要があります。 これは、 **Visual studio の実験的なインスタンスのリセット**と呼ばれ、VISUAL studio SDK の一部として出荷されます。 このスクリプトは、拡張機能へのすべての参照を実験環境から削除するので、最初から開始できます。

このスクリプトは、次の2つの方法のいずれかで取得できます。

1. デスクトップから、[ **Visual Studio の実験用インスタンスのリセット**] を探します。

2. コマンド ラインから次を実行します。

    ```cmd
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>拡張機能をデプロイする

ツール拡張機能を希望どおりに実行できるようになったので、友人や同僚との共有について考えてみましょう。 これは、Visual Studio 2015 がインストールされている限り、簡単です。 作成した *.vsix*ファイルを送信するだけで済みます。 (リリースモードでビルドするようにしてください)。

この拡張機能の *.vsix*ファイルは、 *firstmenucommand* bin ディレクトリにあります。 具体的には、リリース構成をビルドしたことを前提として、次のようになります。

*\<code directory>\FirstMenuCommand\FirstMenuCommand\bin\Release\FirstMenuCommand.vsix*

拡張機能をインストールするには、フレンドが開いている Visual Studio のインスタンスをすべて閉じ、.vsix ファイルをダブルクリックする必要があり*ます*。これにより、 **vsix インストーラー**が表示されます。 ファイルは *%LocalAppData%\Microsoft\VisualStudio \<version> \ Extensions*ディレクトリにコピーされます。

友人が Visual Studio を再度起動すると、[**ツール**] [  >  **拡張機能と更新プログラム**] に firstmenucommand 拡張機能が表示されます。 拡張機能**と更新プログラム**にアクセスして、拡張機能をアンインストールまたは無効にすることができます。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、Visual Studio 拡張機能で実行できることのほんの一部のみを示しました。 Visual Studio 拡張機能で実行できるその他の (非常に簡単な) 項目を次に示します。

1. 単純なメニューコマンドを使用して、さらに多くのことを行うことができます。

   1. 独自のアイコンを追加[する: メニューコマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)

   2. メニューコマンドのテキストを変更する:[メニューコマンドのテキストを変更](../extensibility/changing-the-text-of-a-menu-command.md)する

   3. コマンドにメニューショートカットを追加する:[キーボードショートカットをメニュー項目にバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. さまざまな種類のコマンド、メニュー、およびツールバーを追加する:[メニューとコマンドを拡張](../extensibility/extending-menus-and-commands.md)する

3. ツールウィンドウの追加と組み込みの Visual Studio ツールウィンドウの拡張:[ツールウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)

4. IntelliSense、コード候補、およびその他の機能を既存のコードエディターに追加する:[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)

5. 拡張機能にオプションおよびプロパティページとユーザー設定を追加する:[プロパティとプロパティウィンドウを拡張](../extensibility/extending-properties-and-the-property-window.md)し、[ユーザー設定とオプションを拡張](../extensibility/extending-user-settings-and-options.md)します。

   その他の種類の拡張機能には、新しい種類のプロジェクトの作成 (プロジェクトの[拡張](../extensibility/extending-projects.md))、新しい種類のエディターの作成 ([カスタムエディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md))、分離シェルでの拡張機能の実装 ( [Visual Studio 分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)) など、さらに多くの作業が必要です。
