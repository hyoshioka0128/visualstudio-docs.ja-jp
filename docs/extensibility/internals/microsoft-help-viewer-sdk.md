---
title: Microsoft ヘルプビューアー SDK |Microsoft Docs
description: 記事の作成、ヘルプビューアーのコンテンツブランド化パッケージの作成、一連の記事のデプロイなど、Visual Studio ヘルプビューアーのタスクについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c53191c5f6e02c0b37d29f89a65119f1edab92ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063319"
---
# <a name="microsoft-help-viewer-sdk"></a>Microsoft ヘルプ ビューアー SDK

この記事には、Visual Studio ヘルプビューアーインテグレーターに関する次のタスクが含まれています。

- トピックの作成 (F1 サポート)

- ヘルプビューアーのコンテンツブランドパッケージの作成

- 一連の記事の配置

- Visual Studio シェルへのヘルプの追加 (統合または分離)

- その他のリソース

## <a name="create-a-topic-f1-support"></a>トピックを作成する (F1 サポート)

ここでは、表示されるトピックのコンポーネントの概要、トピックの要件、トピックの作成方法に関する簡単な説明 (F1 サポート要件を含む) について説明します。最後に、結果を表示するトピックの例を示します。

**ヘルプビューアートピックの概要**

トピックを表示するために呼び出されると、ヘルプビューアーは、インストール時または最終更新時にトピックに関連付けられているブランド化パッケージ要素をトピック XHTML と共に取得し、2つを組み合わせて、表示されるコンテンツビュー (ブランドデータ + トピックデータ) に表示します。  ブランド化パッケージには、ロゴ、コンテンツの動作のサポート、ブランドのテキスト (著作権など) が含まれています。  ブランド化パッケージの要素の詳細については、以下の「ブランド化パッケージの作成」を参照してください。  トピックに関連付けられているブランド化パッケージがない場合、ヘルプビューアーは、ヘルプビューアーアプリケーションルート (Branding_en-.mshc) にあるフォールバックブランドパッケージを使用します。

**ヘルプビューアートピックの要件**

ヘルプビューアー内で正しくレンダリングされるためには、未加工のトピックコンテンツが W3C Basic 1.1 XHTML である必要があります。

トピックには、通常、次の2つのセクションが含まれます。

- メタデータ (コンテンツメタデータリファレンスを参照): トピックに関するデータ。たとえば、トピックの一意の ID、キーワード値、トピック TOC ID、親ノード ID などです。

- 本文の内容: サポートされているコンテンツ動作 (折りたたみ可能な領域、コードスニペットなど) を含む W3C Basic 1.1 XHTML に準拠しています。完全な一覧を次に示します)。

Visual Studio ブランド化パッケージでサポートされるコントロール:

- リンク

- CodeSnippet

- CollapsibleArea

- 継承されたメンバー

- LanguageSpecificText

サポートされている言語の文字列 (大文字と小文字は区別されません):

- JavaScript

- csharp または c#

- cplusplus または visualc + + または c++

- jscript

- visual basic または vb

- f # または fsharp.core または fs

- その他-言語名を表す文字列

**ヘルプビューアートピックの作成**

ContosoTopic4.htm という名前の新しい XHTML ドキュメントを作成し、タイトルタグ (下記) を含めます。

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

次に、トピックの表示方法を定義するためにデータを追加します (自己ブランド化されているかどうか)。このトピックを参照する方法については、このトピックの目次内、ID (他のトピックによるリンク参照用) などを参照してください。サポートされているメタデータの完全な一覧については、以下の「コンテンツメタデータ」の表を参照してください。

- この例では、Visual Studio ヘルプビューアーブランド化パッケージのバリエーションである独自のブランド化パッケージを使用します。

- IDE プロパティバッグで、指定された F1 値に一致する F1 メタ名と値 ("ContosoTopic4") を追加します。 (詳細については、「F1 サポート」セクションを参照してください)。これは、ide で F1 を選択したときに、このトピックを表示するために IDE 内からの F1 呼び出しに一致する値です。

- トピック ID を追加します。 これは、このトピックにリンクするために他のトピックによって使用される文字列です。 これは、このトピックのヘルプビューアー ID です。

- TOC の場合は、このトピックの親ノードを追加して、このトピックの TOC ノードが表示される場所を定義します。

- TOC の場合は、このトピックのノードの順序を追加します。 親ノードに `n` 子ノードの数がある場合は、このトピックの場所の子ノードの順序でを定義します。 たとえば、このトピックは4つの子トピックである4個です。

メタデータセクションの例:

```html
<html>
<head>
<title>Contoso Topic 4</title>

<meta name="SelfBranded" content="false" />
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />

</head>

<body>

</body>
</html>
```

**トピック本文**

トピックの本文 (ヘッダーとフッターを除く) には、ページリンク、メモセクション、折りたたみ可能な領域、コードスニペット、および言語固有のテキストのセクションが含まれます。  表示されるトピックの領域については、「ブランド化」セクションを参照してください。

1. トピックタイトルタグを追加します。  `<div class="title">Contoso Topic 4</div>`

2. メモセクションを追加します。 `<div class="alert"> add your table tag and text </div>`

3. 折りたたみ可能な領域の追加:  `<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. コードスニペットを追加します。  `<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. コード言語固有のテキストを追加する:  `<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />` では `devLangnu=` 、他の言語を入力できます。 たとえば、 `devLangnu="Fortran"` コードスニペット DisplayLanguage = fortran の場合、は fortran を表示します。

6. ページリンクの追加: `<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> 注: サポートされていない新しい "表示言語" (例、F #、Cobol、Fortran) では、コードスニペットのコードの色付けはモノクロになります。

**ヘルプビューアーのトピックの例** このコードは、メタデータ、コードスニペット、折りたたみ可能な領域、および言語固有のテキストを定義する方法を示しています。

```html
<?xml version="1.0" encoding="utf-8"?>
<html>
<head>
<title>Contoso Topic 4</title>

    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="Microsoft.Help.Id" content="ContosoTopic4" />
<meta name="Microsoft.Help.F1" content=" ContosoTopic4" />
    <meta name="Language" content="en-us" />
<meta name="Microsoft.Help.TocParent" content="ContosoTopic0" />
<meta name="Microsoft.Help.TocOrder" content="4" />
<meta name="SelfBranded" content="false" />
</head>

<body>
<div class="title">Contoso Topic 4</div>

  <div id="header">
<table id="bottomTable" cellpadding="0" cellspacing="0"  width="100%">
        <tr id="headerTableRow2"><td align="left">
            <span id="nsrTitle">Contoso Topic 1</span>
          </td>
<td align="right">
</td></tr>
<tr id="headerTableRow1"><td align="left">
            <span id="runningHeaderText">Contoso Widgets & Sprockets</span>
          </td></tr>
      </table>
</div>

<h2>Table of Contents</h2>

