---
title: 'チュートリアル: コードスニペットの実装 |Microsoft Docs'
description: コードスニペットを作成して、エディター拡張機能に含めることができます。 このチュートリアルを使用して、コードスニペットを作成/登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
author: leslierichardson95
ms.author: lerich
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: b21a7515f7ad4bad74088b6b580a4a3122a2e12a
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216983"
---
# <a name="walkthrough-implement-code-snippets"></a>チュートリアル: コードスニペットの実装
コードスニペットを作成してエディター拡張機能に含めると、拡張機能のユーザーが独自のコードに追加できるようになります。

 コードスニペットは、ファイルに組み込むことができるコードまたはその他のテキストの断片です。 特定のプログラミング言語用に登録されているすべてのスニペットを表示するには、[ **ツール** ] メニューの [ **コードスニペットマネージャー**] をクリックします。 スニペットをファイルに挿入するには、スニペットを配置する場所を右クリックし、[スニペットの挿入] または [ **ブロック** の挿入] をクリックして、目的のスニペットを見つけてダブルクリックします。 **Tab** キーまた **は Shift** tab キーを押して + スニペットの関連部分を変更し **、enter** キーまたは **Esc** キーを押して受け入れます。 詳細については、「 [コードスニペット](../ide/code-snippets.md)」を参照してください。

 コードスニペットは、スニペット * ファイル名拡張子を持つ XML ファイルに含まれています。 スニペットには、スニペットが挿入された後に強調表示されるフィールドを含めることができます。これにより、ユーザーはそれらを見つけて変更できます。 スニペットファイルは、 **コードスニペットマネージャー** に関する情報も提供します。これにより、スニペット名が正しいカテゴリに表示されます。 スニペットスキーマの詳細については、「 [コードスニペットスキーマリファレンス](../ide/code-snippets-schema-reference.md)」を参照してください。

 このチュートリアルでは、次のタスクを実行する方法について説明します。

1. 特定の言語のコードスニペットを作成して登録します。

2. [ **スニペットの挿入** ] コマンドをショートカットメニューに追加します。

3. スニペット拡張を実装します。

   このチュートリアルは、 [「チュートリアル: Display ステートメントの入力候補](../extensibility/walkthrough-displaying-statement-completion.md)」に基づいています。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-and-register-code-snippets"></a>コードスニペットの作成と登録
 通常、コードスニペットは、登録されている言語サービスに関連付けられています。 ただし、コードスニペットを登録するためにを実装する必要はありません <xref:Microsoft.VisualStudio.Package.LanguageService> 。 代わりに、スニペットのインデックスファイルで GUID を指定し、プロジェクトに追加するで同じ GUID を使用し <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> ます。

 次の手順では、コードスニペットを作成し、特定の GUID に関連付ける方法を示します。

1. 次のディレクトリ構造を作成します。

    **%InstallDir%\TestSnippets\Snippets\1033\\**

    ここで、 *% InstallDir%* は Visual Studio のインストールフォルダーです。 (通常、このパスはコードスニペットのインストールに使用されますが、任意のパスを指定できます)。

2. \ 1033 \ フォルダーで、 *.xml* ファイルを作成し、 **TestSnippets.xml** という名前を指定します。 (通常、この名前はスニペットのインデックスファイルに使用されますが、 *.xml* ファイル名拡張子を持つ限り、任意の名前を指定できます)。次のテキストを追加し、プレースホルダー GUID を削除して、独自の GUID を追加します。

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <SnippetCollection>
       <Language Lang="TestSnippets" Guid="{00000000-0000-0000-0000-000000000000}">
           <SnippetDir>
               <OnOff>On</OnOff>
               <Installed>true</Installed>
               <Locale>1033</Locale>
               <DirPath>%InstallRoot%\TestSnippets\Snippets\%LCID%\</DirPath>
               <LocalizedName>Snippets</LocalizedName>
           </SnippetDir>
       </Language>
   </SnippetCollection>
   ```

3. スニペットフォルダー内にファイルを作成し、 **test** という名前を入力して、 `.snippet` 次のテキストを追加します。

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <CodeSnippets  xmlns="http://schemas.microsoft.com/VisualStudio/2005/CodeSnippet">
       <CodeSnippet Format="1.0.0">
           <Header>
               <Title>Test replacement fields</Title>
               <Shortcut>test</Shortcut>
               <Description>Code snippet for testing replacement fields</Description>
               <Author>MSIT</Author>
               <SnippetTypes>
                   <SnippetType>Expansion</SnippetType>
               </SnippetTypes>
           </Header>
           <Snippet>
               <Declarations>
                   <Literal>
                     <ID>param1</ID>
                       <ToolTip>First field</ToolTip>
                       <Default>first</Default>
                   </Literal>
                   <Literal>
                       <ID>param2</ID>
                       <ToolTip>Second field</ToolTip>
                       <Default>second</Default>
                   </Literal>
               </Declarations>
               <References>
                  <Reference>
                      <Assembly>System.Windows.Forms.dll</Assembly>
                  </Reference>
               </References>
               <Code Language="TestSnippets">
                   <![CDATA[MessageBox.Show("$param1$");
        MessageBox.Show("$param2$");]]>
               </Code>
           </Snippet>
       </CodeSnippet>
   </CodeSnippets>
   ```

   次の手順は、コードスニペットを登録する方法を示しています。

