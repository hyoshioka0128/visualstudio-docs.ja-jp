---
title: 従来の言語サービスでのコード スニペットのサポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- snippets, supporting in language services
- code snippets, supporting in language services [managed package framework]
- language services [managed package framework], supporting code snippets
ms.assetid: 7490325b-acee-4c2d-ac56-1cd5db1a1083
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad871eb73341f6ab87229687e2a6df898ffda32d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704906"
---
# <a name="support-for-code-snippets-in-a-legacy-language-service"></a>従来の言語サービスでのコード スニペットのサポート
コード スニペットは、ソース ファイルに挿入されるコードの一部です。 スニペット自体は、フィールドのセットを持つ XML ベースのテンプレートです。 これらのフィールドは、スニペットが挿入された後に強調表示され、スニペットが挿入されるコンテキストに応じて異なる値を持つことができます。 スニペットが挿入された直後に、言語サービスはスニペットを書式設定できます。

 このスニペットは、Tab キーを使用してスニペットのフィールドを移動できる特別な編集モードで挿入されます。 フィールドは、IntelliSense スタイルのドロップダウン メニューをサポートできます。 ユーザーは、Enter キーまたは Esc キーを入力して、ソース ファイルにスニペットをコミットします。 スニペットの詳細については、「[コード スニペット](../../ide/code-snippets.md)」を参照してください。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 詳細については、「[チュートリアル: コード スニペットの実装](../../extensibility/walkthrough-implementing-code-snippets.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="managed-package-framework-support-for-code-snippets"></a>コード スニペットのマネージ パッケージ フレームワークのサポート
 マネージ パッケージ フレームワーク (MPF) は、テンプレートの読み取りからスニペットの挿入、特別な編集モードの有効化まで、ほとんどのスニペット機能をサポートしています。 サポートはクラスを通<xref:Microsoft.VisualStudio.Package.ExpansionProvider>じて管理されます。

 クラスが<xref:Microsoft.VisualStudio.Package.Source>インスタンス化されると、<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionProvider%2A><xref:Microsoft.VisualStudio.Package.LanguageService>クラス内のメソッドが呼び出され、オブジェクト<xref:Microsoft.VisualStudio.Package.ExpansionProvider>が取得されます (基本<xref:Microsoft.VisualStudio.Package.LanguageService>クラスは常にオブジェクト<xref:Microsoft.VisualStudio.Package.ExpansionProvider>ごとに<xref:Microsoft.VisualStudio.Package.Source>新しいオブジェクトを返します)。

 MPF は拡張機能をサポートしていません。 拡張関数は、スニペット テンプレートに埋め込まれ、フィールドに配置される 1 つ以上の値を返す名前付き関数です。 値は、<xref:Microsoft.VisualStudio.Package.ExpansionFunction>オブジェクトを介して言語サービス自体によって返されます。 拡張<xref:Microsoft.VisualStudio.Package.ExpansionFunction>機能をサポートするには、言語サービスによってオブジェクトを実装する必要があります。

## <a name="providing-support-for-code-snippets"></a>コード スニペットのサポートの提供
 コード スニペットのサポートを有効にするには、スニペットを指定またはインストールする必要があります。 コード スニペットのサポートを有効にするには、次の 3 つの手順があります。

1. スニペット ファイルをインストールします。

2. 言語サービスのコード スニペットを有効にする。

3. オブジェクトの呼<xref:Microsoft.VisualStudio.Package.ExpansionProvider>び出し。

### <a name="installing-the-snippet-files"></a>スニペット ファイルのインストール
 言語のすべてのスニペットは、XML ファイル (通常はファイルごとに 1 つのスニペット テンプレート) にテンプレートとして格納されます。 コード スニペット テンプレートに使用される XML スキーマの詳細については、「[コード スニペット スキーマ リファレンス](../../ide/code-snippets-schema-reference.md)」を参照してください。 各スニペット テンプレートは、言語 ID で識別されます。 この言語 ID はレジストリで指定され、テンプレートの`Language`code \<> タグの属性に格納されます。

 通常、スニペット テンプレート ファイルが格納される場所は、1) 言語がインストールされた場所と、ユーザーのフォルダーに 2) の 2 つの場所があります。 これらの場所は、Visual Studio**コード スニペット マネージャー**がスニペットを検索できるように、レジストリに追加されます。 ユーザーのフォルダーは、ユーザーによって作成されたスニペットが格納される場所です。

 インストールされたスニペット テンプレート ファイルの一般的なフォルダー レイアウト*は次のようになります*\\ *[TestLanguage]*。\\ *[LCID]*

 *[InstallRoot]は*、あなたの言語がインストールされているフォルダです。

 *[TestLanguage] は*、フォルダ名として使用する言語の名前です。

 *[LCID] は*ロケール ID です。 これは、スニペットのローカライズ版が格納される方法です。 たとえば、英語のロケール ID は 1033 なので *、[LCID] は*1033 に置き換えられます。

 追加のファイルを 1 つ指定する必要があり、これは通常、SnippetsIndex.xml または拡張インデックス.xml と呼ばれるインデックス ファイルです (.xml で終わる任意の有効なファイル名を使用できます)。 このファイルは通常 *[InstallRoot]*\\ *[TestLanguage]* フォルダーに格納され、スニペット フォルダーの正確な場所だけでなく、スニペットを使用する言語サービスの言語 ID と GUID を指定します。 インデックス ファイルの正確なパスは、後述する「レジストリ エントリのインストール」で説明するとおり、レジストリに格納されます。 スニペットインデックス.xmlファイルの例を次に示します。