<ul class="toc">
<li class="tocline1"><a href="#introduction" target="_self">1.0 Introduction</a></li>
<li class="tocline1"><a href="#seealso" target="_self">See Also</a></li>
</ul>

<div class="topic">

<div id="mainSection">
<div id="mainBody">

<a name="introduction"></a>
<h2>1.0 Introduction</h2>
<p>[This documentation is for sample purposes only.]</p>

<p>Contoso Topic 1 contains examples of:
<ul>
<li>Collapsible Area</li>
<li>Bookmark ("See also")</li>
<li>Code Snippets from Branding Package</li>
</ul>
 </p>
<div class="alert"><table><tr><th>
<strong>Note </strong></th></tr>
<tr><td>
<p>This is an example of a <span class="label">Note </span>section.
Call out important items for your reader in this <span class="label">Note </span>box.
</p></td></tr>
</table>
</div>
</div>

<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading">

            <a id="sectionToggle0"><!----></a>

<div>
Example of Collapsible Area
<br/>
Lorem ipsum dolor sit amet...
</div>
</CollapsibleArea>

<div id="snippetGroup" >
<CodeSnippet EnableCopyCode="true" Language="VisualBasic" ContainsMarkup="false" DisplayLanguage="Visual Basic" >
Private Sub ToolStripRenderer1_RenderGrip(sender as Object, e as ToolStripGripRenderEventArgs) _ Handles ToolStripRenderer1.RenderGrip
Dim messageBoxVB as New System.Text.StringBuilder()
    messageBoxVB.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds)
    messageBoxVB.AppendLine()
 ...
    MessageBox.Show(messageBoxVB.ToString(),"RenderGrip Event")
End Sub
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" >
private void ToolStripRenderer1_RenderGrip(Object sender, ToolStripGripRenderEventArgs e)
{
System.Text.StringBuilder messageBoxCS = new System.Text.StringBuilder();
messageBoxCS.AppendFormat("{0} = {1}", "GripBounds", e.GripBounds );
messageBoxCS.AppendLine();
...
MessageBox.Show(messageBoxCS.ToString(), "RenderGrip Event" );
}
</CodeSnippet>

<CodeSnippet EnableCopyCode="true" Language="fsharp" ContainsMarkup="false" DisplayLanguage="F#" >
some F# code
</CodeSnippet>
</div>

<h4 class="subHeading">Example of code specific text</h4>Language = <LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />

<a name="seealso"></a>
<h1 class="heading">See Also</h1>

    <div id="seeAlsoSection" class="section">
    <div class="seeAlsoStyle">
        <a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>
    </div>
 </div>
