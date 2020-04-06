---
title: こんにちは世界の拡張チュートリアル |マイクロソフトドキュメント
ms.date: 03/14/2019
ms.topic: conceptual
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c66f48a4b3c5948393e10f34810f3cb87c78c924
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711660"
---
# <a name="create-your-first-extension-hello-world"></a>最初の拡張機能を作成する: ハローワールド

この Hello World の例では、Visual Studio の最初の拡張機能を作成する方法について説明します。 このチュートリアルでは、Visual Studio に新しいコマンドを追加する方法を示します。

このプロセスでは、次の方法について学習します。

* **[機能拡張プロジェクトを作成する](#create-an-extensibility-project)**
* **[カスタム コマンドを追加する](#add-a-custom-command)**
* **[ソース コードを変更する](#modify-the-source-code)**
* **[実行します](#run-it)**

この例では、Visual C# を使用して"Hello World" という名前のカスタム メニュー ボタンを追加します。 これは次のようになります。

![ハローワールドコマンド](media/hello-world-say-hello-world.png)

> [!NOTE]
> この資料は、Windows の Visual Studio に適用されます。 Mac 用の Visual Studio の[チュートリアルを参照](/visualstudio/mac/extending-visual-studio-mac-walkthrough)してください。

## <a name="prerequisites"></a>必須コンポーネント

開始する前に、必要な VSIX テンプレートとサンプル コードを含む**Visual Studio 拡張機能開発**ワークロードがインストールされていることを確認してください。

> [!NOTE]
> Visual Studio の任意のエディション (コミュニティ、プロフェッショナル、またはエンタープライズ) を使用して、Visual Studio の機能拡張プロジェクトを作成できます。

## <a name="create-an-extensibility-project"></a>機能拡張プロジェクトを作成する

::: moniker range="vs-2017"

手順 1. **[ファイル]** メニューから、**[新規]** > **[プロジェクト]** の順に選択します。

手順 2. 右上の検索ボックスに「vsix」と入力し、Visual C# **VSIX プロジェクトを**選択します。 ダイアログの下部にある**名前**に「HelloWorld」と入力し **、[OK]** を選択します。

![新しいプロジェクト](media/hello-world-new-project.png)

[はじめに] ページとサンプル リソースが表示されます。

このチュートリアルを終了して、そのチュートリアルに戻る必要がある場合は、[最近] セクションのスタート**ページ**で新しい HelloWorld プロジェクトを**見**つけることができます。

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **[ファイル]** メニューから、**[新規]** > **[プロジェクト]** の順に選択します。 "vsix" を検索し、Visual C# **VSIX プロジェクト**を選択し、**次に次にします**。

手順 2. **プロジェクト名**に「HelloWorld」と入力し、[**作成**] を選択します。

![新しいプロジェクト](media/hello-world-new-project-2019.png)

**ソリューション エクスプローラー**に HelloWorld プロジェクトが表示されます。

::: moniker-end

## <a name="add-a-custom-command"></a>カスタム コマンドを追加する

手順 1. *vsixmanifest マニフェスト*ファイルを選択すると、説明、作成者、バージョンなど、変更可能なオプションを確認できます。

手順 2. プロジェクトを右クリックします (ソリューションではありません)。 コンテキスト メニューで 、[**追加**] をクリックし、[**新しいアイテム] をクリック**します。

手順 3. [**機能拡張**] セクションを選択し、[**コマンド**] を選択します。

手順 4. 下部の [**名前]** フィールドに *、Command.cs*などのファイル名を入力します。

![カスタム コマンド](media/hello-world-vsix-command.png)

新しいコマンド ファイルが**ソリューション エクスプローラ**に表示されます。 **[リソース**] ノードの下には、コマンドに関連する他のファイルがあります。 たとえば、画像を変更する場合は、PNG ファイルが表示されます。

## <a name="modify-the-source-code"></a>ソース コードを変更する

この時点で、コマンドとボタンのテキストは自動生成され、あまり興味深くありません。 変更を加える場合は、VSCT ファイルと CS ファイルを変更できます。

* VSCT ファイルは、Visual Studio のコマンド システムでコマンドの名前を変更したり、コマンドの場所を定義したりできる場所です。 VSCT ファイルを調べるにつれて、VSCT コードの各セクションが何を制御するかを説明するコメントが表示されます。

* CS ファイルは、クリック ハンドラなどのアクションを定義できる場所です。

::: moniker range="vs-2017"

手順 1. **ソリューション エクスプローラー**で、新しいコマンドの VSCT ファイルを見つけます。 この場合は、*コマンド パッケージ.vsct*と呼ばれます。

![コマンド パッケージ vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

手順 1. **ソリューション エクスプローラー**で、VS パッケージの拡張機能の VSCT ファイルを探します。 この場合は *、HelloWorldPackage.vsct*と呼ばれます。

::: moniker-end

手順 2. パラメータを`ButtonText`に`Say Hello World!`変更します。

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

手順 3. **ソリューション エクスプローラー**に戻り *、Command.cs*ファイルを見つけます。 メソッドで`Execute`、文字列`message`を から`string.Format(..)`に`Hello World!`変更します。

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

これで、Visual Studio の実験用インスタンスでソース コードを実行できます。

手順 1. **F5 キー**を押して **、[デバッグの開始]** コマンドを実行します。 このコマンドは、プロジェクトをビルドし、デバッガーを起動し **、Visual**Studio の新しいインスタンスを起動します。

::: moniker range="vs-2017"

Visual Studio のタイトル バーに **[実験用インスタンス]** という言葉が表示されます。

![実験インスタンスのタイトルバー](media/hello-world-exp-instance.png)

::: moniker-end

手順 2. **実験用インスタンス**の **[ツール**] メニューで、[**こんにちは世界!**

![最終結果](media/hello-world-final-result.png)

新しいカスタムコマンドからの出力が表示されます,この場合はHello Worldを提供する画面の中央にダイアログが表示**されます。** メッセージが表示されます。

## <a name="next-steps"></a>次の手順

Visual Studio の機能拡張を使用する際の基本について理解したので、ここで詳しく説明します。

* [Visual Studio 拡張機能の開発を開始 -](starting-to-develop-visual-studio-extensions.md)サンプル、チュートリアル。 拡張機能の公開
* [Visual Studio 2017 SDK の新機能](what-s-new-in-the-visual-studio-2017-sdk.md)- Visual Studio 2017 の新機能の機能拡張機能
* [Visual Studio 2019 SDK の新機能](whats-new-visual-studio-2019-sdk.md)- Visual Studio 2019 の新機能の機能拡張機能
* [Visual Studio SDK の内部](internals/inside-the-visual-studio-sdk.md)- Visual Studio の機能拡張の詳細を確認する
