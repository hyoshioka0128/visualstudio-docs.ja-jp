---
title: 'チュートリアル: コードスニペットの実装 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb720589bc9bc31b7cf2a04b05559cb9c9d46961
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201983"
---
# <a name="walkthrough-implementing-code-snippets"></a>チュートリアル: コード スニペットの実装
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コードスニペットを作成してエディター拡張機能に含めると、拡張機能のユーザーが独自のコードに追加できるようになります。  
  
 コードスニペットは、ファイルに組み込むことができるコードまたはその他のテキストの断片です。 特定のプログラミング言語用に登録されているすべてのスニペットを表示するには、[ **ツール** ] メニューの [ **コードスニペットマネージャー**] をクリックします。 スニペットをファイルに挿入するには、スニペットを配置する場所を右クリックし、[ **スニペットの挿入** ] または [ **ブロック**の挿入] をクリックして、目的のスニペットを見つけてダブルクリックします。 TAB キーまたは SHIFT + TAB キーを押してスニペットの関連部分を変更し、enter キーまたは ESC キーを押して受け入れます。 詳細については、「[Code Snippets](../ide/code-snippets.md)」を参照してください。  
  
 コードスニペットは、スニペットファイル名拡張子を持つ XML ファイルに含まれています。 スニペットには、スニペットが挿入された後に強調表示されるフィールドを含めることができます。これにより、ユーザーはそれらを見つけて変更できます。 スニペットファイルは、 **コードスニペットマネージャー** に関する情報も提供します。これにより、スニペット名が正しいカテゴリに表示されます。 スニペットスキーマの詳細については、「 [コードスニペットスキーマリファレンス](../ide/code-snippets-schema-reference.md)」を参照してください。  
  
 このチュートリアルでは、次のタスクを実行する方法について説明します。  
  
1. 特定の言語のコードスニペットを作成して登録します。  
  
2. [ **スニペットの挿入** ] コマンドをショートカットメニューに追加します。  
  
3. スニペット拡張を実装します。  
  
   このチュートリアルは、 [ステートメント入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)に関するチュートリアルに基づいています。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-and-registering-code-snippets"></a>コードスニペットの作成と登録  
 通常、コードスニペットは、登録されている言語サービスに関連付けられています。 ただし、コードスニペットを登録するためにを実装する必要はありません <xref:Microsoft.VisualStudio.Package.LanguageService> 。 代わりに、スニペットのインデックスファイルで GUID を指定し、プロジェクトに追加するで同じ GUID を使用し <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute> ます。  
  
 次の手順では、コードスニペットを作成し、特定の GUID に関連付ける方法を示します。  
  
1. 次のディレクトリ構造を作成します。  
  
    **%InstallDir%\TestSnippets\Snippets\1033\\**  
  
    ここで、 *% InstallDir%* は Visual Studio のインストールフォルダーです。 (通常、このパスはコードスニペットのインストールに使用されますが、任意のパスを指定できます)。  
  
2. \ 1033 \ フォルダーで、.xml ファイルを作成し、 **TestSnippets.xml**という名前を指定します。 (通常、この名前はスニペットのインデックスファイルに使用されますが、.xml ファイル名拡張子を持つ限り、任意の名前を指定できます)。次のテキストを追加し、プレースホルダー GUID を削除して、独自の GUID を追加します。  
  
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
  
3. スニペットフォルダー内にファイルを作成し、 **test**という名前を入力して、 `.snippet` 次のテキストを追加します。  
  
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
  
#### <a name="to-register-code-snippets-for-a-specific-guid"></a>特定の GUID のコードスニペットを登録するには  
  
1. [確認] **テスト** プロジェクトを開きます。 このプロジェクトを作成する方法の詳細については、「 [チュートリアル: ステートメント入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)」を参照してください。  
  
2. プロジェクトで、次のアセンブリへの参照を追加します。  
  
    - VisualStudio。相互運用  
  
    - VisualStudio (Microsoft. 相互運用性)  
  
    - microsoft msxml  
  
3. プロジェクトで、source.extension.vsixmanifest ファイルを開きます。  
  
4. [ **アセット** ] タブに **VsPackage** コンテンツタイプが含まれており、その **プロジェクト** がプロジェクトの名前に設定されていることを確認します。  
  