</div>
</div>
</body>
</html>
```

**F1 サポート**

Visual Studio で F1 を選択すると、IDE 内のカーソルの位置から指定された値が生成され、指定された値 (カーソル位置に基づく) が "プロパティバッグ" に設定されます。 カーソルが機能 x 上にある場合、機能 x はアクティブ/フォーカスが設定され、プロパティバッグに値が設定されます。  F1 キーを選択すると、プロパティバッグが設定され、Visual Studio F1 コードによって、顧客の既定のヘルプソースがローカルまたはオンライン (既定値は online) であるかどうかが確認されます。次に、ユーザー設定 (既定では online) に基づいて適切な文字列が作成されます (exe 起動パラメーターのヘルプ管理者ガイドを参照してください)。ローカルヘルプが既定値の場合は、プロパティバッグのローカルヘルプビューアー + キーワードのパラメーターを指定します。、または、パラメーターリストにキーワードが含まれている MSDN URL。

複数値の文字列と呼ばれる F1 に対して3つの文字列が返された場合は、最初の用語を使用してヒットを探し、見つかった場合は終了します。それ以外の場合は、次の文字列に移動します。  順序は重要です。 複数値のキーワードを使用する場合は、最短文字列型の文字列にすることをお勧めします。  複数値のキーワードの場合、これを確認するには、オンラインの F1 URL 文字列を調べます。これには、選択したキーワードが含まれます。

Visual Studio 2012 では、オンラインとオフラインの間でより強力な分割が意図的に行われているため、ユーザーの設定がオンラインになっている場合は、Visual Studio 2010 で使用していたヘルプライブラリエージェントを経由せずに、MSDN のオンラインクエリサービスに F1 要求を直接渡すだけです。 次に、"vendor content installed = true" という状態を使用して、そのコンテキストで別の操作を実行するかどうかを判断します。 True の場合、お客様にサポートするものに応じて、この解析とルーティングのロジックを実行します。 False の場合は、MSDN にアクセスします。 ユーザーの設定が Local に設定されている場合は、すべての呼び出しがローカルヘルプエンジンに送られます。

F1 フローダイアグラム:

![F1 フロー](../../extensibility/internals/media/f1flow.png "F1flow")

ヘルプビューアーの既定のヘルプコンテンツソースが [オンライン] に設定されている場合 ([ブラウザーで起動]):

- Visual Studio Partner (VSP) 機能は、F1 プロパティバッグに値を出力します (プロパティバッグプレフィックス。レジストリで見つかったプレフィックスの URL とオンライン URL): F1 は、VSP URL + パラメーターをブラウザーに送信します。

- Visual Studio の機能 (言語エディター、Visual Studio 固有のメニュー項目など): F1 キーを押して Visual Studio の URL をブラウザーに送信します。

ヘルプビューアーの既定のヘルプコンテンツソースがローカルヘルプ (ヘルプビューアーで起動) に設定されている場合は、次のようになります。

- 次のように、キーワードが F1 プロパティバッグとローカルストアインデックス (つまり、プロパティバッグプレフィックス. keyword = ローカルストアインデックスで検出された値) と一致する VSP 機能。 F1 はヘルプビューアーでトピックを表示します。

- Visual Studio の機能 (Visual Studio の機能から生成されたプロパティバッグを VSP がオーバーライドするオプションはありません): F1 では、Visual Studio のトピックがヘルプビューアーに表示されます。

次のレジストリ値を設定して、ベンダーのヘルプコンテンツの F1 フォールバックを有効にします。 F1 フォールバックは、ヘルプビューアーが F1 ヘルプコンテンツをオンラインで検索するように設定されており、ベンダーのコンテンツがユーザーのハードドライブにローカルでインストールされていることを意味します。 ヘルプビューアーは、既定の設定がオンラインヘルプの場合でも、コンテンツのローカルヘルプを確認する必要があります。

1. Help 2.3 レジストリキーの下に **VendorContent** 値を設定します。

   - 32ビットオペレーティングシステムの場合:

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = dword: 00000001

   - 64ビットオペレーティングシステムの場合:

        HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "VendorContent" = dword: 00000001

2. Help 2.3 レジストリキーの下に、partner 名前空間を登録します。

   - 32ビットオペレーティングシステムの場合:

      <em> \\<名前空間 \> </em>の HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Partner

      "場所" = "オフライン"

   - 64ビットオペレーティングシステムの場合:

      <em> \\<名前空間 \> </em>の HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Partner

      "場所" = "オフライン"

**基本のネイティブ名前空間の解析**

基本のネイティブ名前空間の解析を有効にするには、レジストリで、BaseNativeNamespaces の名前を指定して新しい DWORD を追加し、その値を 1 (サポートするカタログキーの下) に設定します。  たとえば、Visual Studio カタログを使用する場合は、次のようにキーをパスに追加します。

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

形式ヘッダー/メソッドで F1 キーワードが検出されると、'/' 文字が解析され、次のような構造になります。

- ヘッダー: は、レジストリに登録するために使用できる名前空間になります。

- METHOD: これは、を通じて渡されるキーワードになります。

たとえば、CustomLibrary というカスタムライブラリと MyTestMethod いう名前のメソッドがある場合、F1 要求があると、として書式設定され `CustomLibrary/MyTestMethod` ます。

その後、ユーザーは、パートナーハイブの下に名前空間として CustomLibrary を登録し、必要な任意の場所キーを指定します。クエリに渡されたキーワードは MyTestMethod ようになります。

**IDE でヘルプデバッグツールを有効にする**

次のレジストリキーと値を追加します。

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\15.0\Dynamic Help**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\16.0\Dynamic Help**

::: moniker-end

値: 製品データにデバッグ出力を表示します: はい

IDE の [ヘルプ] メニュー項目で、[ **ヘルプコンテキストのデバッグ**] を選択します。

**コンテンツのメタデータ**

次の表では、角かっこで囲まれた文字列は、認識された値に置き換える必要があるプレースホルダーです。 たとえば、では \<meta name="Microsoft.Help.Locale" content="[language code]" /> 、"[言語コード]" を "en-us" などの値に置き換える必要があります。

| Property (HTML 表現) | Description |
| - | - |
| \< meta name="Microsoft.Help.Locale" content="[language-code]" /> | このトピックのロケールを設定します。 このタグがトピックで使用されている場合は、1回だけ使用する必要があり、その他の Microsoft ヘルプタグの上に挿入する必要があります。 このタグが使用されていない場合、指定されている場合、製品のロケールに関連付けられているワードブレーカーを使用して、トピックの本文のインデックスが作成されます。それ以外の場合は、en-us ワードブレーカーが使用されます。 このタグは ISOC RFC 4646 に準拠しています。 Microsoft ヘルプが正しく動作するようにするには、一般言語属性ではなく、このプロパティを使用します。 |
| \< meta name="Microsoft.Help.TopicLocale" content="[language-code]" /> | 他のロケールも使用されている場合に、このトピックのロケールを設定します。 このタグがトピックで使用されている場合は、1回だけ使用する必要があります。 このタグは、カタログに複数の言語のコンテンツが含まれている場合に使用します。 カタログ内の複数のトピックは同じ ID を持つことができますが、それぞれが一意のトピックのロケールを指定する必要があります。 カタログのロケールに一致するトピックのロケールを指定するトピックは、目次に表示されるトピックです。 ただし、検索結果には、トピックのすべての言語バージョンが表示されます。 |
| \< title>題\</title> | このトピックのタイトルを指定します。 このタグは必須であり、トピック内で1回だけ使用する必要があります。 トピックの本文に title セクションが含まれていない場合 \<div> 、このタイトルはトピックと目次に表示されます。 |
| \< meta name=" Microsoft.Help.Keywords" content="[aKeywordPhrase]"/> | ヘルプビューアーの [インデックス] ペインに表示されるリンクのテキストを指定します。 リンクをクリックすると、トピックが表示されます。 1つのトピックに対して複数のインデックスキーワードを指定することも、このトピックへのリンクがインデックスに表示されないようにする場合は、このタグを省略することもできます。 以前のバージョンのヘルプの "K" キーワードは、このプロパティに変換できます。 |
| \< meta name="Microsoft.Help.Id" content="[TopicID]"/> | このトピックの識別子を設定します。 このタグは必須であり、トピック内で1回だけ使用する必要があります。 ID は、同じロケール設定のカタログ内のトピック間で一意である必要があります。 別のトピックでは、この ID を使用して、このトピックへのリンクを作成できます。 |
| \< meta name="Microsoft.Help.F1" content="[System.Windows.Controls.Primitives.IRecyclingItemContainerGenerator]"/> | このトピックの F1 キーワードを指定します。 1つのトピックに対して複数の F1 キーワードを指定できます。また、アプリケーションユーザーが F1 キーを押したときにこのトピックが表示されないようにする場合は、このタグを省略できます。 通常、1つのトピックに対して F1 キーワードを1つだけ指定します。 以前のバージョンのヘルプの "F" キーワードは、このプロパティに変換できます。 |
| \< meta name="Description" content="[topic description]" /> | このトピックの内容の簡単な概要を示します。 このタグがトピックで使用されている場合は、1回だけ使用する必要があります。 このプロパティは、クエリライブラリによって直接アクセスされます。インデックスファイルには格納されません。 |
| meta name = "TocParent" content = "[parent_Id]"/> | 目次内のこのトピックの親トピックを指定します。 このタグは必須であり、トピック内で1回だけ使用する必要があります。 値は、親の Microsoft.Help.Id です。 トピックは、目次内で1つの場所のみを持つことができます。 "-1" は、TOC ルートのトピック ID と見なされます。 で [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] は、このページはヘルプビューアーのホームページです。 これは、TocParent =-1 をいくつかのトピックに明示的に追加して、それらが最上位レベルに表示されるようにするためのものです。 ヘルプビューアーのホームページはシステムページであり、置き換え可能ではありません。 VSP が ID が-1 のページを追加しようとすると、コンテンツセットに追加されることがありますが、ヘルプビューアーは常に [システム] ページの [ヘルプビューアーホーム] を使用します。 |
| \< meta name="Microsoft.Help.TocOrder" content="[positive integer]"/> | このトピックの目次で、ピアトピックに対して相対的に表示される場所を指定します。 このタグは必須であり、トピック内で1回だけ使用する必要があります。 値は整数です。 より値の大きい整数を指定するトピックの上に、値が小さい整数を指定するトピックがあります。 |
| \< meta name="Microsoft.Help.Product" content="[product code]"/> | このトピックで説明する製品を指定します。 このタグがトピックで使用されている場合は、1回だけ使用する必要があります。 この情報は、ヘルプインデクサーに渡されるパラメーターとして指定することもできます。 |
| \< meta name="Microsoft.Help.ProductVersion" content="[version number]"/> | このトピックで説明する製品のバージョンを指定します。 このタグがトピックで使用されている場合は、1回だけ使用する必要があります。 この情報は、ヘルプインデクサーに渡されるパラメーターとして指定することもできます。 |
| \< meta name="Microsoft.Help.Category" content="[string]"/> | コンテンツのサブセクションを識別するために製品によって使用されます。 1つのトピックに対して複数のサブセクションを特定できます。また、サブセクションを識別するリンクが必要ない場合は、このタグを省略できます。 このタグは、トピックが以前のバージョンのヘルプから変換された場合に、TargetOS および TargetFrameworkMoniker の属性を格納するために使用されます。 コンテンツの形式は AttributeName: AttributeValue です。 |
| \< meta name="Microsoft.Help.TopicVersion content="[topic version number]"/> | カタログ内に複数のバージョンが存在する場合に、このバージョンのトピックを指定します。 Microsoft.Help.Id は一意であることが保証されていないため、カタログに複数のバージョンのトピックが存在する場合、このタグが必要になります。たとえば、カタログに .NET Framework 3.5 のトピックと .NET Framework 4 のトピックが含まれ、両方が同じ Microsoft.Help.Id を持っている場合などです。 |
| \< meta name="SelfBranded" content="[TRUE or FALSE]"/> | このトピックで、ヘルプライブラリマネージャのスタートアップブランドパッケージを使用するか、トピックに固有のブランドパッケージを使用するかを指定します。 このタグは、TRUE または FALSE のいずれかである必要があります。 TRUE の場合、関連付けられているトピックのブランド化パッケージは、ヘルプライブラリマネージャーが起動したときに設定されているブランド化パッケージよりも優先されます。これにより、トピックが他のコンテンツのレンダリングと異なる場合でも意図したとおりに表示されるようになります。 FALSE の場合は、ヘルプライブラリマネージャーが起動したときに設定されているブランド化パッケージに従って、現在のトピックが表示されます。 既定では、SelfBranded 変数が TRUE として宣言されていない限り、ヘルプライブラリマネージャーは自己ブランド化を false にすることを前提としています。したがって、を宣言する必要はありません \<meta name="SelfBranded" content="FALSE"/> 。 |

## <a name="create-a-branding-package"></a>ブランド化パッケージを作成する

Visual studio リリースには、Visual studio パートナー向けの分離された統合シェルを含むさまざまな Visual Studio 製品が含まれています。  これらの製品には、製品に固有のトピックベースのヘルプコンテンツブランドサポートが必要です。  たとえば、Visual Studio のトピックには一貫したブランドプレゼンテーションが必要ですが、ISO シェルをラップする SQL Studio では、各トピックに固有のヘルプコンテンツのブランド化が必要です。  統合シェルパートナーは、独自のトピックブランドを維持したまま、親の Visual Studio 製品ヘルプコンテンツ内でヘルプトピックを表示することができます。

ブランド化パッケージは、ヘルプビューアーを含む製品によってインストールされます。  Visual Studio 製品の場合:

- フォールバックブランディングパッケージ (Branding_) は、ヘルプビューアーの \<locale> 言語パックによって、ヘルプビューアー2.3 アプリのルート (例: C:\Program files (x86) \Microsoft Help Viewer\v2.3) にインストールされます。  これは、製品ブランディングパッケージがインストールされていない場合 (コンテンツがインストールされていない場合)、またはインストールされているブランド化パッケージが破損している場合に使用されます。  アプリのルートフォールバックブランドパッケージが使用されている場合、Visual Studio の要素 (ロゴとフィードバック) は無視されます。

- コンテンツパッケージサービスから Visual Studio コンテンツがインストールされると、ブランドパッケージもインストールされます (初めてコンテンツをインストールする場合)。  ブランド化パッケージの更新プログラムがある場合は、次のコンテンツ更新プログラムまたはパッケージの追加インストールアクションが実行されるときに、更新プログラムがインストールされます。

Microsoft ヘルプビューアーでは、トピックのメタデータに基づくトピックのブランド化がサポートされています。

- Topic メタデータで自己ブランド化 = true が定義されている場合は、トピックをそのままレンダリングします (ブランド化と同様)。

- Topic メタデータで自己ブランド化 = false を定義する場合は、トピック「ベンダーメタデータ値」に関連付けられているブランド化パッケージを使用します。

- トピックのメタデータでは、name = "Microsoft. topic ベンダ" content = を定義し \< branding package name in vendor MSHA> ます。コンテンツの値で定義されているブランド化パッケージを使用します。

- Visual Studio カタログ内には、ブランド化パッケージの優先的な適用があります。  最初の Visual Studio の既定のブランド化が適用され、トピックのメタデータで定義されていて、関連付けられているブランド化パッケージ (インストール msha で定義) でサポートされている場合は、ベンダーが定義したブランドが上書きとして適用されます。

ブランド化要素は、通常、次の3つの主なカテゴリに分類されます。

- ヘッダー要素 (例には、フィードバックリンク、条件付き免責テキスト、ロゴ)

- コンテンツの動作 (例には、展開/折りたたみコントロールテキスト要素とコードスニペット要素が含まれます)

- フッター要素 (著作権の例)

ブランド要素と見なされる項目には、次のようなものがあります (この仕様で詳しく説明します)。

- カタログ/製品ロゴ (例、Visual Studio)

- フィードバックリンクと電子メールの要素

- 免責事項のテキスト

- 著作権テキスト

Visual Studio ヘルプビューアーのブランド化パッケージに含まれるサポートファイルは次のとおりです。

- グラフィックス (ロゴ、アイコンなど)

- Branding.js-コンテンツの動作をサポートするスクリプトファイル

- Branding.xml-カタログコンテンツ全体で一貫して使用される文字列。  注: branding.xml の Visual Studio のローカライズテキスト要素の場合は、_locID = "" を含めます。 \<unique value>

- ブランド化の css スタイルの定義 (プレゼンテーションの一貫性)

- 印刷された印刷用の css スタイルの定義

前述のように、ブランド化パッケージはトピックに関連付けられています。

- メタデータで SelfBranded = false が定義されている場合、トピックはカタログブランド化パッケージを継承します。

- または、SelfBranded = false の場合、MSHA で定義された一意のブランド化パッケージがあり、コンテンツがインストールされているときに使用できます。

カスタムブランドパッケージ (VSP コンテンツ、SelfBranded = True) を実装する .Vsps の場合、続行する1つの方法は、フォールバックブランドパッケージ (ヘルプビューアーと共にインストールされます) から開始し、必要に応じてファイル名を変更することです。  \<locale>.Mshc ファイルは、ファイル拡張子が. .mshc に変更された zip ファイルです。 .mshc から .zip に拡張子を変更し、コンテンツを抽出します。 Branding_  以下を参照してパッケージ要素をブランド化し、必要に応じて変更します (たとえば、ロゴを VSP ロゴに変更し、Branding.xml ファイルのロゴへの参照、.VSP 固有の Branding.xml 更新など)。

すべての変更が完了したら、必要なブランド要素を含む zip ファイルを作成し、拡張子を .mshc に変更します。

カスタムブランドパッケージを関連付けるには、.mshc ファイルへの参照とコンテンツ .mshc (トピックを含む) を含む MSHA を作成します。  基本的な MSHA を作成する方法については、「MSHA」を参照してください。

Branding.xml ファイルには、トピックにが含まれる場合に、トピック内の特定の項目を一貫して表示するために使用される要素の一覧が含まれてい \<meta name="Microsoft.Help.SelfBranded" content="false"/> ます。  Branding.xml ファイル内の要素の Visual Studio の一覧を次に示します。  このリストは、独自の製品ブランド化のニーズを満たすために、これらの要素 (ロゴ、フィードバック、著作権など) を変更する ISO シェル採用者向けのテンプレートとして使用することを目的としています。

注: "{n}" で示されている変数にはコードの依存関係があります。これらの値を削除または変更すると、エラーが発生し、アプリケーションがクラッシュする可能性があります。 ローカライズ識別子 (例 _locID = "codesnippet") は、Visual Studio ブランド化パッケージに含まれています。

**Branding.xml**

| 要素 | 説明 |
| - | - |
| 機能: | **CollapsibleArea** |
| 次のコマンドを使用します。 | 折りたたみコンテンツコントロールのテキストを展開します |
| **要素** | **Value** |
| ExpandText | Expand |
| CollapseText | [折りたたみ] |
| 機能: | **CodeSnippet** |
| 次のコマンドを使用します。 | コードスニペットコントロールテキスト。  注: "非互換性" 領域があるコードスニペットコンテンツは、スペースに変更されます。 |
| **要素** | **Value** |
| CopyToClipboard | [クリップボードにコピー] |
| ViewColorizedText | 色分け表示 |
| 連結 Edvbtabdisplaylanguage | Visual Basic (サンプル) |
| VBDeclaration | 宣言 |
| VBUsage | 使用 |
| 機能: | **フィードバック、フッター、ロゴ** |
| 次のコマンドを使用します。 | 顧客が電子メールで現在のトピックに関するフィードバックを提供するフィードバックコントロールを提供します。  コンテンツの著作権テキスト。  ロゴの定義。 |
| **要素** | **値 (これらの文字列は、コンテンツの導入者のニーズに合わせて変更できます。)** |
| 侵害 | © 2013 Microsoft Corporation. All rights reserved. |
| SendFeedback | \<a href="{0}" {1}>\</a>このトピックに関するフィードバックを Microsoft に送信してください。 |
| No-results-found-feedbacklink | |
| LogoTitle | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| LogoFileName | vs_logo_bk.gif |
| LogoFileNameHC | vs_logo_wh.gif |
| 機能: | **免責事項** |
| 次のコマンドを使用します。 | 機械翻訳されたコンテンツのケース固有の免責事項のセット。 |
| **要素** | **Value** |
| MT_Editable | この記事は機械翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択して、このページを編集可能モードで表示し、元の英語コンテンツを同時に表示します。 |
| MT_NonEditable | この記事は機械翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択して、このページを編集可能モードで表示し、元の英語コンテンツを同時に表示します。 |
| MT_QualityEditable | この記事は手動で翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択して、このページを編集可能モードで表示し、元の英語コンテンツを同時に表示します。 |
| MT_QualityNonEditable | この記事は手動で翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択して、このページを編集可能モードで表示し、元の英語コンテンツを同時に表示します。 |
| MT_BetaContents | この記事は、予備リリース用に機械翻訳されたものです。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択して、このページを編集可能モードで表示し、元の英語コンテンツを同時に表示します。 |
| MT_BetaRecycledContents | この記事は、暫定版用に手動で翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択して、このページを編集可能モードで表示し、元の英語コンテンツを同時に表示します。 |
| 機能: | **実行** |
| 次のコマンドを使用します。 | オンライントピックリンクのサポート |
| **要素** | **Value** |
| LinkTableTitle | リンクテーブル |
| トピック Enulinktext | \</a>お使いのコンピューターで利用可能な英語版のトピックを表示します。 |
| TopicOnlineLinkText | このトピックをオンラインで表示する \<a href="{0}" {1}>\</a> |
| オンラインテキスト | オンライン |
| 機能: | **ビデオオーディオコントロール** |
| 次のコマンドを使用します。 | ビデオコンテンツの要素とテキストを表示する |
| **要素** | **Value** |
| MultiMediaNotSupported | コンテンツをサポートするには、Internet Explorer 9 以降がインストールされている必要があり {0} ます。 |
| VideoText | ビデオの表示 |
| AudioText | オーディオのストリーミング |
| OnlineVideoLinkText | \<p>このトピックに関連付けられているビデオを表示するには、ここをクリックして {0} \<a href="{1}"> {2} \</a> ください。\</p> |
| オンラインの Audiolinktext | \<p>このトピックに関連付けられているオーディオをリッスンするには、ここをクリックして {0} \<a href="{1}"> {2} \</a> ください。\</p> |
| 機能: | **コンテンツがインストールされていないコントロール** |
| 次のコマンドを使用します。 | contentnotinstalled.htm の表示に使用されるテキスト要素 (文字列) |
| **要素** | **Value** |
| Contentnotのタイトル | コンピューターにコンテンツが見つかりませんでした。 |
| Contentnotの Downloadcontenttext | \<p>コンテンツをコンピューターにダウンロードするに \<a href="{0}" {1}> は、[管理] タブをクリックし \</a> ます。\</p> |
| Contentnotのテキスト | \<p>コンピューターにコンテンツがインストールされていません。 ローカルのヘルプコンテンツのインストールについては、管理者にお問い合わせください。\</p> |
| 機能: | **トピックが見つかりませんコントロール** |
| 次のコマンドを使用します。 | topicnotfound.htm の表示に使用されるテキスト要素 (文字列) |
| **要素** | **Value** |
| トピック Notfound タイトル | コンピューターに要求されたトピックが見つかりません。 |
| トピック Notfound Viewオンラインテキスト | \<p>要求されたトピックはコンピューターに見つかりませんでしたが、 \<a href="{0}" {1}> トピックはオンラインで表示でき \</a> ます。\</p> |
| トピック Notfound Downloadcontenttext | \<p>同様のトピックへのリンクについては、ナビゲーションウィンドウを参照してください。または \<a href="{0}" {1}> 、[管理] タブをクリックして、 \</a> コンテンツをコンピューターにダウンロードしてください。\</p> |
| トピック Notfound Text | \<p>お客様のコンピューターに要求されたトピックが見つかりませんでした。\</p> |
| 機能: | **トピックの破損コントロール** |
| 次のコマンドを使用します。 | topiccorrupted.htm の表示に使用されるテキスト要素 (文字列) |
| **要素** | **Value** |
| TopicCorruptedTitle | 要求されたトピックを表示できません。 |
| TopicCorruptedViewOnlineText | \<p>ヘルプビューアーで、要求されたトピックを表示できません。 トピックの内容または基になるシステムの依存関係にエラーがある可能性があります。\</p> |
| 機能: | **ホームページコントロール** |
| 次のコマンドを使用します。 | ヘルプビューアーの最上位レベルのノードコンテンツの表示をサポートするテキストです。 |
| **要素** | **Value** |
| HomePageTitle | ヘルプビューアーホーム |
| ホームページの概要 | \<p>Microsoft のツール、製品、テクノロジ、サービスを使用するすべてのユーザーにとって重要な情報源である Microsoft ヘルプビューアーへようこそ。 ヘルプビューアーを使用すると、操作方法と参照情報、サンプルコード、技術記事などにアクセスできます。 必要なコンテンツを探すには、目次を参照するか、フルテキスト検索を使用するか、キーワード index を使用してコンテンツ間を移動します。\</p> |
| HomePageContentInstallText | \<p>\<br />[ \<a href="{0}" {1}> コンテンツの管理 \</a> ] タブを使用して、 \<ul> \<li> コンピューターにコンテンツを追加 \</li> \<li> します。ローカルコンテンツの更新プログラムを確認します。 \</li> \<li>コンピューターからコンテンツを削除します。\</li>\</ul>\</p> |
| ホームページの発行書籍 | インストールされたブック |
| ホーム Pagのインストール | コンピューターにコンテンツが見つかりませんでした。 |
| ホームページの Helpsettings | ヘルプコンテンツの設定 |
| HomePageHelpSettingsText | \<p>現在の設定はローカルヘルプです。 ヘルプビューアーには、コンピューターにインストールされているコンテンツが表示されます。 \<br />ヘルプコンテンツのソースを変更するには、Visual Studio のメニューバーで [ヘルプ]、[ヘルプ設定の設定] の順に選択し \<span style="{0}"> \</span> ます。\<br />\</p> |
| Mb | MB |

**branding.js**

branding.js ファイルには、Visual Studio ヘルプビューアーのブランド要素によって使用される JavaScript が含まれています。  次に、ブランド化要素とサポートする JavaScript 関数の一覧を示します。  このファイルのローカライズ対象となるすべての文字列は、このファイルの先頭にある "ローカライズ可能な文字列" セクションで定義されます。  branding.js ファイル内の loc 文字列用に ICL ファイルが作成されました。

|**ブランド化機能**|**JavaScript 関数**|**説明**|
|-|-|-|
|変数...||変数の定義|
|ユーザーコード言語を取得する|setUserPreferenceLang|インデックス # をコード言語にマップします|
|Cookie 値の設定と取得|getCookie、setCookie||
|継承されたメンバー|changeMembersLabel|継承されたメンバーの展開/折りたたみ|
|SelfBranded = False の場合|onLoad|クエリ文字列を読み取り、それが印刷要求かどうかを確認します。  すべての codesnippets を設定して、ユーザーの優先タブにフォーカスを設定します。 印刷要求の場合は、isPrinterFriendly を true に設定します。 ハイコントラストモードを確認します。|
|コード スニペット|addSpecificTextLanguageTagSet||
||getIndexFromDevLang||
||[ChangeTab]||
||setCodesnippetLang||
||setCurrentLang||
||CopyToClipboard||
|CollapsibleArea|addToCollapsibleControlSet|折りたたみ可能なすべてのコントロールオブジェクトを一覧に書き込みます。|
||CA_Click|折りたたみ可能な領域の状態に基づいて、表示するイメージとテキストを定義します。|
|ロゴのコントラストサポート|isBlackBackground ()|背景が黒かどうかを判断するために呼び出されます。  ハイコントラストモードの場合は正確です。|
||isHighContrast()|カラースパンを使用してハイコントラストモードを検出する|
||onHighContrast (黒)|ハイコントラストが検出されると呼び出されます。|
|LST の機能|||
||Addtolanspectexdset (id)||
||updateLST (currentLang)||
||getDevLangFromCodeSnippet (lang)||
|マルチメディア機能|キャプション (開始、終了、テキスト、スタイル)||
||findAllMediaControls (normalizedId)||
||getActivePlayer (normalizedId)||
||captionsOnOff (id)||
||toSeconds (t)||
||getAllComments (ノード)||
||styleRectify (styleName, スタイル値)||
||showCC (id)||
||サブタイトル (id)||

**HTM ファイル**

ブランド化パッケージには、ユーザーのために重要な情報を提供するための一連の HTM ファイルが含まれています。たとえば、インストールされているコンテンツセットを示すセクションを含むホームページや、トピックのローカルセットにトピックが見つからない場合にユーザーに通知するページなどがあります。 これらの HTM ファイルは製品ごとに変更できます。  ISO シェルベンダーは、既定のブランドパッケージを取得し、これらのページの動作とコンテンツを必要に応じて変更できます。  これらのファイルは、ブランド化タグが branding.xml ファイルから対応するコンテンツを取得するために、それぞれのブランドパッケージを参照します。

|**ファイル**|**用途**|**表示されるコンテンツソース**|
|-|-|-|
|homepage.htm|これは、現在インストールされているコンテンツと、そのコンテンツについてユーザーに提示するのに適したその他のメッセージを表示するページです。  このファイルには、追加のメタデータ属性 "Microsoft.Help.Id" content = "-1" があります。これにより、このコンテンツはローカルコンテンツ TOC の先頭に配置されます。||
||<META_HOME_PAGE_TITLE_ADD/>|Branding.xml、タグ \<HomePageTitle>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD/>|Branding.xml、タグ \<HomePageIntroduction>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD/>|Branding.xml、タグ \<HomePageContentInstallText>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD/>|見出しセクション Branding.xml、 \<HomePageInstalledBooks>  \<HomePageNoBooksInstalled> ブックがインストールされていない場合にアプリケーションから生成されるデータです。|
||<HOME_PAGE_SETTINGS_SECTION_ADD/>|見出しセクション Branding.xml タグ \<HomePageHelpSettings> 、セクションテキスト \<HomePageHelpSettingsText> です。|
|topiccorrupted.htm|トピックがローカルセット内に存在するが、何らかの理由で表示できない場合 (破損したコンテンツ)。||
||<META_TOPIC_CORRUPTED_TITLE_ADD/>|Branding.xml、タグ \<TopicCorruptedTitle>|
||<TOPIC_CORRUPTED_SECTION_ADD/>|Branding.xml、タグ \<TopicCorruptedViewOnlineText>|
|topicnotfound.htm|トピックがローカルコンテンツセットに見つからない場合、またはオンラインで利用できない場合||
||<META_TOPIC_NOT_FOUND_TITLE_ADD/>|Branding.xml、タグ \<TopicNotFoundTitle>|
||<META_TOPIC_NOT_FOUND_ID_ADD/>|Branding.xml、タグ \<TopicNotFoundViewOnlineText> + \<TopicNotFoundDownloadContentText>|
||<TOPIC_NOT_FOUND_SECTION_ADD/>|Branding.xml、タグ \<TopicNotFoundText>|
|contentnotinstalled.htm|製品用にローカルコンテンツがインストールされていない場合。||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD/>|Branding.xml、タグ \<ContentNotInstalledTitle>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD/>|Branding.xml、タグ \<ContentNotInstalledDownloadContentText>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD/>|Branding.xml、タグ \<ContentNotInstalledText>|

**CSS ファイル**

Visual Studio ヘルプビューアーのブランド化パッケージには、一貫した Visual Studio ヘルプコンテンツプレゼンテーションをサポートする2つの css ファイルが含まれています。

- .Css-自己ブランド化 = false のレンダリング用の css 要素が含まれています

- Printer .css-自己ブランド化 = false のレンダリング用の css 要素が含まれています

ブランド化された .css ファイルには、Visual Studio トピックプレゼンテーションの定義が含まれます (注意点として、パッケージサービスの .mshc Branding_ に含まれる .css が変更される \<locale> 可能性があります)。

**グラフィックファイル**

Visual Studio のコンテンツには、Visual Studio のロゴとその他のグラフィックスが表示されます。  Visual Studio ヘルプビューアーのブランド化パッケージに含まれるグラフィックファイルの完全な一覧を次に示します。

|**ファイル**|**用途**|**使用例**|
|-|-|-|
|clear.gif|折りたたみ可能な領域を表示するために使用されます||
|footer_slice.gif|フッタープレゼンテーション||
|info_icon.gif|情報を表示するときに使用されます|免責情報|
|online_icon.gif|このアイコンはオンラインリンクに関連付けられています||
|tabLeftBD.gif|コードスニペットコンテナーをレンダリングするために使用されます||
|tabRightBD.gif|コードスニペットコンテナーをレンダリングするために使用されます||
|vs_logo_bk.gif|Branding.xml タグで定義されている通常のコントラストのロゴ参照に使用され \<LogoFileName> ます。  Visual Studio 製品の場合、ロゴ名は vs_logo_bk.gif ます。||
|vs_logo_wh.gif|Branding.xml タグで定義されている通常の高ロゴ参照に使用され \<LogoFileNameHC> ます。  Visual Studio 製品の場合、ロゴ名は vs_logo_wh.gif ます。||
|ccOff.png|キャプショングラフィック||
|ccOn.png|キャプショングラフィック||
|ImageSprite.png|折りたたみ可能な領域を表示するために使用されます|グラフィックの展開または折りたたみ|

## <a name="deploy-a-set-of-topics"></a>一連のトピックを展開する

このチュートリアルでは、MSHA ファイルと、トピックを含む cab または MSHCs のセットで構成されるヘルプビューアーコンテンツ展開セットを作成するための簡単なチュートリアルを紹介します。 MSHA は、一連の cab ファイルまたは .MSHC ファイルを記述する XML ファイルです。 ヘルプビューアーは、MSHA を読み取ってコンテンツの一覧を取得できます (「」を参照してください。CAB または。.MSHC ファイル) をローカルインストールで使用できます。

これは、ヘルプビューアー MSHA の非常に基本的な XML スキーマについて説明したものです。  この brief の概要とサンプルの HelpContentSetup. msha の下に実装例があります。

この入門の目的では、MSHA の名前は HelpContentSetup です。 msha (ファイル名は任意で、拡張子は) です。MSHA)。 HelpContentSetup. msha (次の例を参照) には、使用可能な cab または MSHCs の一覧が含まれている必要があります。  ファイルの種類は、MSHA 内で一貫している必要があります (では、MSHA と CAB ファイルの種類の組み合わせはサポートされません)。 CAB または .mshc ごとに、 \<div class="package"> ... \</div> (次の例を参照) が存在する必要があります。

注: 次の実装例では、ブランド化パッケージが含まれています。 これは、必要な Visual Studio コンテンツのレンダリング要素とコンテンツ動作を取得するために、を含めることが重要です。

サンプル HelpContentSetup. msha ファイル: ("content set name 1" と "content set name 2" などを実際のファイル名に置き換えます)。

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>.
```

