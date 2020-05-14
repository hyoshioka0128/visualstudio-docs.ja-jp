---
title: 'チュートリアル: コード スニペットの実装 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: adbc5382-d170-441c-9fd0-80faa1816478
author: acangialosi
ms.author: anthc
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: ba1b6e0852c1ec1b306938b791eed78e79d211ce
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697097"
---
# <a name="walkthrough-implement-code-snippets"></a>チュートリアル: コード スニペットを実装する
コード スニペットを作成し、エディター拡張機能に含めることができるので、拡張機能のユーザーがコードに追加できます。

 コード スニペットは、ファイルに組み込むことができるコードやその他のテキストの断片です。 特定のプログラミング言語に登録されているすべてのスニペットを表示するには、[**ツール**] メニューの [コード**スニペット マネージャ**] をクリックします。 ファイルにスニペットを挿入するには、スニペットを挿入する場所を右クリックし、[スニペットの挿入] または **[一緒に囲む**] をクリックし、スニペットをダブルクリックします。 **Tab**キーまたは**Shift**+**Tab キー**を押してスニペットの関連部分を変更し **、Enter**キーまたは**Esc キー**を押してそれを受け入れます。 詳細については、「コード[スニペット](../ide/code-snippets.md)」を参照してください。

 コード スニペットは、.snippet* ファイル名拡張子を持つ XML ファイルに含まれています。 スニペットには、スニペットを挿入した後に強調表示されるフィールドを含めることができるため、ユーザーは検索して変更できます。 スニペット ファイルには、スニペット名を正しいカテゴリに表示できるように **、コード スニペット マネージャー**の情報も提供します。 スニペット スキーマの詳細については、「[コード スニペット スキーマ リファレンス](../ide/code-snippets-schema-reference.md)」を参照してください。

 このチュートリアルでは、次のタスクを実行する方法について説明します。

1. 特定の言語のコード スニペットを作成および登録します。

2. ショートカット メニューに **[スニペットの挿入]** コマンドを追加します。

3. スニペットの拡張を実装します。

   このチュートリアルは[、「チュートリアル: ステートメントの入力候補を表示」に](../extensibility/walkthrough-displaying-statement-completion.md)基づいています。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-and-register-code-snippets"></a>コード スニペットの作成と登録
 通常、コード スニペットは登録済みの言語サービスに関連付けられます。 ただし、コード スニペットを登録するために<xref:Microsoft.VisualStudio.Package.LanguageService>を実装する必要はありません。 代わりに、スニペット インデックス ファイルで GUID を指定し、プロジェクトに追加<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>するのと同じ GUID を使用します。

 次の手順では、コード スニペットを作成し、それらを特定の GUID に関連付ける方法を示します。

1. 次のディレクトリ構造を作成します。

    **%インストールディレクトリ%\テストスニペット\スニペット\1033\\**

    %*インストールディレクトリ%* は、Visual Studio のインストール フォルダーです。 (このパスは通常、コード スニペットのインストールに使用されますが、任意のパスを指定できます)。

2. \1033\ フォルダーに *.xml*ファイルを作成し **、TestSnippets.xml という名前を付けます**。 (この名前は通常、スニペット インデックス ファイルに使用されますが、*拡張子が .xml*である限り、任意の名前を指定できます)。次のテキストを追加し、プレースホルダーの GUID を削除して独自の GUID を追加します。

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

3. スニペット フォルダーにファイルを作成し **、test**`.snippet`という名前を付けてから、次のテキストを追加します。

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

   次の手順は、コード スニペットを登録する方法を示しています。

### <a name="to-register-code-snippets-for-a-specific-guid"></a>特定の GUID のコード スニペットを登録するには

1. **完了テスト**プロジェクトを開きます。 このプロジェクトの作成方法については、「 チュートリアル[: ステートメント入力候補を表示](../extensibility/walkthrough-displaying-statement-completion.md)する 」を参照してください。

2. プロジェクトで、次のアセンブリへの参照を追加します。

    - 相互運用機能

    - のテキスト マネージャー.8.0

    - をクリックします。

3. プロジェクトで、**ソース.拡張子.vsixmanifestファイルを**開きます。

4. [**アセット**] タブに**VsPackage**コンテンツ タイプが含まれていること、および**プロジェクト**がプロジェクトの名前に設定されていることを確認します。

5. 完了テスト プロジェクトを選択し、プロパティ ウィンドウで**Pkgdef ファイルの生成**を**true**に設定します。 プロジェクトを保存します。

