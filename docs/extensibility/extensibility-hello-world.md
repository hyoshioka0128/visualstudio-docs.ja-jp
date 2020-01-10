---
title: Hello World 拡張機能のチュートリアル |Microsoft Docs
ms.date: 03/14/2019
ms.topic: conceptual
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0345d67a4202b8b267d213e0c288847e2774f722
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404129"
---
# <a name="create-your-first-extension-hello-world"></a>最初の拡張機能を作成する: Hello World

この Hello World の例では、Visual Studio の初めての拡張機能の作成手順について説明します。 このチュートリアルでは、Visual Studio に新しいコマンドを追加する方法について説明します。

学習方法は以下の手順となります。

* **[機能拡張プロジェクトの作成](#create-an-extensibility-project)**
* **[カスタム コマンドの追加](#add-a-custom-command)**
* **[ソース コードを変更](#modify-the-source-code)**
* **[実行](#run-it)**

この例ではVisual C#を使用して次に示すような「Say Hello World!」という名前のカスタム メニュー ボタンを追加します。 次のようになります。

![Hello World コマンド](media/hello-world-say-hello-world.png)

> [!NOTE]
> この記事は、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac では、次の[Visual Studio for Mac での拡張機能のチュートリアル](/visualstudio/mac/extending-visual-studio-mac-walkthrough) を参照してください。

## <a name="prerequisites"></a>Prerequisites

開始する前に、 **Visual Studio 拡張機能の開発**ワークロードがインストールされていることを確認してください。これには、必要な VSIX テンプレートとサンプルコードが含まれています。

> [!NOTE]
> Visual Studio 機能拡張プロジェクトを作成するには、Visual Studio の任意のエディション(Community、Professional、または Enterprise)を使用することができます。

## <a name="create-an-extensibility-project"></a>機能拡張プロジェクトの作成

::: moniker range="vs-2017"

手順 1. **[ファイル]** メニューで **[新規作成]**  >  **[プロジェクト]** の順に選択します。

手順 2. 右上の検索ボックスに「vsix」と入力し、ビジュアルC# **vsix プロジェクト**を選択します。 ダイアログの下部にある**名前**に「HelloWorld」と入力し、 **[OK]** を選択します。

![新しいプロジェクト](media/hello-world-new-project.png)

はじめに *Getting Started* ページといくつかのサンプル リソースが表示されます。

このチュートリアルを終了した後に再開する必要がある場合、 **スタート ページ** の **最近** セクションで HelloWorld プロジェクトを見つけられます。

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **[ファイル]** メニューで **[新規作成]**  >  **[プロジェクト]** の順に選択します。 "Vsix" を検索し、ビジュアルC# **vsix プロジェクト**を選択して、 **[次へ]** をクリックします。

手順 2. **プロジェクト名**として「HelloWorld」と入力し、 **[作成]** を選択します。

![新しいプロジェクト](media/hello-world-new-project-2019.png)

これで、**ソリューションエクスプローラー**に HelloWorld プロジェクトが表示されます。

::: moniker-end

## <a name="add-a-custom-command"></a>カスタム コマンドの追加

手順 1. *Source.extension.vsixmanifest*マニフェストファイルを選択した場合は、[説明]、[作成者]、[バージョン] など、変更可能なオプションを確認できます。

手順 2. (ソリューションではなく) プロジェクトを右クリックします。 コンテキストメニューで、 **[追加]** 、 **[新しい項目]** の順に選択します。

手順 3. **[機能拡張]** セクションを選択し、 **[コマンド]** を選択します。

手順 4. 下部にある **[名前]** フィールドに、 *Command.cs*などのファイル名を入力します。

![カスタムコマンド](media/hello-world-vsix-command.png)

新しいコマンドファイルが**ソリューションエクスプローラー**に表示されます。 **[リソース]** ノードの下に、コマンドに関連する他のファイルが表示されます。 たとえば、画像を変更する場合は、PNG ファイルがここに表示されます。

## <a name="modify-the-source-code"></a>ソース コードの変更

この時点で、コマンドとボタンのテキストは自動生成され、あまり興味深いものではありません。 変更する場合は、VSCT ファイルと CS ファイルを変更できます。

* VSCT ファイルはコマンドの名前の変更だけでなく、Visual Studioのコマンドシステムでの場所を定義します。 VSCT ファイルを調べると、VSCT コードの各セクションについて説明するコメントが表示されます。

* CS ファイルでは、クリックハンドラーなどのアクションを定義できます。

::: moniker range="vs-2017"

手順 1. **ソリューション エクスプローラー**内で新規作成したコマンドの VSCT ファイルを検索します。 今回の場合は*CommandPackage.vsct*となっています。

![コマンドパッケージ .vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **ソリューションエクスプローラー**で、拡張機能 VS パッケージの vsct ファイルを見つけます。 この場合、 *HelloWorldPackage*という名前が付いています。

::: moniker-end

手順 2. `ButtonText`パラメーターを`Say Hello World!`に変更します。

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

手順 3. **ソリューション エクスプ ローラー**に戻って、*Command.cs*ファイルを探します。 `Execute` メソッドで、文字列 `message` を `string.Format(..)` から `Hello World!`に変更します。

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

各ファイルの変更が保存されているか確認してください。

## <a name="run-it"></a>実行

これで、Visual Studio の実験的なインスタンスでソースコードを実行できるようになりました。

手順 1. **F5**キーを押して、 **[デバッグの開始]** コマンドを実行します。 このコマンドは、プロジェクトをビルドし、デバッガーを起動して、**実験用インスタンス**と呼ばれる Visual Studio の新しいインスタンスを起動します。

::: moniker range="vs-2017"

Visual Studioのタイトル バーには**実験的なインスタンス**と表示されます。

![実験的なインスタンスのタイトル バー](media/hello-world-exp-instance.png)

::: moniker-end

手順 2. **実験用インスタンス**の **[ツール]** メニューで、 **[Hello World!]** をクリックします。

![最終結果](media/hello-world-final-result.png)

新規作成したカスタム コマンドからの出力、この場合では画面の中央のダイアログ ボックスに **Hello World!** というメッセージが返されることはありません。

## <a name="next-steps"></a>次のステップ:

Visual Studio 拡張機能 の作業の基礎を知ることができたので、以下でさらに学習ができます。

* [Visual Studio 拡張機能の開発を開始](starting-to-develop-visual-studio-extensions.md)します。サンプル、チュートリアル。 拡張機能を公開する
* [Visual studio 2017 SDK](what-s-new-in-the-visual-studio-2017-sdk.md)の新機能-visual studio 2017 の新しい機能拡張機能
* [Visual studio 2019 SDK](whats-new-visual-studio-2019-sdk.md)の新機能-visual studio 2019 の新しい機能拡張機能
* [Visual STUDIO SDK 内](internals/inside-the-visual-studio-sdk.md)-visual Studio の機能拡張の詳細について説明します。