1. ローカルフォルダーを作成します ("C:\SampleContent" など)。

2. この例では、.MSHC ファイルを使用してトピックを格納します。  .MSHC は zip で、ファイルの拡張子が .zip からに変更されています。.MSHC.

3. 次の HelpContentSetup. msha をテキストファイルとして作成し (メモ帳を使用してファイルを作成しました)、前述のフォルダーに保存します (手順1を参照)。

クラス "ブランディング" は存在し、一意です。 ブランド化の .mshc がこの入門に含まれており、インストールされているコンテンツにブランドを持たせることができます。また、MSHCs に含まれるコンテンツの動作には、ブランドパッケージに含まれる適切なサポート要素が含まれます。 これを行わないと、取り込んだ (インストールされている) コンテンツの一部ではないサポート項目がシステムによって検索されたときに、エラーが発生します。

Visual Studio ブランド化パッケージを入手するには、.mshc ファイルを C:\Program Files (x86) \Microsoft Help Viewer\v2.3\ にコピーして、作業フォルダーに Branding_en コピーします。

```html
<html>
<head />
<body class="vendor-book">
<div class="details">
<span class="vendor">Your Company</span>
<span class="locale">en-us</span>
<span class="product">Your Company Help Content</span>
<span class="name">Your Company Help Content</span>
</div>
<div class="package-list">
<div class="package">
<span class="name">Your_Company _Content_Set_1</span>
<span class="deployed">True</span>
<a class="current-link" href="Your_Company _Content_Set_1.mshc">Your_Company _Content_Set_1.mshc </a>
</div>
<div class="package">
<span class="name">Your_Company _Content_Set_2</span>
<span class="deployed">True</span>
<a class="current-link"href=" Your_Company _Content_Set_2.mshc "> Your_Company _Content_Set_2.mshc </a>
</div>
<div class="package">
<span class="packageType">branding</span>
<span class="name">Branding_en-US</span>
<span class="deployed">True</span>
<a class="current-link" href="Branding_en-US.mshc">Branding_en-US.mshc</a>
</div>
</div>
</body>
</html>
```

