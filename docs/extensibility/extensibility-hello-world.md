---
title: Hello World 拡張機能のチュートリアル |Microsoft Docs
ms.date: 03/14/2019
ms.topic: tutorial
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 796cb53ea5124662c695cce55241794802f042c0
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905928"
---
# <a name="tutorial---create-your-first-extension-hello-world"></a>チュートリアル-最初の拡張機能を作成する: Hello World

この Hello World の例では、Visual Studio の最初の拡張機能を作成する手順について説明します。 このチュートリアルでは、Visual Studio に新しいコマンドを追加する方法について説明します。

このプロセスでは、次の方法を学習します。

* **[機能拡張プロジェクトを作成する](#create-an-extensibility-project)**
* **[カスタムコマンドを追加する](#add-a-custom-command)**
* **[ソースコードを変更する](#modify-the-source-code)**
* **[実行します](#run-it)**

この例では、Visual C# を使用して、"言っ Hello World!" という名前のカスタムメニューボタンを追加します。 次のようになります。

![Hello World コマンド](media/hello-world-say-hello-world.png)

> [!NOTE]
> この記事は、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、 [Visual Studio for Mac の「拡張機能のチュートリアル](/visualstudio/mac/extending-visual-studio-mac-walkthrough)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

開始する前に、 **Visual Studio 拡張機能の開発**ワークロードがインストールされていることを確認してください。これには、必要な VSIX テンプレートとサンプルコードが含まれています。

> [!NOTE]
> Visual Studio の任意のエディション (Community、Professional、または Enterprise) を使用して、Visual Studio の機能拡張プロジェクトを作成できます。

## <a name="create-an-extensibility-project"></a>機能拡張プロジェクトを作成する

::: moniker range="vs-2017"

手順 1. **[ファイル]** メニューで **[新規作成]**  >  **[プロジェクト]** の順に選択します。

手順 2. 右上の検索ボックスに「vsix」と入力し、[Visual C#] **Vsix プロジェクト**を選択します。 ダイアログの下部にある**名前**に「HelloWorld」と入力し、[ **OK**] を選択します。

![新しいプロジェクト](media/hello-world-new-project.png)

はじめにのページといくつかのサンプルリソースが表示されます。

このチュートリアルを終了して戻す必要がある場合は、[**最近**] セクションの [**スタート] ページ**で新しい HelloWorld プロジェクトを見つけることができます。

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **[ファイル]** メニューで **[新規作成]**  >  **[プロジェクト]** の順に選択します。 "Vsix" を検索し、[Visual C#] **Vsix プロジェクト**を選択して、[**次へ**] をクリックします。

手順 2. **プロジェクト名**として「HelloWorld」と入力し、[**作成**] を選択します。

![新しいプロジェクト](media/hello-world-new-project-2019.png)

これで、**ソリューションエクスプローラー**に HelloWorld プロジェクトが表示されます。

::: moniker-end

## <a name="add-a-custom-command"></a>カスタムコマンドを追加する

手順 1. *Source.extension.vsixmanifest*マニフェストファイルを選択した場合は、[説明]、[作成者]、[バージョン] など、変更可能なオプションを確認できます。

手順 2. (ソリューションではなく) プロジェクトを右クリックします。 コンテキストメニューで、[**追加**]、[**新しい項目**] の順に選択します。

手順 3. [**機能拡張**] セクションを選択し、[**コマンド**] を選択します。

手順 4. 下部にある [**名前**] フィールドに、 *Command.cs*などのファイル名を入力します。

![カスタムコマンド](media/hello-world-vsix-command.png)

新しいコマンドファイルが**ソリューションエクスプローラー**に表示されます。 [**リソース**] ノードの下に、コマンドに関連する他のファイルが表示されます。 たとえば、画像を変更する場合は、PNG ファイルがここに表示されます。

## <a name="modify-the-source-code"></a>ソースコードを変更する

この時点で、コマンドとボタンのテキストは自動生成され、あまり興味深いものではありません。 変更する場合は、VSCT ファイルと CS ファイルを変更できます。

* VSCT ファイルでは、コマンドの名前を変更したり、Visual Studio コマンドシステム内の場所を定義したりできます。 VSCT ファイルを調べると、VSCT コードの各セクションについて説明するコメントが表示されます。

* CS ファイルでは、クリックハンドラーなどのアクションを定義できます。

::: moniker range="vs-2017"

手順 1. **ソリューションエクスプローラー**で、新しいコマンドの vsct ファイルを見つけます。 この場合、これは*Commandpackage. vsct*と呼ばれます。

![コマンドパッケージ .vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **ソリューションエクスプローラー**で、拡張機能 VS パッケージの vsct ファイルを見つけます。 この場合、 *HelloWorldPackage*という名前が付いています。

::: moniker-end

手順 2. `ButtonText`パラメーターをに変更 `Say Hello World!` します。

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

手順 3. **ソリューションエクスプローラー**に戻り、 *Command.cs*ファイルを見つけます。 メソッドで、 `Execute` 文字列を `message` からに変更し `string.Format(..)` `Hello World!` ます。

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

各ファイルに変更を保存してください。

## <a name="run-it"></a>実行します

これで、Visual Studio の実験的なインスタンスでソースコードを実行できるようになりました。

手順 1. **F5**キーを押して、[**デバッグの開始**] コマンドを実行します。 このコマンドは、プロジェクトをビルドし、デバッガーを起動して、**実験用インスタンス**と呼ばれる Visual Studio の新しいインスタンスを起動します。

::: moniker range="vs-2017"

Visual Studio のタイトルバーに "**実験的なインスタンス**" という語が表示されます。

![実験用インスタンスのタイトルバー](media/hello-world-exp-instance.png)

::: moniker-end

手順 2. **実験用インスタンス**の [**ツール**] メニューで、[ **Hello World!**] をクリックします。

![最終結果](media/hello-world-final-result.png)

新しいカスタムコマンドからの出力が表示されます。この例では、画面の中央にある、Hello World を示すダイアログが表示されます **。** メッセージが表示されます。

## <a name="next-steps"></a>次の手順

ここでは、Visual Studio の機能拡張を使用するための基本について説明しました。詳細については、こちらを参照してください。

* [Visual Studio 拡張機能の開発を開始](starting-to-develop-visual-studio-extensions.md)します。サンプル、チュートリアル。 拡張機能を公開する
* [Visual studio 2017 SDK](what-s-new-in-the-visual-studio-2017-sdk.md)の新機能-visual studio 2017 の新しい機能拡張機能
* [Visual studio 2019 SDK](whats-new-visual-studio-2019-sdk.md)の新機能-visual studio 2019 の新しい機能拡張機能
* [Visual STUDIO SDK 内](internals/inside-the-visual-studio-sdk.md)-visual Studio の機能拡張の詳細について説明します。
