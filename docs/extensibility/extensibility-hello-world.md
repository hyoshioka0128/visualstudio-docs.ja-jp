---
title: Hello World 拡張機能のチュートリアル | Microsoft Docs
ms.date: 03/14/2019
ms.topic: tutorial
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 796cb53ea5124662c695cce55241794802f042c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85905928"
---
# <a name="tutorial---create-your-first-extension-hello-world"></a>チュートリアル - 初めての拡張機能の作成:Hello World

この Hello World の例では、Visual Studio の初めての拡張機能を作成する方法について説明します。 このチュートリアルでは、Visual Studio に新しいコマンドを追加する方法を示します。

このプロセスでは、次の方法を学習します。

* **[機能拡張プロジェクトを作成する](#create-an-extensibility-project)**
* **[カスタム コマンドを追加する](#add-a-custom-command)**
* **[ソース コードを変更する](#modify-the-source-code)**
* **[実行します](#run-it)**

この例では、Visual C# を使用して、"Say Hello World!" という 次のようなカスタム メニュー ボタンを追加します。

![Hello World コマンド](media/hello-world-say-hello-world.png)

> [!NOTE]
> この記事は、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac での拡張機能のチュートリアル](/visualstudio/mac/extending-visual-studio-mac-walkthrough)のページを参照してください。

## <a name="prerequisites"></a>前提条件

開始する前に、必要な VSIX テンプレートとサンプル コードを含む **[Visual Studio 拡張機能の開発]** ワークロードがインストールされていることを確認します。

> [!NOTE]
> Visual Studio の任意のエディション (Community、Professional、または Enterprise) を使用して、Visual Studio の機能拡張プロジェクトを作成できます。

## <a name="create-an-extensibility-project"></a>機能拡張プロジェクトを作成する

::: moniker range="vs-2017"

手順 1. **[ファイル]** メニューで **[新規作成]**  >  **[プロジェクト]** の順に選択します。

手順 2. 右上の検索ボックスに「vsix」と入力し、Visual C# の **[VSIX プロジェクト]** を選択します。 ダイアログの下部にある **[名前]** に「HelloWorld」と入力し、 **[OK]** を選択します。

![新しいプロジェクト](media/hello-world-new-project.png)

[はじめに] ページといくつかのサンプル リソースが表示されます。

このチュートリアルを中断して後で再開する必要がある場合は、 **[開始ページ]** の **[最近]** セクションで新しい HelloWorld プロジェクトを見つけることができます。

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **[ファイル]** メニューで **[新規作成]**  >  **[プロジェクト]** の順に選択します。 "vsix" を検索して、Visual C# の **[VSIX プロジェクト]** 、 **[次へ]** の順に選択します。

手順 2. **[プロジェクト名]** に「HelloWorld」と入力し、 **[作成]** を選択します。

![新しいプロジェクト](media/hello-world-new-project-2019.png)

これで、HelloWorld プロジェクトが**ソリューション エクスプローラー**に表示されます。

::: moniker-end

## <a name="add-a-custom-command"></a>カスタム コマンドを追加する

手順 1. *.vsixmanifest* マニフェスト ファイルを選択すると、説明、作成者、バージョンなど、変更可能なオプションを確認できます。

手順 2. (ソリューションではなく) プロジェクトを右クリックします。 コンテキスト メニューで、 **[追加]** 、 **[新しい項目]** の順に選択します。

手順 3. **[機能拡張]** セクションを選択し、 **[コマンド]** を選択します。

手順 4. 下部にある **[名前]** フィールドに「*Command.cs*」などのファイル名を入力します。

![カスタム コマンド](media/hello-world-vsix-command.png)

新しいコマンド ファイルが**ソリューション エクスプローラー**に表示されます。 **[リソース]** ノードの下に、コマンドに関連する他のファイルが表示されます。 たとえば、画像を変更する場合は、PNG ファイルはここに表示されます。

## <a name="modify-the-source-code"></a>ソース コードを変更する

この時点では、コマンドとボタンのテキストは自動生成されており、あまり興味深いものではありません。 変更する場合は、VSCT ファイルと CS ファイルを変更できます。

* VSCT ファイルを使用すると、コマンドの名前を変更するだけでなく、Visual Studio コマンド システム内の場所を定義することもできます。 VSCT ファイルを調べると、VSCT コードの各セクションが制御する対象を説明するコメントがあります。

* CS ファイルを使用すると、クリック ハンドラーなどのアクションを定義することができます。

::: moniker range="vs-2017"

手順 1. **ソリューション エクスプローラー**で、新しいコマンドの VSCT ファイルを見つけます。 この例では *CommandPackage.vsct* という名前です。

![command package vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **ソリューション エクスプローラー**で、拡張機能 VS パッケージの VSCT ファイルを見つけます。 この例では、*HelloWorldPackage.vsct* という名前です。

::: moniker-end

手順 2. `ButtonText` パラメーターを `Say Hello World!` に変更します。

```xml
  ...
  <Button guid="guidCommandPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidCommandPackageCmdSet" id="MyMenuGroup" />
     <Icon guid="guidImages" id="bmpPic1" />
     <Strings>
        <ButtonText>Say Hello World!</ButtonText>
     </Strings>
  </Button>
  ...
```

手順 3. **ソリューション エクスプローラー**に戻り、*Command.cs* ファイルを見つけます。 `Execute` メソッドで、文字列 `message` を `string.Format(..)` から `Hello World!` に変更します。

```csharp
  ...
  private void Execute(object sender, EventArgs e)
  {
    ThreadHelper.ThrowIfNotOnUIThread();
    string message = "Hello World!";
    string title = "Command";

    // Show a message box to prove we were here
    VsShellUtilities.ShowMessageBox(
        this.ServiceProvider,
        message,
        title,
        OLEMSGICON.OLEMSGICON_INFO,
        OLEMSGBUTTON.OLEMSGBUTTON_OK,
        OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST);
  }
  ...
```

必ず各ファイルへの変更を保存してください。

## <a name="run-it"></a>実行します

これで、Visual Studio の実験的なインスタンスでソース コードを実行できるようになりました。

手順 1. **F5** キーを押して、 **[デバッグの開始]** コマンドを実行します。 このコマンドによって、プロジェクトがビルドされ、デバッガーが開始され、**実験的なインスタンス**と呼ばれる Visual Studio の新しいインスタンスが起動されます。

::: moniker range="vs-2017"

Visual Studio のタイトル バーに**実験的なインスタンス**という単語が表示されます。

![[実験的なインスタンス] タイトル バー](media/hello-world-exp-instance.png)

::: moniker-end

手順 2. **[実験的なインスタンス]** の **[ツール]** メニューで、 **[Say Hello World!]** をクリックします。

![最終的な結果](media/hello-world-final-result.png)

新しいカスタム コマンドの出力が表示されます。この例では、画面の中央のダイアログに "**Hello World!** " が表示されます。 メッセージが表示されます。

## <a name="next-steps"></a>次のステップ

ここでは、Visual Studio 機能拡張での作業の基本について説明しました。以下を参照すると、さらに詳細を学習できます。

* [Visual Studio 拡張機能の開発を始める](starting-to-develop-visual-studio-extensions.md) - サンプル、チュートリアル。 拡張機能の公開。
* [Visual Studio 2017 SDK の新機能](what-s-new-in-the-visual-studio-2017-sdk.md) - Visual Studio 2017 の新しい拡張機能
* [Visual Studio 2019 SDK の新機能](whats-new-visual-studio-2019-sdk.md) - Visual Studio 2019 の新しい拡張機能
* [Visual Studio SDK の内部](internals/inside-the-visual-studio-sdk.md) - Visual Studio の機能拡張の詳細を確認します