**まとめ**

上記の手順を使用および拡張すると、Vsp は Visual Studio ヘルプビューアー用のコンテンツセットを配置できるようになります。

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>Visual Studio シェルにヘルプを追加する (統合および分離)

**はじめに**

このチュートリアルでは、Visual Studio シェルアプリケーションにヘルプコンテンツを組み込み、それを展開する方法について説明します。

**必要条件**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [Visual Studio 2013 分離シェル再頒布可能パッケージ](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

**概要**

[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]シェルは、 [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] アプリケーションのベースとして使用できる IDE のバージョンです。 このようなアプリケーションには、作成した拡張機能と共に分離シェルが含まれています。 拡張機能をビルドするには、SDK に含まれている分離シェルプロジェクトテンプレートを使用し [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] ます。

分離シェルベースのアプリケーションとそのヘルプを作成するための基本的な手順は次のとおりです。

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]ISO シェル再頒布可能パッケージ (Microsoft ダウンロード) を入手します。

2. Visual Studio で、分離シェルに基づくヘルプ拡張機能を作成します。たとえば、このチュートリアルで後ほど説明する Contoso Help 拡張機能を作成します。

3. 拡張機能と ISO シェル再頒布可能パッケージを展開 MSI (アプリケーションセットアップ) にラップします。 このチュートリアルには、セットアップ手順は含まれていません。