5. [作成] テストプロジェクトを選択し、[プロパティウィンドウ [ **Pkgdef ファイルの生成** ] を [ **true**] に設定します。 プロジェクトを保存します。  
  
6. 静的クラスを `SnippetUtilities` プロジェクトに追加します。  
  
     [!code-csharp[VSSDKCompletionTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#22)]
     [!code-vb[VSSDKCompletionTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#22)]  
  
7. SnippetUtilities クラスで、GUID を定義し、SnippetsIndex.xml ファイルで使用した値を指定します。  
  
     [!code-csharp[VSSDKCompletionTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#23)]
     [!code-vb[VSSDKCompletionTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#23)]  
  
8. <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>をクラスに追加し `TestCompletionHandler` ます。 この属性は、プロジェクト内の任意のパブリックまたは内部 (非静的) クラスに追加できます。 (場合によっては `using` 、VisualStudio 名前空間のステートメントを追加する必要があります)。  
  
     [!code-csharp[VSSDKCompletionTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#24)]
     [!code-vb[VSSDKCompletionTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#24)]  
  
9. プロジェクトをビルドして実行します。 プロジェクトの実行時に起動される Visual Studio の実験用インスタンスでは、先ほど登録したスニペットが**testsnippets**言語の下にある**コードスニペットマネージャー**に表示されます。  
  
## <a name="adding-the-insert-snippet-command-to-the-shortcut-menu"></a>ショートカットメニューに [スニペットの挿入] コマンドを追加する  
 [ **スニペットの挿入** ] コマンドは、テキストファイルのショートカットメニューには含まれていません。 そのため、コマンドを有効にする必要があります。  
  
#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>[スニペットの挿入] コマンドをショートカットメニューに追加するには  
  
1. `TestCompletionCommandHandler`クラスファイルを開きます。  
  
     このクラスはを実装しているため、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> メソッドで [ **スニペットの挿入** ] コマンドをアクティブにすることができ <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> ます。 コマンドを有効にする前に、このメソッドがオートメーション関数の内部で呼び出されていないことを確認してください。これは、[ **スニペットの挿入** ] コマンドをクリックすると、スニペットピッカーユーザーインターフェイス (UI) が表示されるためです。  
  
     [!code-csharp[VSSDKCompletionTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#25)]
     [!code-vb[VSSDKCompletionTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#25)]  
  
2. プロジェクトをビルドして実行します。 実験用インスタンスで、ファイル名拡張子が zzz のファイルを開き、その中の任意の場所を右クリックします。 ショートカットメニューに [ **スニペットの挿入** ] コマンドが表示されます。  
  
## <a name="implementing-snippet-expansion-in-the-snippet-picker-ui"></a>スニペットピッカー UI でのスニペット拡張の実装  
 このセクションでは、ショートカットメニューの [ **スニペットの挿入** ] をクリックしたときにスニペットピッカー UI が表示されるように、コードスニペット拡張を実装する方法について説明します。 コードスニペットは、ユーザーがコードスニペットのショートカットを入力し、TAB キーを押したときにも展開されます。  
  
 スニペットピッカー UI を表示し、ナビゲーションと挿入後のスニペットの受け入れを有効にするには、メソッドを使用し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。 挿入自体は、メソッドによって処理され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> ます。  
  
 コードスニペット拡張の実装では、レガシインターフェイスを使用し <xref:Microsoft.VisualStudio.TextManager.Interop> ます。 現在のエディタークラスからレガシコードに変換する場合は、従来のインターフェイスでは、行番号と列番号の組み合わせを使用してテキストバッファー内の場所を指定しますが、現在のクラスは1つのインデックスを使用することに注意してください。 したがって、バッファーには、それぞれに10文字 (1 文字としてカウントされる改行) を持つ3つの行が含まれている場合、3行目の4番目の文字は現在の実装では27になりますが、前の実装では行2の位置3になります。  
  
#### <a name="to-implement-snippet-expansion"></a>スニペット拡張を実装するには  
  
1. クラスを含むファイルに `TestCompletionCommandHandler` 、次のステートメントを追加し `using` ます。  
  
     [!code-csharp[VSSDKCompletionTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#26)]
     [!code-vb[VSSDKCompletionTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#26)]  
  
2. クラスが `TestCompletionCommandHandler` インターフェイスを実装するようにし <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> ます。  
  
     [!code-csharp[VSSDKCompletionTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#27)]
     [!code-vb[VSSDKCompletionTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#27)]  
  
3. クラスで `TestCompletionCommandHandlerProvider` 、をインポートし <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ます。  
  
     [!code-csharp[VSSDKCompletionTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#28)]
     [!code-vb[VSSDKCompletionTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#28)]  
  
4. コード拡張インターフェイスとにプライベートフィールドを追加し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。  
  
     [!code-csharp[VSSDKCompletionTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#29)]
     [!code-vb[VSSDKCompletionTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#29)]  
  
5. クラスのコンストラクターで `TestCompletionCommandHandler` 、次のフィールドを設定します。  
  
     [!code-csharp[VSSDKCompletionTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#30)]
     [!code-vb[VSSDKCompletionTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#30)]  
  
6. ユーザーが [ **スニペットの挿入** ] コマンドをクリックしたときにスニペットピッカーを表示するには、メソッドに次のコードを追加し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。 (この説明を読みやすくするために、ステートメント入力候補に使用される Exec () コードは表示されません。代わりに、既存のメソッドにコードのブロックが追加されます)。文字をチェックするコードの後に、次のコードブロックを追加します。  
  
     [!code-csharp[VSSDKCompletionTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#31)]
     [!code-vb[VSSDKCompletionTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#31)]  
  
7. 移動できるフィールドがスニペットにある場合、拡張が明示的に許可されるまで拡張セッションは開いたままになります。スニペットにフィールドがない場合、セッションは閉じられ、メソッドによってとして返され `null` <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A> ます。 メソッドで <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 、前の手順で追加したスニペットピッカー UI コードの後に、スニペットナビゲーションを処理する次のコードを追加します (ユーザーがスニペットの挿入後に TAB キーまたは SHIFT + TAB キーを押した場合)。  
  
     [!code-csharp[VSSDKCompletionTest#32](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#32)]
     [!code-vb[VSSDKCompletionTest#32](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#32)]  
  
8. ユーザーが対応するショートカットを入力し、TAB キーを押したときにコードスニペットを挿入するには、メソッドにコードを追加し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。 スニペットを挿入するプライベートメソッドが、後の手順で表示されます。 前の手順で追加したナビゲーションコードの後に、次のコードを追加します。  
  
     [!code-csharp[VSSDKCompletionTest#33](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#33)]
     [!code-vb[VSSDKCompletionTest#33](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#33)]  
  
9. インターフェイスのメソッドを実装し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient> ます。 この実装では、目的のメソッドはとだけです <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> 。 他のメソッドはを返すだけ <xref:Microsoft.VisualStudio.VSConstants.S_OK> です。  
  
     [!code-csharp[VSSDKCompletionTest#34](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#34)]
     [!code-vb[VSSDKCompletionTest#34](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#34)]  
  
10. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> メソッドを実装します。 展開を実際に挿入するヘルパーメソッドについては、後の手順で説明します。 は <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> 行と列の情報を提供します。この情報はから取得でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。  
  
     [!code-csharp[VSSDKCompletionTest#35](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#35)]
     [!code-vb[VSSDKCompletionTest#35](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#35)]  
  
11. 次のプライベートメソッドは、ショートカットまたはタイトルとパスに基づいて、コードスニペットを挿入します。 次 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A> に、スニペットを使用してメソッドを呼び出します。  
  
     [!code-csharp[VSSDKCompletionTest#36](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/snippetutilities.cs#36)]
     [!code-vb[VSSDKCompletionTest#36](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/snippetutilities.vb#36)]  
  
## <a name="building-and-testing-code-snippet-expansion"></a>コードスニペットの展開のビルドとテスト  
 プロジェクトでスニペットの展開が機能するかどうかをテストできます。  
  
1. ソリューションをビルドします。 デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
2. テキストファイルを開き、テキストを入力します。  
  
3. テキスト内の任意の場所を右クリックし、[ **スニペットの挿入**] をクリックします。  
  
4. [スニペットピッカー UI ( **テスト置換フィールド**)」というポップアップが表示されます。 ポップアップをダブルクリックします。  
  
     次のスニペットを挿入する必要があります。  
  
    ```  
    MessageBox.Show("first");  
    MessageBox.Show("second");  
    ```  
  
     Enter キーまたは ESC キーを押さないでください。  
  
5. TAB キーおよび SHIFT + TAB キーを押して、"first" と "second" の間を切り替えます。  
  
6. ENTER キーまたは ESC キーを押して、挿入を受け入れます。  
  
7. テキストの別の部分に「test」と入力し、TAB キーを押します。 "Test" はコードスニペットのショートカットであるため、スニペットを再び挿入する必要があります。  
  
## <a name="next-steps"></a>次の手順