```
<?xml version="1.0" encoding="utf-8" ?>
<SnippetCollection>
    <Language Lang="Testlanguage" Guid="{b614a40a-80d9-4fac-a6ad-fc2868fff7cd}">
        <SnippetDir>
            <OnOff>On</OnOff>
            <Installed>true</Installed>
            <Locale>1033</Locale>
            <DirPath>%InstallRoot%\TestLanguage\Snippets\%LCID%\Snippets\</DirPath>
            <LocalizedName>Snippets</LocalizedName>
        </SnippetDir>
    </Language>
</SnippetCollection>
```

 言語\<> タグは、言語 ID `Lang` (属性) と言語サービスの GUID を指定します。

 この例では、Visual Studio のインストール フォルダーに言語サービスがインストールされていることを前提としています。 %LCID% は、ユーザーの現在のロケール ID に置き換えられます。 複数\<の SnippetDir> タグを追加できます(ディレクトリとロケールごとに 1 つ)。 さらに、スニペット フォルダーには、各フォルダーは、\<スニペット ディレクトリ> タグに埋め込まれているスニペットサブディレクトリ> タグを持つ\<インデックス ファイルで識別されるサブフォルダーを含めることができます。

 ユーザーは、自分の言語用に独自のスニペットを作成することもできます。 これらは通常、ユーザーの設定フォルダーに格納されます *(たとえば、[TestDocs]* \コード スニペット\\ *[テスト言語]* \テスト コード スニペット、[ *TestDocs] は*Visual Studio のユーザーの設定フォルダーの場所です)。

 インデックス ファイルの DirPath> タグに格納\<されているパスには、次の置換要素を配置できます。

|要素|説明|
|-------------|-----------------|
|%LCID%|ロケール ID。|
|%インストールルート%|たとえば、C:\プログラム ファイル\マイクロソフト Visual Studio 8 などの Visual Studio のルート インストール フォルダー。|
|%プロジダー%|現在のプロジェクトを含むフォルダ。|
|%プロジアイテム%|現在のプロジェクト項目を含むフォルダ。|
|%テストドキュメント%|ユーザーの設定フォルダー内のフォルダー(たとえば、C:\ドキュメントと設定\\ *[ユーザー名] \*マイ ドキュメント\Visual Studio\8)。|