Visual Studio コンテンツストアを作成します。 統合シェルシナリオでは、次のように Visual Studio12 を製品カタログ名に変更します。

- フォルダー C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15. の作成

- CatalogType.xml という名前のファイルを作成し、フォルダーに追加します。 ファイルには、次のコード行が含まれている必要があります。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

レジストリでコンテンツストアを定義します。 統合シェルの場合は、VisualStudio15 を製品カタログ名に変更します。

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15

   キー: LocationPath 文字列値: C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15\

- HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15\en-US

   キー: CatalogName String 値: [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Documentation

**プロジェクトを作成する**

分離シェル拡張機能を作成するには、次のようにします。

1. Visual Studio の [ **ファイル**] で、[ **新しいプロジェクト**] を選択し、[ **その他のプロジェクトの種類] の** [ **拡張機能**] を選択し、[  **visual studio Shell 分離**] を選択します。 プロジェクトに名前を指定して、 `ContosoHelpShell` Visual Studio の分離シェルテンプレートに基づく機能拡張プロジェクトを作成します。

2. ソリューションエクスプローラーの ContosoHelpShellUI プロジェクトで、[リソースファイル] フォルダーの [ApplicationCommands] を開きます。 この行がコメントアウトされていることを確認します ("No_Help" を検索してください)。 `<!-- <define name="No_HelpMenuCommands"/> -->`

3. F5 キーを押してコンパイルし、 **デバッグ** を実行します。 分離シェル IDE の実験用インスタンスで、[ **ヘルプ** ] メニューを選択します。 [ヘルプの **表示**]、[ヘルプ **コンテンツの追加と削除**]、および [ヘルプ設定の **設定** ] の各コマンドが表示されていることを確認します。

4. ソリューションエクスプローラーの ContosHelpShell プロジェクトで、[シェルのカスタマイズ] フォルダーの ContosoHelpShell を開きます。 Contoso ヘルプカタログを定義するには、次の行を追加します。

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. ソリューションエクスプローラーの ContosHelpShell プロジェクトで、[シェルのカスタマイズ] フォルダーの ContosoHelpShell を開きます。 F1 ヘルプを有効にするには、次の行を追加します。

    ```
    // F1 Help Provider

    [$RootKey$\HelpProviders\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
    "Name"="13407"
    "Package"="{DA9FB551-C724-11d0-AE1F-00A0C90FFFC3}"
    @="Help3 Provider"
    [$RootKey$\HelpProviders]
    @="{C99BDC23-FF29-46bf-9658-ADD634CCAED8}"
    [$RootKey$\Services\{C99BDC23-FF29-46bf-9658-ADD634CCAED8}]
    "Name"="Help3 Provider"
    @="{4A791146-19E4-11D3-B86B-00C04F79F802}"
    ```

6. ソリューションエクスプローラーの ContosoHelpShell ソリューションのコンテキストメニューで、[ **プロパティ** ] メニュー項目を選択します。 [ **構成プロパティ**] で [ **Configuration Manager**] を選択します。 [ **構成** ] 列で、[デバッグ] の値を [リリース] に変更します。

7. ソリューションをビルドします。 これにより、リリースフォルダーに一連のファイルが作成されます。これは次のセクションで使用します。

デプロイされているかのようにこれをテストするには:

1. Contoso を展開するコンピューターで、ダウンロードした (上記の) ISO シェルをインストールします。

2. \\ファイル (x86) にフォルダーを作成 \\ し、という名前を指定し `Contoso` ます。

3. ContosoHelpShell release フォルダーの内容を、\Contoso\ フォルダーにコピーし \\ ます。

4. [**スタート**] メニューの [**実行**] をクリックし、「」と入力して、レジストリエディターを起動し `Regedit` ます。 レジストリエディターで、[ **ファイル**]、[ **インポート**] の順に選択します。 ContosoHelpShell プロジェクトフォルダーを参照します。 ContosoHelpShell サブフォルダーで、ContosoHelpShell を選択します。

5. コンテンツストアを作成します。

    ISO シェルの場合-Contoso コンテンツストア C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\ContosoDev12 を作成する

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]Integrated Shell の場合は、フォルダー C:\ProgramData\Microsoft\HelpLibrary2\Catalogs\VisualStudio15 を作成します。

