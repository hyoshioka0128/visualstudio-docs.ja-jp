---
title: メニュー コマンドを使用して拡張機能を作成する |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
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
ms.openlocfilehash: da1be8c6e00efd5d9ac94e53bf551d82d0f17ca4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739562"
---
# <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成する

このチュートリアルでは、メモ帳を起動するメニュー コマンドを使用して拡張機能を作成する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-menu-command"></a>メニュー コマンドを作成する

1. という名前の VSIX プロジェクト**を作成します**。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら、 **FirstCommand**という名前のカスタム コマンド項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログで **、[Visual C#** > **の機能拡張**] に移動し、[**カスタム コマンド**] を選択します。 ウィンドウの下部にある [**名前]** フィールドで、コマンド ファイル名を *[FirstCommand.cs]* に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

    Visual Studio の実験用インスタンスが表示されます。 実験インスタンスの詳細については、「[実験インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

::: moniker range="vs-2017"

4. 実験用インスタンスで、[**ツール** > **の拡張機能と更新]** ウィンドウを開きます。 ここで**FirstMenuCommand**拡張機能が表示されます。 (Visual Studio の作業用インスタンスで**拡張機能と更新プログラム**を開くと **、FirstMenuCommand**が表示されません。

::: moniker-end

::: moniker range=">=vs-2019"

4. 実験用インスタンスで、**拡張機能** > の管理 ウィンドウ**を**開きます。 ここで**FirstMenuCommand**拡張機能が表示されます。 (Visual Studio の作業インスタンスで**拡張機能の管理**を開くと **、FirstMenuCommand**が表示されません。

::: moniker-end

実験用インスタンスの **[ツール]** メニューに移動します。 **「FirstCommand コマンドの呼び出し」が**表示されます。 この時点で、コマンドは **、FirstCommand パッケージインサイドファーストメニューコマンド.FirstCommand.MenuItemCallback()** というメッセージ ボックスを表示します。 このコマンドからメモ帳を実際に起動する方法については、次のセクションで説明します。

## <a name="change-the-menu-command-handler"></a>メニュー コマンド ハンドラーを変更する

次に、メモ帳を起動するようにコマンド ハンドラーを更新してみましょう。

1. デバッグを停止し、Visual Studio の作業インスタンスに戻ります。 *FirstCommand.cs*ファイルを開き、次の using ステートメントを追加します。

    ```csharp
    using System.Diagnostics;
    ```

2. プライベート FirstCommand コンストラクターを検索します。 ここで、コマンドがコマンド サービスに接続され、コマンド ハンドラーが指定されます。 コマンド ハンドラーの名前を次のように StartNotepad に変更します。

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

3. メソッドを`MenuItemCallback`削除し、メモ`StartNotepad`帳を起動するメソッドを追加します。

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. 今それを試してみてください。プロジェクトのデバッグを開始し、[**ツール** > **呼び出し FirstCommand]** をクリックすると、メモ帳のインスタンスが表示されます。

    <xref:System.Diagnostics.Process>クラスのインスタンスを使用して、メモ帳だけでなく実行可能ファイルを実行できます。 たとえば`calc.exe`、で試してみてください。

## <a name="clean-up-the-experimental-environment"></a>実験環境のクリーンアップ

複数の拡張機能を開発する場合や、異なるバージョンの拡張コードで結果を調べる場合、実験環境が本来の動作を停止する可能性があります。 この場合は、リセット スクリプトを実行する必要があります。 これは **、Visual Studio の実験用インスタンスのリセット**と呼ばれ、Visual Studio SDK の一部として出荷されます。 このスクリプトは、最初から開始できるように、エクステンションへのすべての参照を実験環境から削除します。

このスクリプトは、次の 2 つの方法のいずれかで取得できます。

1. デスクトップから、「 **Visual Studio の実験用インスタンスのリセット 」** を参照してください。

2. コマンド ラインから次を実行します。

    ```xml
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>拡張機能を展開する

ツール拡張機能が必要な方法で実行できたので、友達や同僚と共有することを考えてみましょう。 これは、Visual Studio 2015 がインストールされている限り、簡単です。 あなたがしなければならないのは、あなたが構築した *.vsix*ファイルを彼らに送ることだけです。 (必ずリリースモードでビルドしてください。

この拡張子の *.vsix*ファイルは *、FirstMenuCommand*ディレクトリにあります。 具体的には、リリース構成を構築した場合、次のようになります。

*\<コード ディレクトリ>\ファーストメニュー コマンド\ファーストメニュー コマンド\ビン\リリース\ファーストメニュー コマンド.vsix*

拡張機能をインストールするには、フレンドが Visual Studio の開いているインスタンスをすべて閉じ *、.vsix*ファイルをダブルクリックして**VSIX インストーラ**を起動する必要があります。 ファイルは *%LocalAppData%\マイクロソフト\VisualStudio\<バージョン>\拡張機能*ディレクトリにコピーされます。

フレンドが Visual Studio を再び起動すると、ツール拡張機能**と更新プログラム**の FirstMenuCommand 拡張機能が**見** > つかります。 **拡張機能と更新プログラム**に移動して、拡張機能をアンインストールまたは無効にすることもできます。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、Visual Studio 拡張機能を使用して実行できる操作のほんの一部のみを示しています。 Visual Studio 拡張機能で実行できるその他の (かなり簡単な) 操作の簡単な一覧を次に示します。

1. 簡単なメニューコマンドを使うと、さらに多くの操作を行うことができます。

   1. 独自のアイコンを追加する:[メニューコマンドにアイコンを追加する](../extensibility/adding-icons-to-menu-commands.md)

   2. メニュー コマンドのテキストを[変更する: メニュー コマンドのテキストを変更する](../extensibility/changing-the-text-of-a-menu-command.md)

   3. メニュー ショートカットをコマンドに追加する:[ショートカット キーをメニュー項目にバインドする](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. さまざまな種類のコマンド、メニュー、およびツールバーを追加する:[メニューとコマンドを拡張](../extensibility/extending-menus-and-commands.md)する

3. ツール ウィンドウを追加し、組み込みの Visual Studio ツール ウィンドウを拡張する:[ツール ウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)

4. IntelliSense、コード候補、およびその他の機能を既存のコード エディターに追加する:[エディターと言語サービスを拡張する](../extensibility/extending-the-editor-and-language-services.md)

5. 拡張機能にオプションとプロパティ ページとユーザー設定を追加する:[プロパティとプロパティ ウィンドウを拡張](../extensibility/extending-properties-and-the-property-window.md)し、[ユーザー設定とオプションを拡張します。](../extensibility/extending-user-settings-and-options.md)

   その他の種類の拡張機能では、新しい種類のプロジェクトの作成 ([プロジェクトの拡張](../extensibility/extending-projects.md)) 、新しい種類のエディターの作成 ([カスタム エディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md)) 、分離シェルでの拡張機能の実装など、もう少し作業が必要です。 [Visual Studio isolated shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