### <a name="enabling-code-snippets-for-your-language-service"></a>言語サービスのコード スニペットを有効にする
 VSPackage に属性を追加することで、言語サービスの<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>コード スニペットを有効にすることができます (詳細については、「[レガシ言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」を参照してください)。 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.ShowRoots%2A>と<xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute.SearchPaths%2A>パラメーターは省略可能ですが、コード スニペット`SearchPaths`**マネージャー**にスニペットの場所を知らせるために、名前付きパラメーターを含める必要があります。

 この属性の使用例を次に示します。

```
[ProvideLanguageCodeExpansion(
         typeof(TestSnippetLanguageService),
         "Test Snippet Language",          // Name of language used as registry key
         0,                               // Resource ID of localized name of language service
         "Test Snippet Language",        // Name of Language attribute in snippet template
         @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\SnippetsIndex.xml",  // Path to snippets index
         SearchPaths = @"%InstallRoot%\Test Snippet Language\Snippets\%LCID%\")]    // Path to snippets
```

### <a name="calling-the-expansion-provider"></a>拡張プロバイダーの呼び出し
 言語サービスは、コード スニペットの挿入と、挿入の呼び出し方法を制御します。

## <a name="calling-the-expansion-provider-for-code-snippets"></a>コード スニペットの拡張プロバイダーの呼び出し
 拡張プロバイダーを呼び出すには、メニュー コマンドを使用する方法と、入力候補一覧のショートカットを使用する方法の 2 つがあります。

### <a name="inserting-a-code-snippet-by-using-a-menu-command"></a>メニュー コマンドを使用したコード スニペットの挿入
 メニュー コマンドを使用してスニペット ブラウザーを表示するには、メニュー コマンドを追加し、<xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A>そのメニュー<xref:Microsoft.VisualStudio.Package.ExpansionProvider>コマンドに応答してインターフェイスでメソッドを呼び出します。

1. コマンドとボタンを .vsct ファイルに追加します。 この手順については、「[メニュー コマンドを使用した拡張機能の作成」を参照してください](../../extensibility/creating-an-extension-with-a-menu-command.md)。

2. クラスからクラスを<xref:Microsoft.VisualStudio.Package.ViewFilter>派生させ、メソッドを<xref:Microsoft.VisualStudio.Package.ViewFilter.QueryCommandStatus%2A>オーバーライドして、新しいメニュー コマンドのサポートを示します。 この例では、常にメニュー コマンドを有効にします。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public TestViewFilter(CodeWindowManager mgr, IVsTextView view)
                : base(mgr, view)
            {
            }

            protected override int QueryCommandStatus(ref Guid guidCmdGroup,
                                                      uint nCmdId)
            {
                int hr = base.QueryCommandStatus(ref guidCmdGroup, nCmdId);
                // If the base class did not recognize the command then
                // see if we can handle the command.
                if (hr == (int)Microsoft.VisualStudio.OLE.Interop.Constants.OLECMDERR_E_UNKNOWNGROUP)
                {
                    if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                    {
                        if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                        {
                            hr = (int)(OLECMDF.OLECMDF_SUPPORTED | OLECMDF.OLECMDF_ENABLED);
                        }
                    }
                }
                return hr;
            }
        }
    }
    ```

3. クラスの<xref:Microsoft.VisualStudio.Package.ViewFilter.HandlePreExec%2A>メソッドを<xref:Microsoft.VisualStudio.Package.ViewFilter>オーバーライドしてオブジェクトを<xref:Microsoft.VisualStudio.Package.ExpansionProvider>取得し、そのオブジェクト<xref:Microsoft.VisualStudio.Package.ExpansionProvider.DisplayExpansionBrowser%2A>のメソッドを呼び出します。

    ```csharp
    using Microsoft.VisualStudio.Package;

    namespace TestLanguagePackage
    {
        class TestViewFilter : ViewFilter
        {
            public override bool HandlePreExec(ref Guid guidCmdGroup,
                                               uint nCmdId,
                                               uint nCmdexecopt,
                                               IntPtr pvaIn,
                                               IntPtr pvaOut)
            {
                if (base.HandlePreExec(ref guidCmdGroup,
                                       nCmdId,
                                       nCmdexecopt,
                                       pvaIn,
                                       pvaOut))
                {
                    // Base class handled the command.  Do nothing more here.
                    return true;
                }

                if (guidCmdGroup == GuidList.guidTestLanguagePackageCmdSet)
                {
                    if (nCmdId == PkgCmdIDList.InvokeCodeSnippetsBrowser)
                    {
                        ExpansionProvider ep = this.GetExpansionProvider();
                        if (this.TextView != null && ep != null)
                        {
                            bool bDisplayed = ep.DisplayExpansionBrowser(
                                this.TextView,
                                "TestLanguagePackage Snippet:",
                                null,
                                false,
                                null,
                                false);
                        }
                        return true;   // Handled the command.
                    }
                }
                return false;   // Did not handle the command.
            }
        }
    }

    ```

     クラス内の次の<xref:Microsoft.VisualStudio.Package.ExpansionProvider>メソッドは、スニペットを挿入するプロセス中に、指定された順序で Visual Studio によって呼び出されます。

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnItemChosen%2A>

5. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

6. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

7. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

8. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

     メソッドが<xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>呼び出されると、スニペットが挿入され、<xref:Microsoft.VisualStudio.Package.ExpansionProvider>オブジェクトは挿入されたばかりのスニペットを変更するために使用される特別な編集モードになります。

### <a name="inserting-a-code-snippet-by-using-a-shortcut"></a>ショートカットを使用したコード スニペットの挿入
 完了リストからのショートカットの実装は、メニュー コマンドを実装する場合よりもはるかに複雑です。 最初に、スニペットのショートカットを IntelliSense 単語補完リストに追加する必要があります。 次に、完了の結果としてスニペットのショートカット名が挿入されたことを検出する必要があります。 最後に、ショートカット名を使用してスニペットのタイトルとパスを取得し、<xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A><xref:Microsoft.VisualStudio.Package.ExpansionProvider>その情報をメソッドに渡す必要があります。

 スニペットのショートカットを単語補完リストに追加するには、クラスの<xref:Microsoft.VisualStudio.Package.Declarations>オブジェクトに追加します<xref:Microsoft.VisualStudio.Package.AuthoringScope>。 ショートカットをスニペット名として識別できることを確認する必要があります。 例については、「[チュートリアル: インストールされているコード スニペットの一覧の取得 (レガシ実装)」](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)を参照してください。

 コード スニペットのショートカットの挿入は、クラスの<xref:Microsoft.VisualStudio.Package.Declarations.OnAutoComplete%2A>メソッドで検出できます。 <xref:Microsoft.VisualStudio.Package.Declarations> スニペット名はソース ファイルに既に挿入されているため、展開を挿入するときに削除する必要があります。 この<xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A>メソッドは、スニペットの挿入ポイントを記述する範囲をとります。スパンにソースファイル内のスニペット名全体が含まれている場合、その名前はスニペットに置き換えられます。

 次に、ショートカット名を<xref:Microsoft.VisualStudio.Package.Declarations>指定してスニペットの挿入を処理するクラスのバージョンを示します。 クラス内の他<xref:Microsoft.VisualStudio.Package.Declarations>のメソッドは、わかりやすくするために省略されています。 このクラスのコンストラクターはオブジェクトを<xref:Microsoft.VisualStudio.Package.LanguageService>受け取ります。 これは、<xref:Microsoft.VisualStudio.Package.AuthoringScope>オブジェクトのバージョンから渡すことができます (たとえば、<xref:Microsoft.VisualStudio.Package.AuthoringScope>クラスの実装は、そのコンストラクターで<xref:Microsoft.VisualStudio.Package.LanguageService>オブジェクトを取得し、そのオブジェクトをクラス コンストラクターに渡す`TestDeclarations`場合があります)。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclarations : Declarations
    {
        private ArrayList       declarations;
        private LanguageService languageService;
        private TextSpan        commitSpan;

        public TestDeclarations(LanguageService langService)
            : base()
        {
            languageService = langService;
            declarations = new ArrayList();
        }

        // This method is used to add declarations to the internal list.
        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        // This method is called to get the string to commit to the source buffer.
        // Note that the initial extent is only what the user has typed so far.
        public override string OnCommit(IVsTextView textView,
                                        string textSoFar,
                                        char commitCharacter,
                                        int index,
                                        ref TextSpan initialExtent)
        {
            // We intercept this call only to get the initial extent
            // of what was committed to the source buffer.
            commitSpan = initialExtent;

            return base.OnCommit(textView,
                                 textSoFar,
                                 commitCharacter,
                                 index,
                                 ref initialExtent);
        }

        // This method is called after the string has been committed to the source buffer.
        public override char OnAutoComplete(IVsTextView textView,
                                            string committedText,
                                            char commitCharacter,
                                            int index)
        {
            TestDeclaration item = declarations[index] as TestDeclaration;
            if (item != null)
            {
                // In this example, TestDeclaration identifies types with a string.
                // You can choose a different approach.
                if (item.Type == "snippet")
                {
                    Source src = languageService.GetSource(textView);
                    if (src != null)
                    {
                        ExpansionProvider ep = src.GetExpansionProvider();
                        if (ep != null)
                        {
                            string title;
                            string path;
                            int commitLength = commitSpan.iEndIndex - commitSpan.iStartIndex;
                            if (commitLength < committedText.Length)
                            {
                                // Replace everything that was inserted
                                // so calculate the span of the full
                                // insertion, taking into account what
                                // was inserted when the commitSpan
                                // was obtained in the first place.
                                commitSpan.iEndIndex += (committedText.Length - commitLength);
                            }

                            if (ep.FindExpansionByShortcut(textView,
                                                           committedText,
                                                           commitSpan,
                                                           true,
                                                           out title,
                                                           out path))
                            {
                                ep.InsertNamedExpansion(textView,
                                                        title,
                                                        path,
                                                        commitSpan,
                                                        false);
                            }
                        }
                    }
                }
            }
            return '\0';
        }
    }
}
```

 言語サービスは、ショートカット名を取得すると、メソッドを<xref:Microsoft.VisualStudio.Package.ExpansionProvider.FindExpansionByShortcut%2A>呼び出して、ファイル名とコード スニペットのタイトルを取得します。 次に、言語サービスは<xref:Microsoft.VisualStudio.Package.ExpansionProvider.InsertNamedExpansion%2A>、コード<xref:Microsoft.VisualStudio.Package.ExpansionProvider>スニペットを挿入するクラス内のメソッドを呼び出します。 次のメソッドは、スニペットを挿入するプロセス中に、クラス<xref:Microsoft.VisualStudio.Package.ExpansionProvider>内の指定された順序で Visual Studio によって呼び出されます。

1. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.IsValidKind%2A>

2. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnBeforeInsertion%2A>

3. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.FormatSpan%2A>

4. <xref:Microsoft.VisualStudio.Package.ExpansionProvider.OnAfterInsertion%2A>

   使用している言語サービス用にインストールされているコード スニペットの一覧を取得する方法の詳細については、「[チュートリアル: インストールされているコード スニペットの一覧の取得 (レガシ実装)」](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)を参照してください。

## <a name="implementing-the-expansionfunction-class"></a>拡張関数クラスの実装
 拡張関数は、スニペット テンプレートに埋め込まれ、フィールドに配置される 1 つ以上の値を返す名前付き関数です。 言語サービスで拡張関数をサポートするには、<xref:Microsoft.VisualStudio.Package.ExpansionFunction>クラスからクラスを派生させ、メソッドを実装する<xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetCurrentValue%2A>必要があります。 次に、クラス内<xref:Microsoft.VisualStudio.Package.LanguageService.CreateExpansionFunction%2A>のメソッドを<xref:Microsoft.VisualStudio.Package.LanguageService>オーバーライドして、サポートする各拡張関数のクラスのバージョンの<xref:Microsoft.VisualStudio.Package.ExpansionFunction>新しいインスタンス化を返す必要があります。 拡張関数から使用可能な値のリストをサポートしている場合は、<xref:Microsoft.VisualStudio.Package.ExpansionFunction.GetIntellisenseList%2A><xref:Microsoft.VisualStudio.Package.ExpansionFunction>クラス内のメソッドをオーバーライドして、それらの値のリストを返す必要があります。

 拡張関数が呼び出されるまでに拡張プロバイダーが完全に初期化されない場合があるため、引数を受け取る拡張関数や他のフィールドにアクセスする必要がある拡張関数は、編集可能フィールドに関連付けるべきではありません。 その結果、拡張関数は、その引数またはその他のフィールドの値を取得できません。

### <a name="example"></a>例
 呼び出された`GetName`単純な拡張関数を実装する方法の例を次に示します。 この拡張関数は、拡張関数がインスタンス化されるたびに基本クラス名に数値を追加します (これは、関連付けられたコード スニペットが挿入されるたびに対応します)。

```csharp
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    public class TestLanguageService : LanguageService
    {
        private int classNameCounter = 0;

        public override ExpansionFunction CreateExpansionFunction(
            ExpansionProvider provider,
            string functionName)
        {
            ExpansionFunction function = null;
            if (functionName == "GetName")
            {
                ++classNameCounter;
                function = new TestGetNameExpansionFunction(provider, classNameCounter);
            }
            return function;
        }
    }

    internal class TestGetNameExpansionFunction : ExpansionFunction
    {
        private int nameCount;

        TestGetNameExpansionFunction(ExpansionProvider provider, int counter)
            : base(provider)
        {
            nameCount = counter;
        }

        public override string GetCurrentValue()
        {
            string name = "TestClass";
            name += nameCount.ToString();
            return name;
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)
- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)
- [コード スニペット](../../ide/code-snippets.md)
- [チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)