6. CatalogType.xml を作成し、次の内容を含むコンテンツストア (前の手順) に追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. 次のレジストリキーを追加します。

    HKLM\SOFTWARE\Wow6432Node\Microsoft\Help\v2.3\Catalogs\VisualStudio15Key: LocationPath 文字列値:

    ISO シェルの場合:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] 統合シェル:

    C:ProgramDataMicrosoftHelpLibrary2CatalogsVisualStudio15en-US

    キー: CatalogName String value: [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] Documentation。 ISO シェルの場合、これはカタログの名前です。

8. コンテンツ (cab または .MSHC と MSHA) をローカルフォルダーにコピーします。

9. コンテンツストアをテストするための統合シェルコマンドラインの例。 ISO シェルの場合は、製品に一致するように、カタログと launchingApp の値を適宜変更します。

     "C:\Program Files (x86) \Microsoft Help Viewer\v2.3\HlpViewer.exe"/catalogName VisualStudio15/helpquery method = "page&id = ContosoTopic0"/launchingapp Microsoft, VisualStudio, 12.0

10. (Contoso アプリのルートから) Contoso アプリケーションを起動します。 ISO シェル内で [ **ヘルプ** ] メニュー項目を選択し、[ **ヘルプ** 設定の設定] を [ **ローカルヘルプを使用** する] に変更します。

11. シェル内で [ **ヘルプ** ] メニュー項目を選択し、[ **ヘルプの表示**] をクリックします。 ローカルヘルプビューアーが起動します。 [ **コンテンツの管理** ] タブを選択します。[ **インストールソース**] で、[ **ディスク** ] オプションボタンをクリックします。 [ **...** ] ボタンをクリックして、(前の手順でローカルフォルダーにコピーした) Contoso コンテンツを含むローカルフォルダーを参照します。 [HelpContentSetup. msha] を選択します。 Contoso は、選択した書籍に書籍として表示されます。 [ **追加**] を選択し、[ **更新** ] ボタン (右下隅) を選択します。

12. Contoso IDE 内で f1 キーを押して、F1 機能をテストします。

## <a name="additional-resources"></a>その他のリソース

ランタイム API については、「 [Windows ヘルプ API](/previous-versions/windows/desktop/helpapi/helpapi-portal)」を参照してください。

ヘルプ API を活用する方法の詳細については、「 [ヘルプビューアーのコード例](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples)」を参照してください。

[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)で機能の提案を送信できます。