6. プロジェクトに静的`SnippetUtilities`クラスを追加します。

     [!code-csharp[VSSDKCompletionTest#22](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_1.cs)]
     [!code-vb[VSSDKCompletionTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_1.vb)]

7. クラスで、GUID を定義し、*スニペットインデックス.xml*ファイルで使用した値を指定します。

     [!code-csharp[VSSDKCompletionTest#23](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_2.cs)]
     [!code-vb[VSSDKCompletionTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_2.vb)]

8. クラスに<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>を`TestCompletionHandler`追加します。 この属性は、プロジェクト内の任意のパブリック クラスまたは内部 (非静的) クラスに追加できます。 (名前空間の`using`ディレクティブを追加する必要があります)。

     [!code-csharp[VSSDKCompletionTest#24](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_3.cs)]
     [!code-vb[VSSDKCompletionTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_3.vb)]

9. プロジェクトをビルドして実行します。 プロジェクトの実行時に開始される Visual Studio の実験用インスタンスでは、登録したスニペットが**TestSnippets**言語の**下のコード スニペット マネージャー**に表示されます。

## <a name="add-the-insert-snippet-command-to-the-shortcut-menu"></a>ショートカット メニューに [スニペットの挿入] コマンドを追加する
 [**スニペットの挿入]** コマンドは、テキスト ファイルのショートカット メニューには含まれません。 したがって、コマンドを有効にする必要があります。

#### <a name="to-add-the-insert-snippet-command-to-the-shortcut-menu"></a>ショートカット メニューに [スニペットの挿入] コマンドを追加するには

1. クラス`TestCompletionCommandHandler`ファイルを開きます。

     このクラスは<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>実装されているため、メソッドで **[スニペットの挿入**]<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>コマンドをアクティブにできます。 コマンドを有効にする前に、このメソッドがオートメーション関数内で呼び出されないことを確認**Insert Snippet**します。

     [!code-csharp[VSSDKCompletionTest#25](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_4.cs)]
     [!code-vb[VSSDKCompletionTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_4.vb)]

2. プロジェクトをビルドして実行します。 実験用インスタンスで *、.zzz*ファイル名拡張子を持つファイルを開き、そのファイル内の任意の場所を右クリックします。 [**スニペットの挿入]** コマンドがショートカット メニューに表示されます。

## <a name="implement-snippet-expansion-in-the-snippet-picker-ui"></a>スニペット ピッカー UI でスニペット展開を実装する
 このセクションでは、コード スニペットの展開を実装して、ショートカット メニューの **[スニペットの挿入**] をクリックしたときにスニペット ピッカー UI が表示されるようにする方法を示します。 コード スニペットは、ユーザーがコード スニペットのショートカットを入力し **、Tab**キーを押したときにも展開されます。

 スニペット ピッカー UI を表示し、ナビゲーションおよび挿入後のスニペットの受け<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>入れを有効にするには、このメソッドを使用します。 挿入自体はメソッドによって処理されます<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>。

 コード スニペット拡張の実装では、<xref:Microsoft.VisualStudio.TextManager.Interop>レガシ インターフェイスを使用します。 現在のエディター クラスからレガシ コードに変換する場合、レガシ インターフェイスでは行番号と列番号の組み合わせを使用してテキスト バッファー内の場所を指定しますが、現在のクラスでは 1 つのインデックスが使用されます。 したがって、バッファーにそれぞれ 10 文字 (1 文字としてカウントされる改行) がある 3 行の場合、3 行目の 4 番目の文字は現在の実装では 27 桁目になりますが、古い実装では 2 行目、3 桁目になります。

#### <a name="to-implement-snippet-expansion"></a>スニペット展開を実装するには

1. クラスを含むファイルに`TestCompletionCommandHandler`、次`using`のディレクティブを追加します。

     [!code-csharp[VSSDKCompletionTest#26](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_5.cs)]
     [!code-vb[VSSDKCompletionTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_5.vb)]

2. クラスに`TestCompletionCommandHandler`インターフェイスを実装<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient>させる。

     [!code-csharp[VSSDKCompletionTest#27](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_6.cs)]
     [!code-vb[VSSDKCompletionTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_6.vb)]

3. クラスで`TestCompletionCommandHandlerProvider`、 をインポート<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>します。

     [!code-csharp[VSSDKCompletionTest#28](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_7.cs)]
     [!code-vb[VSSDKCompletionTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_7.vb)]

4. コード拡張インターフェイスと<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.

     [!code-csharp[VSSDKCompletionTest#29](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_8.cs)]
     [!code-vb[VSSDKCompletionTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_8.vb)]

5. クラスのコンストラクターで`TestCompletionCommandHandler`、次のフィールドを設定します。

     [!code-csharp[VSSDKCompletionTest#30](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_9.cs)]
     [!code-vb[VSSDKCompletionTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_9.vb)]

6. ユーザーが [スニペットの挿入] コマンドをクリックしたときに**スニペット**ピッカーを表示するには、次<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>のコードをメソッドに追加します。 (この説明を読みやすくするために、ステートメント`Exec()`入力候補に使用されるコードは表示されず、代わりに既存のメソッドにコード ブロックが追加されます。文字をチェックするコードの後に、次のコード ブロックを追加します。

     [!code-csharp[VSSDKCompletionTest#31](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_10.cs)]
     [!code-vb[VSSDKCompletionTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_10.vb)]

7. スニペットにナビゲートできるフィールドがある場合、展開セッションは展開が明示的に受け入れられるまで開いたままになります。スニペットにフィールドがない場合、セッションは閉じられ、`null`<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.InvokeInsertionUI%2A>メソッドによって返されます。 このメソッド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>では、前の手順で追加したスニペット ピッカーの UI コードの後に、スニペット ナビゲーションを処理する次のコードを追加します (ユーザーがスニペットの挿入後に**Tab キー**または**Shift**+**Tab**キーを押したとき)。

     [!code-csharp[VSSDKCompletionTest#32](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_11.cs)]
     [!code-vb[VSSDKCompletionTest#32](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_11.vb)]

8. ユーザーが対応するショートカットを入力し、 **Tab**キーを押したときにコード スニペットを挿入するには<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>、メソッドにコードを追加します。 スニペットを挿入するプライベート メソッドは、後の手順で示します。 前の手順で追加したナビゲーション コードの後に、次のコードを追加します。

     [!code-csharp[VSSDKCompletionTest#33](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_12.cs)]
     [!code-vb[VSSDKCompletionTest#33](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_12.vb)]

9. インターフェイスのメソッドを<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient>実装します。 この実装では、対象となるメソッドは<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.EndExpansion%2A>と<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A>だけです。 他のメソッドは、<xref:Microsoft.VisualStudio.VSConstants.S_OK>を返すだけです。

     [!code-csharp[VSSDKCompletionTest#34](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_13.cs)]
     [!code-vb[VSSDKCompletionTest#34](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_13.vb)]

10. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionClient.OnItemChosen%2A> メソッドを実装します。 実際に拡張を挿入するヘルパー メソッドについては、後の手順で説明します。 には<xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan>、行と列の情報が提供され、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>から取得できます。

     [!code-csharp[VSSDKCompletionTest#35](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_14.cs)]
     [!code-vb[VSSDKCompletionTest#35](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_14.vb)]

11. 次のプライベート メソッドは、ショートカットまたはタイトルとパスに基づいてコード スニペットを挿入します。 その後、スニペット<xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansion.InsertNamedExpansion%2A>を使用してメソッドを呼び出します。

     [!code-csharp[VSSDKCompletionTest#36](../extensibility/codesnippet/CSharp/walkthrough-implementing-code-snippets_15.cs)]
     [!code-vb[VSSDKCompletionTest#36](../extensibility/codesnippet/VisualBasic/walkthrough-implementing-code-snippets_15.vb)]

## <a name="build-and-test-code-snippet-expansion"></a>コード スニペットの拡張をビルドおよびテストする
 スニペットの拡張がプロジェクトで機能するかどうかをテストできます。

1. ソリューションをビルドします。 デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

2. テキスト ファイルを開き、テキストを入力します。

3. テキスト内のどこかを右クリックし、[**スニペットの挿入**] をクリックします。

4. スニペット ピッカー UI がポップアップで表示され **、"置換フィールドのテスト**" と表示されます。 ポップアップをダブルクリックします。

     次のスニペットを挿入する必要があります。

    ```
    MessageBox.Show("first");
    MessageBox.Show("second");
    ```

     **Enter**キーまたは**Esc キー**を押さないでください。

5. **Tab**キーと**Shift キーを押**+**Tab**して、"最初" と "2 番目" を切り替えます。

6. 挿入を受け入れるには **、Enter**キーまたは**Esc キー**を押します。

7. テキストの別の部分に「test」と入力し **、Tab**キーを押します。"test" はコード スニペットのショートカットであるため、スニペットを再度挿入する必要があります。

## <a name="next-steps"></a>次のステップ
