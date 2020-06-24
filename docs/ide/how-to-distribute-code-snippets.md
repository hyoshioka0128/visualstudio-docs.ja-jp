---
title: 拡張機能としてコード スニペットを配布する
ms.date: 03/21/2019
ms.topic: how-to
helpviewer_keywords:
- code snippets, distributing
ms.assetid: 5f717abd-e167-47ae-818c-6b0bae100ceb
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: c283d5ca29b67e772df2a0bb2e25dee70cd63fd3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284374"
---
# <a name="how-to-distribute-code-snippets"></a>方法: コード スニペットを配布する

コード スニペットは友人に配布することができます。友人は**コード スニペット マネージャー**を使用して、そのスニペットを自分のコンピューターにインストールできます。 ただし、配布するスニペットが複数ある場合や、スニペットをより広範に配布する場合は、スニペット ファイルを Visual Studio 拡張機能に含めることができます。 さらに、Visual Studio ユーザーはこの拡張機能をインストールしてスニペットを取得できます。

## <a name="prerequisites"></a>必須コンポーネント

**[VSIX プロジェクト]** プロジェクト テンプレートへのアクセス権を取得するために **[Visual Studio 拡張機能の開発]** ワークロードをインストールします。

![Visual Studio 拡張機能の開発ワークロード](media/vs-2019/extension-development-workload.png)

## <a name="set-up-the-extension"></a>拡張機能を設定する

この手順では、次のチュートリアルで作成したのと同じ Hello World コード スニペットを使います。「[チュートリアル: コード スニペットを作成する](../ide/walkthrough-creating-a-code-snippet.md)」を参照してください。 この記事ではスニペット XML を提供します。したがって、後に戻りスニペットを作成する必要はありません。

1. **空の VSIX プロジェクト** テンプレートから新しいプロジェクトを作成して、そのプロジェクトに **TestSnippet** という名前を付けます。

2. **TestSnippet** プロジェクトで新しい XML ファイルを追加し、*VBCodeSnippet.snippet* という名前を付けます。 内容を次の XML に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <CodeSnippets
        xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
      <CodeSnippet Format="1.0.0">
        <Header>
          <Title>Hello World VB</Title>
          <Shortcut>HelloWorld</Shortcut>
          <Description>Inserts code</Description>
          <Author>MSIT</Author>
          <SnippetTypes>
            <SnippetType>Expansion</SnippetType>
            <SnippetType>SurroundsWith</SnippetType>
          </SnippetTypes>
        </Header>
        <Snippet>
          <Code Language="VB">
            <![CDATA[Console.WriteLine("Hello, World!")]]>
          </Code>
        </Snippet>
      </CodeSnippet>
    </CodeSnippets>
    ```

### <a name="set-up-the-directory-structure"></a>ディレクトリ構造を設定する

1. **ソリューション エクスプローラー**でプロジェクト ノードを選択し、フォルダーを追加します。その名前は、**コード スニペット マネージャー**でスニペットに付けるのと同じ名前にします。 ここでは、**HelloWorldVB** になります。

2. *.snippet* ファイルを *HelloWorldVB* フォルダーに移動します。

3. **ソリューション エクスプローラー**で *.snippet* ファイルを選び、 **[プロパティ]** ウィンドウで **[ビルド アクション]** を **[コンテンツ]** に、 **[出力ディレクトリにコピー]** を **[常にコピーする]** に、 **[VSIX に含める]** を **[true]** に、それぞれ設定します。

### <a name="add-the-pkgdef-file"></a>.pkgdef ファイルを追加する

::: moniker range="vs-2017"

1. *HelloWorldVB* フォルダーにテキスト ファイルを追加し、*HelloWorldVB.pkgdef* という名前を付けます。 このファイルは、レジストリにキーを追加するために使用します。 この場合は、それによって **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Languages\CodeExpansions\Basic** キーに新しいサブキーが追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

1. *HelloWorldVB* フォルダーにテキスト ファイルを追加し、*HelloWorldVB.pkgdef* という名前を付けます。 このファイルは、レジストリにキーを追加するために使用します。 この場合は、それによって **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Languages\CodeExpansions\Basic** キーに新しいサブキーが追加されます。

::: moniker-end

2. ファイルに次の行を追加します。

    ```txt
    // Visual Basic
    [$RootKey$\Languages\CodeExpansions\Basic\Paths]
    "HelloWorldVB"="$PackageFolder$"
    ```

    このキーを調べると、さまざまな言語を指定する方法が分かります。

3. **ソリューション エクスプローラー**で *.pkgdef* ファイルを選択し、 **[プロパティ]** ウィンドウで次のように設定します。

   - **[ビルド アクション]** を **[コンテンツ]** に設定する
   - **[出力ディレクトリにコピー]** を **[常にコピーする]** に設定する
   - **[VSIX に含める]** を **true** に設定する

4. VSIX マニフェストに *.pkgdef* ファイルを資産として追加します。 **source.extension.vsixmanifest** ファイルで、 *[資産]* タブに移動し、 **[新規]** をクリックします。

5. **[新しい資産の追加]** ダイアログ ボックスで、 **[型]** を **Microsoft.VisualStudio.VsPackage** に、 **[ソース]** を **[ファイル システム上のファイル]** に、 **[パス]** を **[HelloWorldVB.pkgdef]** (ドロップダウン リストに表示される) に、それぞれ設定します。

### <a name="test-the-snippet"></a>スニペットをテストする

1. これで、コード スニペットが Visual Studio の実験用インスタンスで動作することを確認できるようになりました。 実験用インスタンスとは、コードの記述に使用する Visual Studio とは異なる、Visual Studio のもう 1 つのコピーです。 これを使用することにより、開発環境に影響を与えずに、拡張機能を処理することができます。

2. プロジェクトをビルドし、デバッグを開始します。

   Visual Studio の 2 番目のインスタンスが表示されます。

3. 実験用インスタンスで、 **[ツール]**  >  **[コード スニペット マネージャー]** の順に移動し、 **[言語]** を **[基本]** に設定します。 フォルダーの 1 つとして *HelloWorldVB* が表示されるはずです。そのフォルダーを展開すると *HelloWorldVB* スニペットを表示できます。

4. スニペットをテストします。 実験用インスタンスで、Visual Basic プロジェクトを開き、コード ファイルのいずれかを開きます。 コードの任意の場所にカーソルを置いて右クリックし、コンテキスト メニューで **[スニペットの挿入]** を選びます。

5. フォルダーの 1 つとして *HelloWorldVB* が表示されるはずです。 これをダブルクリックします。 **[スニペットの挿入: HelloWorldVB >]** ポップアップが表示されます。ここに **[HelloWorldVB]** ドロップダウン リストが表示されます。 **[HelloWorldVB]** ドロップダウン リストをクリックします。

   コード ファイルに次の行が追加されます。

    ```vb
    Console.WriteLine("Hello, World!")
    ```

## <a name="see-also"></a>関連項目

- [コード スニペット](../ide/code-snippets.md)