### <a name="to-register-code-snippets-for-a-specific-guid"></a>特定の GUID のコードスニペットを登録するには

1. [確認] **テスト** プロジェクトを開きます。 このプロジェクトを作成する方法の詳細については、「 [チュートリアル: 表示ステートメント入力候補](../extensibility/walkthrough-displaying-statement-completion.md)」を参照してください。

2. プロジェクトで、次のアセンブリへの参照を追加します。

    - VisualStudio。相互運用

    - VisualStudio (Microsoft. 相互運用性)

    - microsoft msxml

3. プロジェクトで、 **source.extension.vsixmanifest** ファイルを開きます。

4. [ **アセット** ] タブに **VsPackage** コンテンツタイプが含まれており、その **プロジェクト** がプロジェクトの名前に設定されていることを確認します。

5. [作成] テストプロジェクトを選択し、[プロパティウィンドウ [ **Pkgdef ファイルの生成** ] を [ **true**] に設定します。 プロジェクトを保存します。

6. 静的クラスを `SnippetUtilities` プロジェクトに追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet22":::

7. SnippetUtilities クラスで、GUID を定義し、 *SnippetsIndex.xml* ファイルで使用した値を指定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet23":::

8. <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>をクラスに追加し `TestCompletionHandler` ます。 この属性は、プロジェクト内の任意のパブリックまたは内部 (非静的) クラスに追加できます。 (場合によっては `using` 、VisualStudio 名前空間のディレクティブを追加する必要があります)。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet24":::

9. プロジェクトをビルドして実行します。 プロジェクトの実行時に起動される Visual Studio の実験用インスタンスでは、先ほど登録したスニペットが **testsnippets** 言語の下にある **コードスニペットマネージャー** に表示されます。

## <a name="add-the-insert-snippet-command-to-the-shortcut-menu"></a>[スニペットの挿入] コマンドをショートカットメニューに追加する
 [ **スニペットの挿入** ] コマンドは、テキストファイルのショートカットメニューには含まれていません。 そのため、コマンドを有効にする必要があります。

#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>[スニペットの挿入] コマンドをショートカットメニューに追加するには

1. `TestCompletionCommandHandler` クラス ファイルを開きます。

     このクラスはを実装しているため、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> メソッドで [ **スニペットの挿入** ] コマンドをアクティブにすることができ <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> ます。 コマンドを有効にする前に、このメソッドがオートメーション関数の内部で呼び出されていないことを確認してください。これは、[ **スニペットの挿入** ] コマンドをクリックすると、スニペットピッカーユーザーインターフェイス (UI) が表示されるためです。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet25":::

2. プロジェクトをビルドして実行します。 実験用インスタンスで、ファイル名拡張子が *zzz* のファイルを開き、その中の任意の場所を右クリックします。 ショートカットメニューに [ **スニペットの挿入** ] コマンドが表示されます。

## <a name="implement-snippet-expansion-in-the-snippet-picker-ui"></a>スニペットピッカー UI でのスニペット拡張の実装
 このセクションでは、ショートカットメニューの [ **スニペットの挿入** ] をクリックしたときにスニペットピッカー UI が表示されるように、コードスニペット拡張を実装する方法について説明します。 コードスニペットは、ユーザーがコードスニペットのショートカットを入力し、 **tab** キーを押したときにも展開されます。

 スニペットピッカー UI を表示し、ナビゲーションと挿入後のスニペットの受け入れを有効にするには、メソッドを使用し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。 挿入自体は、メソッドによって処理され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> ます。

 コードスニペット拡張の実装では、レガシインターフェイスを使用し <xref:Microsoft.VisualStudio.TextManager.Interop> ます。 現在のエディタークラスからレガシコードに変換する場合は、従来のインターフェイスでは、行番号と列番号の組み合わせを使用してテキストバッファー内の場所を指定しますが、現在のクラスは1つのインデックスを使用することに注意してください。 したがって、バッファーには、それぞれが10文字 (1 文字としてカウントする改行) を持つ3つの行が含まれている場合、3行目の4番目の文字は現在の実装では27の位置にありますが、前の実装では行2の位置3にあります。

#### <a name="to-implement-snippet-expansion"></a>スニペット拡張を実装するには

1. クラスを含むファイルに `TestCompletionCommandHandler` 、次のディレクティブを追加し `using` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet26":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet26":::

2. クラスが `TestCompletionCommandHandler` インターフェイスを実装するようにし <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet27":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet27":::

3. クラスで `TestCompletionCommandHandlerProvider` 、をインポートし <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs" id="Snippet28":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb" id="Snippet28":::

4. コード拡張インターフェイスとにプライベートフィールドを追加し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet29":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet29":::

5. クラスのコンストラクターで `TestCompletionCommandHandler` 、次のフィールドを設定します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet30":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet30":::

6. ユーザーが [ **スニペットの挿入** ] コマンドをクリックしたときにスニペットピッカーを表示するには、メソッドに次のコードを追加し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。 (この説明を読みやすくするために、 `Exec()` ステートメント入力候補に使用されるコードは表示されません。代わりに、既存のメソッドにコードのブロックが追加されます)。文字をチェックするコードの後に、次のコードブロックを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet31":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet31":::

7. 移動できるフィールドがスニペットにある場合、拡張が明示的に許可されるまで拡張セッションは開いたままになります。スニペットにフィールドがない場合、セッションは閉じられ、メソッドによってとして返され `null` <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A> ます。 メソッドで <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 、前の手順で追加したスニペットピッカー UI コードの後に、スニペットナビゲーションを処理する次のコードを追加します (ユーザーがスニペットの挿入後に **tab** または **Shift tab キー** を押した場合 +  )。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet32":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet32":::

8. ユーザーが対応するショートカットを入力し、 **tab** キーを押したときにコードスニペットを挿入するには、メソッドにコードを追加し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。 スニペットを挿入するプライベートメソッドが、後の手順で表示されます。 前の手順で追加したナビゲーションコードの後に、次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet33":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet33":::

9. インターフェイスのメソッドを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> ます。 この実装では、目的のメソッドはとだけです <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 。 他のメソッドはを返すだけ <xref:Microsoft.VisualStudio.VSConstants.S_OK> です。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet34":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet34":::

10. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> メソッドを実装します。 展開を実際に挿入するヘルパーメソッドについては、後の手順で説明します。 は <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> 行と列の情報を提供します。この情報はから取得でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet35":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet35":::

11. 次のプライベートメソッドは、ショートカットまたはタイトルとパスに基づいて、コードスニペットを挿入します。 次 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A> に、スニペットを使用してメソッドを呼び出します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs" id="Snippet36":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb" id="Snippet36":::

## <a name="build-and-test-code-snippet-expansion"></a>コードスニペットの展開のビルドとテスト
 プロジェクトでスニペットの展開が機能するかどうかをテストできます。

1. ソリューションをビルドします。 デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

2. テキストファイルを開き、テキストを入力します。

3. テキスト内の任意の場所を右クリックし、[ **スニペットの挿入**] をクリックします。

4. [スニペットピッカー UI ( **テスト置換フィールド**)」というポップアップが表示されます。 ポップアップをダブルクリックします。

     次のスニペットを挿入する必要があります。

    ```
    MessageBox.Show("first");
    MessageBox.Show("second");
    ```

     **Enter キーまた** は **Esc** キーは押さないでください。

5. **Tab** キーまたは **Shift** tab キーを押して、 +  "first" と "second" の間を切り替えます。

6. **Enter** キーまたは **Esc** キーを押して、挿入を受け入れます。

7. テキストの別の部分に「test」と入力し、 **tab** キーを押します。"Test" はコードスニペットのショートカットであるため、スニペットを再び挿入する必要があります。

## <a name="next-steps"></a>次のステップ
