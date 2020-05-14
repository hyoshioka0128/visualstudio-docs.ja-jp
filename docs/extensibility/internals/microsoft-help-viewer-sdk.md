---
title: マイクロソフト ヘルプ ビューアー SDK |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 620d7dcd-d462-475e-a449-fbfa06ff12c5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 721623edabcaf3b395a143dd193cae3fd71d93d6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707153"
---
# <a name="microsoft-help-viewer-sdk"></a>Microsoft ヘルプ ビューアー SDK

この記事では、Visual Studio ヘルプ ビューアー インテグレーターの次のタスクについて説明します。

- トピックの作成 (F1 サポート)

- ヘルプ ビューアーのコンテンツ ブランド化パッケージの作成

- 一連の記事の展開

- ヘルプを Visual Studio シェルに追加する (統合または分離)

- その他のリソース

## <a name="create-a-topic-f1-support"></a>トピックの作成 (F1 サポート)

このセクションでは、提示されたトピックのコンポーネントの概要、トピック要件、トピックの作成方法の簡単な説明 (F1 サポート要件を含む) と最後に、そのレンダリング結果を含むトピックの例を示します。

**ヘルプ ビューアのトピックの概要**

トピックがレンダリング用に呼び出されると、ヘルプ ビューアーは、インストール時または最終更新時にトピックに関連付けられているブランド化パッケージ要素とトピック XHTML を取得し、2 つを組み合わせて表示されるコンテンツ ビュー (ブランド化データ + トピック データ) を表示します。  ブランディングパッケージには、ロゴ、コンテンツの動作のサポート、およびブランディングテキスト(著作権など)が含まれています。  ブランド化パッケージの要素の詳細については、後述の「ブランドパッケージの作成」を参照してください。  トピックに関連付けられたブランド化パッケージがない場合、ヘルプ ビューアーは、ヘルプ ビューアー アプリケーション ルート (Branding_en-US.mshc) にあるフォールバック ブランド パッケージを使用します。

**ヘルプ ビューアーのトピック要件**

ヘルプ ビューアー内で正しく表示されるようにするには、未加工のトピック コンテンツが W3C Basic 1.1 XHTML である必要があります。

通常、トピックには次の 2 つのセクションがあります。

- メタデータ (コンテンツ メタデータ参照を参照): トピックに関するデータ (トピック固有 ID、キーワード値、トピック TOC ID、親ノード ID など)。

- 本文のコンテンツ: W3C Basic 1.1 XHTML に準拠しており、サポートされているコンテンツの動作 (折りたたみ可能な領域、コード スニペットなど) が含まれています。完全なリストは以下に示されています)。

Visual Studio ブランド パッケージでサポートされているコントロール:

- リンク

- コードスニペット

- 折りたたみエリア

- 継承されたメンバー

- 言語固有のテキスト

サポートされている言語文字列 (大文字と小文字は区別されません):

- JavaScript

- csharp または c#

- cplusplus または visualc++ または c++

- jscript

- ビジュアルベーシックまたはvb

- f# または fsharp または fs

- other - 言語名を表す文字列

**ヘルプ ビューアのトピックを作成する**

ContosoTopic4.htm という名前の新しい XHTML ドキュメントを作成し、タイトル タグ (以下) を含めます。

```html
<html>
<head>
<title>Contoso Topic 4</title>
</head>

<body>

</body>
</html>

```

次に、トピックの表示方法 (自己ブランド化するかどうか)、このトピックを参照する方法を定義するデータを追加する F1、このトピックが TOC 内に存在する場所、ID (他のトピックによるリンク参照用)など。サポートされているメタデータの完全なリストについては、以下の「コンテンツ メタデータ」の表を参照してください。

- この場合、独自のブランド化パッケージを使用します。

- IDE プロパティ バッグに指定された F1 値と一致する F1 メタ名と値 (「Microsoft.Help.F1」 コンテンツ="ContosoTopic4") を追加します。 (詳細については、F1 サポートのセクションを参照してください。これは、IDE で F1 が選択されたときにこのトピックを表示するために、IDE 内からの F1 呼び出しに一致する値です。

- トピック ID を追加します。 これは、このトピックにリンクするために他のトピックで使用される文字列です。 このトピックのヘルプ ビューアー ID です。

- TOC の場合は、このトピックの親ノードを追加して、このトピックの TOC ノードの表示場所を定義します。

- TOC の場合は、このトピックのノード順を追加します。 親ノードに子ノード`n`の数がある場合は、このトピックの位置の子ノードの順序で定義します。 たとえば、このトピックは 4 個の子トピックの 4 つです。

メタデータ セクションの例:

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

**トピックボディ**

トピックの本文 (ヘッダーとフッターを含まない) には、ページ リンク、メモ セクション、折りたたみ可能な領域、コード スニペット、および言語固有のテキストのセクションが含まれます。  このトピックのこれらの領域については、ブランディングセクションを参照してください。

1. トピックタイトルタグを追加します。`<div class="title">Contoso Topic 4</div>`

2. 注記セクションを追加します。`<div class="alert"> add your table tag and text </div>`

3. 折りたたみ可能な領域を追加します。`<CollapsibleArea Expanded="1" Title="Collapsible Area Test Heading"> add text  </CollapsibleArea>`

4. コード スニペットを追加します。`<CodeSnippet EnableCopyCode="true" Language="CSharp" ContainsMarkup="false" DisplayLanguage="C#" > a block of code </CodeSnippet>`

5. コード言語固有のテキストを追加`<LanguageSpecificText devLangcs="CS" devLangvb="VB" devLangcpp="C++" devLangnu="F#" />`する:`devLangnu=`他の言語を入力できます。 たとえば、`devLangnu="Fortran"`コード スニペットの表示言語 = Fortran のときに Fortran を表示します。

6. ページリンクの追加:`<a href="ms-xhelp:///?Id=ContosoTopic1">Main Topic</a>`

> [!NOTE]
> 注: サポートされていない新しい「表示言語」(例えば、F#、Cobol、Fortran)のコードは、コードスニペットの色付けはモノクロになります。

**ヘルプ ビューア のトピックの例**このコードは、メタデータ、コード スニペット、折りたたみ可能領域、および言語固有のテキストを定義する方法を示しています。

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

Visual Studio では、F1 を選択すると、IDE 内のカーソルの配置から指定された値が生成され、(カーソル位置に基づいて) 指定された値を "プロパティ バッグ" に設定します。 カーソルがフィーチャ x の上にある場合、フィーチャ x はアクティブ/フォーカス中になり、プロパティ バッグに値が設定されます。  F1 が選択されると、プロパティ バッグが設定され、Visual Studio F1 コードは、顧客の既定のヘルプ ソースがローカルまたはオンライン (オンラインは既定) であるかどうかを確認し、ユーザー設定 (オンラインは既定) に基づいて適切な文字列を作成します (オンラインは既定です) - シェル実行 (exe 起動のヘルプ管理者ガイドを参照)。、または、パラメータリストにキーワードが含まれている MSDN URL を指定します。

複数値文字列と呼ばれる F1 に対して 3 つの文字列が返された場合は、最初の用語を使用してヒットを探し、見つかった場合は完了です。ない場合は、次の文字列に移動します。  注文事項。 複数値キーワードの表示は、最短の文字列に対して最長の文字列である必要があります。  複数値のキーワードの場合にこれを確認するには、選択したキーワードを含むオンラインの F1 URL 文字列を参照してください。

Visual Studio 2012 では、意図的にオンラインとオフラインの間でより強い分割を行ったので、ユーザーの設定がオンラインの場合、Visual Studio 2010 で使用していたヘルプ ライブラリ エージェントを介してルーティングするのではなく、MSDN のオンライン クエリ サービスに直接 F1 要求を渡しました。 その後、"ベンダーコンテンツがインストールされている = true" の状態に依存して、そのコンテキストで何か違うことを行うかどうかを判断します。 true の場合、お客様がサポートする内容に応じて、この解析とルーティングのロジックを実行します。 false の場合は、MSDN に移動します。 ユーザーの設定が [ローカル] の場合、すべての呼び出しはローカル ヘルプ エンジンに移動します。

F1 フロー図:

![F1 フロー](../../extensibility/internals/media/f1flow.png "F1フロー")

ヘルプ ビューアーの既定のヘルプ コンテンツ ソースがオンライン (ブラウザーで起動) に設定されている場合:

- Visual Studio パートナー (VSP) 機能は、F1 プロパティ バッグに値を出力します (プロパティ バッグ prefix.keyword とレジストリで見つかったプレフィックスのオンライン URL) F1 は、VSP URL+ パラメーターをブラウザーに送信します。

- Visual Studio の機能 (言語エディター、Visual Studio 固有のメニュー項目など) : F1 は、ブラウザーに Visual Studio の URL を送信します。

ヘルプ ビューアーの既定のヘルプ コンテンツ ソースがローカル ヘルプ (ヘルプ ビューアーで起動) に設定されている場合:

- キーワードが F1 プロパティ バッグとローカル ストア インデックスの間でキーワードを一致させる VSP 機能 (つまり、プロパティ バッグ prefix.keyword = ローカル ストア インデックスで見つかった値) F1 はヘルプ ビューアーでトピックを表示します。

- Visual Studio の機能 (VSP が Visual Studio の機能から出力されたプロパティ バッグをオーバーライドするオプションはありません): F1 は、ヘルプ ビューアーで Visual Studio トピックを表示します。

次のレジストリ値を設定して、ベンダーヘルプコンテンツの F1 フォールバックを有効にします。 F1 フォールバックとは、ヘルプ ビューアーが F1 ヘルプ コンテンツをオンラインで検索するように設定され、ベンダーのコンテンツがユーザーのハード ドライブにローカルにインストールされることを意味します。 ヘルプ ビューアーでは、オンライン ヘルプの既定の設定であっても、コンテンツのローカル ヘルプを参照する必要があります。

1. ヘルプ 2.3 レジストリ キーの下に**Vendor コンテンツ**の値を設定します。

   - 32 ビットオペレーティング システムの場合:

        HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v2.3\Catalogs\VisualStudio15

        "ベンダーコンテンツ"=dword:00000001

   - 64 ビット オペレーティング システムの場合:

        HKEY_LOCAL_MACHINE\ソフトウェア\Wow6432ノード\マイクロソフト\ヘルプ\v2.3\カタログ\VisualStudio15

        "ベンダーコンテンツ"=dword:00000001

2. ヘルプ 2.3 レジストリ キーの下にパートナーの名前空間を登録します。

   - 32 ビットオペレーティング システムの場合:

      HKEY_LOCAL_MACHINE\ソフトウェア\マイクロソフト\ヘルプ\v2.3\パートナー<em> \\<名前空間\></em>

      "場所"="オフライン"

   - 64 ビット オペレーティング システムの場合:

      HKEY_LOCAL_MACHINE\ソフトウェア\Wow6432ノード\マイクロソフト\ヘルプ\v2.3\パートナー<em> \\<名前空間\></em>

      "場所"="オフライン"

**ベース ネイティブ名前空間の解析**

基本ネイティブ名前空間の解析を有効にするには、レジストリで次の名前で新しい DWORD を追加し、その値を 1 (サポートするカタログ キーの下) に設定します。  たとえば、Visual Studio カタログを使用する場合は、パスにキーを追加できます。

HKEY_LOCAL_MACHINE\ソフトウェア\Wow6432ノード\マイクロソフト\ヘルプ\v2.3\カタログ\VisualStudio15

ヘッダー/メソッドの形式で F1 キーワードが検出されると、'/' 文字が解析され、次の構文が生成されます。

- HEADER: レジストリに登録するために使用できる名前空間になります

- メソッド: これは渡されるキーワードになります。

たとえば、カスタム ライブラリというカスタム ライブラリと MyTestMethod というメソッドを指定すると、F1 要求が入ったときには、`CustomLibrary/MyTestMethod`という形式の形式になります。

ユーザーは、パートナー ハイブの下で名前空間として CustomLibrary を登録し、必要な場所キーを提供し、クエリに渡されるキーワードは MyTestMethod になります。

**IDE でヘルプデバッグツールを有効にする**

次のレジストリ キーと値を追加します。

::: moniker range="vs-2017"

**HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\15.0\ダイナミック ヘルプ**

::: moniker-end

::: moniker range=">=vs-2019"

**HKEY_CURRENT_USER\ソフトウェア\マイクロソフト\VisualStudio\16.0\ダイナミック ヘルプ**

::: moniker-end

値: 小売データのデバッグ出力を表示: YES

IDE の [ヘルプ] メニュー項目の [**ヘルプ コンテキストのデバッグ**] を選択します。

**コンテンツメタデータ**

次の表では、角かっこの間に表示される文字列はプレースホルダーで、認識された値に置き換える必要があります。 たとえば、\<メタ名="Microsoft.Help.Locale"コンテンツ="[言語コード]"/>では、「[言語コード]」は"en-us"などの値に置き換える必要があります。

| プロパティ (HTML 表現) | 説明 |
| - | - |
| \<メタ名="Microsoft.Help.ロケール"コンテンツ="[言語コード]"/> | このトピックのロケールを設定します。 このタグをトピックで使用する場合は、1 回だけ使用し、他の Microsoft ヘルプ タグの上に挿入する必要があります。 このタグを使用しない場合、トピックの本文テキストは、製品ロケールに関連付けられているワード ブレーカー (指定されている場合) を使用してインデックス付けされます。それ以外の場合は、en-us ワード ブレーカーが使用されます。 このタグは ISOC RFC 4646 に準拠しています。 Microsoft ヘルプが正しく動作することを確認するには、一般的な言語属性ではなく、このプロパティを使用します。 |
| \<メタ名="Microsoft.Help.TopicLocale" コンテンツ="[言語コード]" /> | 他のロケールも使用される場合に、このトピックのロケールを設定します。 このタグがトピックで使用される場合は、1 回だけ使用する必要があります。 カタログに複数の言語のコンテンツが含まれている場合は、このタグを使用します。 カタログ内の複数のトピックに同じ ID を指定できますが、それぞれ固有の TopicLocale を指定する必要があります。 カタログのロケールに一致する TopicLocale を指定するトピックは、目次に表示されるトピックです。 ただし、トピックのすべての言語バージョンが検索結果に表示されます。 |
| \<タイトル> [\<タイトル] /タイトル> | このトピックのタイトルを指定します。 このタグは必須であり、トピック内で 1 回だけ使用する必要があります。 トピックの本文にタイトル\<div> セクションが含まれていない場合、このタイトルはトピックおよび目次に表示されます。 |
| \<メタ名=" マイクロソフトヘルプ.キーワード"コンテンツ="[キーワードフレーズ]/> | ヘルプ ビューアーのインデックス ペインに表示されるリンクのテキストを指定します。 リンクをクリックすると、トピックが表示されます。 トピックに複数の索引キーワードを指定することも、このトピックへのリンクを索引に表示したくない場合は、このタグを省略することもできます。 以前のバージョンのヘルプの "K" キーワードは、このプロパティに変換できます。 |
| \<メタ名="マイクロソフトヘルプ.ID"コンテンツ="[トピックID]"/> | このトピックの識別子を設定します。 このタグは必須であり、トピック内で 1 回だけ使用する必要があります。 ID は、同じロケール設定を持つカタログ内のトピック間で一意である必要があります。 別のトピックでは、この ID を使用してこのトピックへのリンクを作成できます。 |
| \<メタ名="Microsoft.ヘルプ.F1"コンテンツ="[システム.Windows.コントロール.プリミティブ.Iリサイクルアイテムコンテナジェネレータ]/> | このトピックの F1 キーワードを指定します。 1 つのトピックに複数の F1 キーワードを指定するか、アプリケーション・ユーザーが F1 を押したときにこのトピックを表示しない場合は、このタグを省略することができます。 通常、トピックに対して指定される F1 キーワードは 1 つだけです。 以前のバージョンのヘルプの "F" キーワードは、このプロパティに変換できます。 |
| \<メタ名="説明"コンテンツ="[トピックの説明]" /> | このトピックの内容の簡単な概要を示します。 このタグがトピックで使用される場合は、1 回だけ使用する必要があります。 このプロパティはクエリ ライブラリから直接アクセスされます。インデックス ファイルには格納されません。 |
| メタ名="Microsoft.Help.TocParent" コンテンツ="[parent_Id]/> | 目次でこのトピックの親トピックを指定します。 このタグは必須であり、トピック内で 1 回だけ使用する必要があります。 値は親のMicrosoft.Help.Idです。 トピックは、目次に 1 つの場所だけを持つことができます。 "-1" は TOC ルートのトピック ID と見なされます。 では[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]、そのページはヘルプビューアのホームページです。 これは、TopcParent=-1 を一部のトピックに追加して、トップ レベルに表示されるようにするのと同じ理由です。 ヘルプ ビューアーのホーム ページは、システム ページなので、置き換え不可能です。 VSP が ID が -1 のページを追加しようとすると、コンテンツ セットに追加される場合がありますが、ヘルプ ビューアは常にシステム ページを使用します - ヘルプ ビューア ホーム |
| \<メタ名="Microsoft.Help.TocOrder" コンテンツ="[正の整数]"/> | 目次内でこのトピックがピア トピックに対して相対的に表示される場所を指定します。 このタグは必須であり、トピック内で 1 回だけ使用する必要があります。 値は整数です。 より大きい値の整数を指定するトピックの上に、低い値の整数を指定するトピックが表示されます。 |
| \<メタ名="Microsoft.Help.製品"コンテンツ="[製品コード]"/> | このトピックで説明する製品を指定します。 このタグがトピックで使用される場合は、1 回だけ使用する必要があります。 この情報は、ヘルプ インデクサーに渡されるパラメーターとして指定することもできます。 |
| \<メタ名="マイクロソフトヘルプ.製品バージョン"コンテンツ="[バージョン番号]"/> | このトピックで説明する製品のバージョンを指定します。 このタグがトピックで使用される場合は、1 回だけ使用する必要があります。 この情報は、ヘルプ インデクサーに渡されるパラメーターとして指定することもできます。 |
| \<メタ名="Microsoft.Help.カテゴリ"コンテンツ="[文字列]/> | コンテンツのサブセクションを識別するために製品によって使用されます。 トピックの複数のサブセクションを識別することも、リンクでサブセクションを識別しない場合は、このタグを省略することもできます。 このタグは、トピックが以前のバージョンのヘルプから変換されるときに、TargetOS および TargetFrameworkMoniker の属性を格納するために使用されます。 コンテンツの形式は、属性名:属性値です。 |
| \<メタ名="Microsoft.Help.TopicVersion コンテンツ="[トピックバージョン番号]"/> | カタログに複数のバージョンが存在する場合に、このバージョンのトピックを指定します。 Microsoft.Help.Id一意であることが保証されないため、カタログ内に複数のバージョンのトピックが存在する場合、たとえばカタログに .NET Framework 3.5 のトピックと .NET Framework 4 のトピックが含まれ、両方が同じMicrosoft.Help.Idがある場合に、このタグが必要です。 |
| \<メタ名="セルフブランド"コンテンツ="[TRUEまたは偽]"/> | このトピックでヘルプ ライブラリ マネージャーのスタートアップ ブランド化パッケージを使用するか、トピック固有のブランド化パッケージを使用するかを指定します。 このタグは TRUE または FALSE にする必要があります。 TRUE の場合、関連トピックのブランド化パッケージは、ヘルプ ライブラリ マネージャーの起動時に設定されるブランド化パッケージよりも優先され、他のコンテンツのレンダリングと異なる場合でも、意図したとおりに表示されます。 FALSE の場合、ヘルプ ライブラリ マネージャーの起動時に設定されるブランド化パッケージに従って現在のトピックが表示されます。 デフォルトでは、ヘルプライブラリマネージャーは、SelfBranded変数がTRUEとして宣言されていない限り、自己ブランド化は偽であると仮定します。したがって、メタ名="自己ブランド\<"コンテンツ="FALSE"/>を宣言する必要はありません。 |

## <a name="create-a-branding-package"></a>ブランド化パッケージの作成

Visual Studio リリースには、Visual Studio パートナー向けの分離シェルと統合シェルなど、さまざまな Visual Studio 製品が含まれています。  これらの各製品には、ある程度のトピックベースのヘルプ コンテンツ ブランド化のサポートが必要です。  たとえば、Visual Studio のトピックでは一貫したブランド表示が必要ですが、ISO シェルをラップする SQL Studio では、トピックごとに独自のヘルプ コンテンツ ブランディングが必要です。  統合シェル パートナーは、独自のトピック ブランドを維持しながら、ヘルプ トピックを親の Visual Studio 製品ヘルプ コンテンツ内に配置する場合があります。

ブランド化パッケージは、ヘルプ ビューアーを含む製品によってインストールされます。  ビジュアル スタジオ製品の場合:

- フォールバック ブランド パッケージ (Branding_\<ロケール>.mshc) は、ヘルプ ビューアー言語パックによってヘルプ ビューアー 2.3 アプリ ルート (例: C:\Program Files (x86)\Microsoft ヘルプ ビューアー\v2.3) にインストールされます。  これは、製品ブランド化パッケージがインストールされていない (コンテンツがインストールされていない) 場合や、インストールされているブランドパッケージが破損している場合に使用されます。  Visual Studio の要素 (ロゴとフィードバック) は、アプリ ルート フォールバック ブランド化パッケージを使用する場合は無視されます。

- Visual Studio コンテンツがコンテンツ パッケージ サービスからインストールされると、ブランド化パッケージもインストールされます (初めてのコンテンツ インストール シナリオ)。  ブランド化パッケージに更新がある場合、次のコンテンツの更新または追加のパッケージのインストール アクションが発生したときに、更新プログラムがインストールされます。

Microsoft ヘルプ ビューアーでは、トピックのメタデータに基づくトピックのブランド化がサポートされています。

- トピックメタデータで自己ブランド化 = true を定義する場合は、トピックを元のとおりにレンダリングし、(ブランディングに関しては) 何もしません。

- トピックメタデータで自己ブランド化 = false が定義されている場合は、TopicVendor メタデータ値に関連付けられたブランド化パッケージを使用します。

- トピックメタデータが name="Microsoft.Help.TopicVendor" コンテンツ\<= ベンダー MSHA>のブランド化パッケージ名を定義している場合は、コンテンツ値で定義されたブランド化パッケージを使用します。

- Visual Studio カタログ内には、ブランドパッケージの優先アプリケーションがあります。  最初の Visual Studio の既定のブランド化が適用され、次にトピック メタデータで定義され、関連付けられたブランド化パッケージでサポートされている場合 (インストール msha で定義されている)、ベンダー定義のブランド化がオーバーライドとして適用されます。

ブランド化要素は、通常、次の 3 つの主要なカテゴリに分類されます。

- ヘッダー要素 (例としてフィードバック リンク、条件付き免責事項テキスト、ロゴが含まれます)

- コンテンツの動作 (例として、展開/折りたたみコントロールテキスト要素、コード スニペット要素など)

- フッター要素(著作権の例)

ブランド要素として見なされる項目は次のとおりです(この仕様で詳しく説明します)。

- カタログ/製品ロゴ (例: Visual Studio)

- フィードバックリンクと電子メール要素

- 免責事項テキスト

- 著作権テキスト

Visual Studio ヘルプ ビューアーのブランド化パッケージのサポート ファイルには、次のものがあります。

- グラフィック(ロゴ、アイコンなど)

- Branding.js - コンテンツの動作をサポートするスクリプトファイル

- Branding.xml - カタログ コンテンツ間で一貫して使用される文字列。  注: branding.xml の Visual Studio ローカライズ テキスト要素の\<場合、_locID=" 一意の値>」

- Branding.css - プレゼンテーションの一貫性のためのスタイル定義

- 印刷.css - 一貫した印刷プレゼンテーションのスタイル定義

前述のように、ブランディングパッケージはトピックに関連付けられます。

- SelfBranded = false がメタデータで定義されている場合、トピックはカタログ ブランド パッケージを継承します。

- または、SelfBranded = false で、MSHA で定義され、コンテンツがインストールされたときに利用可能な一意のブランドパッケージがある場合

カスタム ブランド化パッケージ (VSP コンテンツ、SelfBranded=True) を実装する VSP の場合、フォールバック ブランド パッケージ (ヘルプ ビューアーと共にインストール) を開始し、必要に応じてファイルの名前を変更する方法があります。  Branding_\<ロケール>.mshc ファイルは、ファイル拡張子が .mshc に変更された zip ファイルであるため、拡張子を .mshc から .zip に変更して内容を抽出するだけです。  以下のパッケージ要素のブランド化と変更 (たとえば、ロゴを VSP ロゴに変更し、Branding.xml ファイルのロゴへの参照を変更したり、VSP 仕様ごとに Branding.xml を更新したりするなど) を参照してください。

すべての変更が完了したら、目的のブランド化要素を含む zip ファイルを作成し、拡張子を .mshc に変更します。

カスタム ブランド化パッケージを関連付けるには、MSHA を作成し、ブランド mshc ファイルへの参照とコンテンツ mshc (トピックを含む) を含むファイルを含みます。  基本的な MSHA の作成方法については、以下の「MSHA」を参照してください。

Branding.xml ファイルには、トピックにメタ名="Microsoft.Help.SelfBranded" コンテンツが含\<まれている場合に、トピック内の特定の項目を一貫してレンダリングするために使用される要素の一覧が含 >まれています。  ブランド化.xml ファイル内の要素の Visual Studio リストは、以下のとおりです。  このリストは、ISO Shell の導入者が自社の製品ブランド化のニーズを満たすためにこれらの要素 (ロゴ、フィードバック、著作権など) を変更するテンプレートとして使用することを目的としています。

注: "{n}" で示される変数にはコードの依存関係があります - これらの値を削除または変更するとエラーが発生し、アプリケーションがクラッシュする可能性があります。 ローカライズ識別子 (例_locID="codesnippet.n") は、Visual Studio ブランド パッケージに含まれています。

**ブランディング.xml**

| | |
| - | - |
| 機能: | **折りたたみエリア** |
| 次のコマンドを使用します。 | 展開コンテンツ コントロールテキストを折りたたみます。 |
| **要素** | **Value** |
| テキストを展開する | expand |
| 折りたたむテキスト | [折りたたみ] |
| 機能: | **コードスニペット** |
| 次のコマンドを使用します。 | コード スニペット コントロール テキスト。  注意: 「改行なし」スペースを含むコード スニペットのコンテンツはスペースに変更されます。 |
| **要素** | **Value** |
| クリップボードにコピー | [クリップボードにコピー] |
| 色分けされたテキストを表示します。 | 色分けされたビュー |
| 複合 VB タブ表示言語 | ビジュアル ベーシック (サンプル) |
| VB 宣言 | 宣言 |
| VB の使用法 | 使用法 |
| 機能: | **フィードバック、フッター、ロゴ** |
| 次のコマンドを使用します。 | お客様が電子メールで現在のトピックに関するフィードバックを提供するためのフィードバック コントロールを提供します。  コンテンツの著作権テキスト。  ロゴ定義。 |
| **要素** | **値 (これらの文字列は、コンテンツ導入者のニーズに合わせて変更できます)。** |
| 著作権 | © 2013 Microsoft Corporation. All rights reserved. |
| フィードバックを送信します。 | \<a href=" "{0}>{1}フィードバック\<を送信する / a このトピックに関する>をマイクロソフトに送信します。 |
| フィードバックリンク | |
| ロゴタイトル | [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)] |
| ロゴファイル名 | vs_logo_bk.gif |
| ファイル名HC | vs_logo_wh.gif |
| 機能: | **免責 事項** |
| 次のコマンドを使用します。 | 機械翻訳コンテンツに対するケース固有の免責事項のセット。 |
| **要素** | **Value** |
| MT_Editable | この記事は機械翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択すると、このページが編集可能モードで表示され、英語の元のコンテンツと同時に表示されます。 |
| MT_NonEditable | この記事は機械翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択すると、このページが編集可能モードで表示され、英語の元のコンテンツと同時に表示されます。 |
| MT_QualityEditable | この記事は手動で翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択すると、このページが編集可能モードで表示され、英語の元のコンテンツと同時に表示されます。 |
| MT_QualityNonEditable | この記事は手動で翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択すると、このページが編集可能モードで表示され、英語の元のコンテンツと同時に表示されます。 |
| MT_BetaContents | この記事は、予備リリース用に翻訳されたマシンです。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択すると、このページが編集可能モードで表示され、英語の元のコンテンツと同時に表示されます。 |
| MT_BetaRecycledContents | この資料は、手動で暫定リリース用に翻訳されました。 インターネットに接続している場合は、[このトピックをオンラインで表示する] を選択すると、このページが編集可能モードで表示され、英語の元のコンテンツと同時に表示されます。 |
| 機能: | **リンクテーブル** |
| 次のコマンドを使用します。 | オンライン トピック リンクのサポート |
| **要素** | **Value** |
| リンクテーブルタイトル | リンクテーブル |
| トピックEnuリンクテキスト | コンピュータで利用可能な\<このトピックの英語版 /a>を表示します。 |
| トピックオンラインリンクテキスト | このトピック\<を参照してください a{0} {1} href=" " オンライン\<>/a> |
| オンラインテキスト | オンライン |
| 機能: | **ビデオ オーディオ コントロール** |
| 次のコマンドを使用します。 | ビデオ コンテンツの要素とテキストを表示する |
| **要素** | **Value** |
| マルチメディアがサポートされていません | コンテンツをサポート{0}するには、Internet Explorer 9 以降をインストールする必要があります。 |
| ビデオテキスト | ビデオの表示 |
| オーディオテキスト | ストリーミングオーディオ |
| オンラインビデオリンクテキスト | \<p>このトピックに関連付けられているビデオを{0}\<表示するには{1}、href=" {2}\<">ここ /a> をクリックします。\</p> |
| オンラインオーディオリンクテキスト | \<p>このトピックに関連付けられているオーディオを聴{0}\<くために、href="{1} {2}">ここ\</a>。\</p> |
| 機能: | **コンテンツがインストールされていないコントロール** |
| 次のコマンドを使用します。 | コンテンツのレンダリングに使用されるテキスト要素 (文字列) |
| **要素** | **Value** |
| コンテンツがインストールされていません | コンピュータにコンテンツが見つかりませんでした。 |
| コンテンツがインストールされていません。 | \<p>コンテンツをコンピュータにダウンロード\<するには、href=">{0} {1} [管理\<] タブをクリック>。\</p> |
| テキストがインストールされていません。 | \<p>コンピュータにコンテンツがインストールされていません。 ローカル ヘルプ コンテンツのインストールについては、管理者に確認してください。\</p> |
| 機能: | **トピックが見つかりませんコントロール** |
| 次のコマンドを使用します。 | topicnotfound.htm のレンダリングに使用されるテキスト要素 (文字列) |
| **要素** | **Value** |
| トピック見つかりませんでした | コンピュータで要求されたトピックが見つかりません。 |
| トピックは見つかりませんでしたビューオンライン テキスト | \<p>要求したトピックはコンピュータ上に見つかりませんでしたが、トピック\<{0}をオンライン{1}\<で表示>、>。\</p> |
| トピックの見つかりませんでしたダウンロードコンテンツテキスト | \<p>類似のトピックへのリンクについてはナビゲーション ウィンドウ\<を参照するか、href=">{0}{1}を\<クリックして、コンテンツをコンピュータにダウンロードするには 、[管理] タブ /a>をクリックします。\</p> |
| トピック見つかりませんでしたテキスト | \<p>要求したトピックがコンピュータ上に見つかりませんでした。\</p> |
| 機能: | **トピックの破損コントロール** |
| 次のコマンドを使用します。 | トピック壊れた.htm のレンダリングに使用されるテキスト要素 (文字列) |
| **要素** | **Value** |
| トピック腐敗したタイトル | 要求されたトピックを表示できません。 |
| トピック破損したビューオンラインテキスト | \<p>ヘルプ ビューアは、要求されたトピックを表示できません。 トピックの内容にエラーがあるか、または基になるシステム依存関係にエラーが発生している可能性があります。\</p> |
| 機能: | **ホーム ページ コントロール** |
| 次のコマンドを使用します。 | ヘルプ ビューアーの最上位ノード コンテンツの表示をサポートするテキスト。 |
| **要素** | **Value** |
| HomePageTitle | ヘルプ ビューアー ホーム |
| ホームページ紹介 | \<p>マイクロソフトのツール、製品、テクノロジ、およびサービスを使用するすべてのユーザーにとって不可欠な情報源である Microsoft ヘルプ ビューアーへようこそ。 ヘルプ ビューアーでは、ハウツーおよび参照情報、サンプル コード、技術記事、および多くへのアクセスを提供します。 必要なコンテンツを見つけるには、目次を参照するか、フルテキスト検索を使用するか、キーワード インデックスを使用してコンテンツ内を移動します。\</p> |
| テキストをインストールします。 | \<p \<>br />a{0}href=" " {1}>\<コンテンツの管理 />\<タブ\<を使用\<して、次の操作を行います>>。\</li \<>li>ローカル コンテンツの更新を確認します。\</li \<>li>コンピュータからコンテンツを削除します。\</li \<>/ul>\</p> |
| ホームページインストールブック | インストール済みブック |
| ホームページNoブックスインストール | コンピュータにコンテンツが見つかりませんでした。 |
| ホームページのヘルプ設定 | ヘルプ コンテンツの設定 |
| ホームページヘルプ設定テキスト | \<p>現在の設定はローカルヘルプです。 ヘルプ ビューアには、コンピュータにインストールされているコンテンツが表示されます。\<br />ヘルプ コンテンツのソースを変更するには、Visual Studio の\<メニュー バーで{0}、span style=""">ヘルプ、ヘルプの設定\</span>を選択します。\<br />\</p> |
| メガバイト | MB |

**ブランディング.js**

branding.js ファイルには、Visual Studio ヘルプ ビューアーのブランド化要素で使用される JavaScript が含まれています。  以下は、ブランディング要素とサポートする JavaScript 関数の一覧です。  このファイルにローカライズされるすべての文字列は、このファイルの先頭にある「ローカライズ可能な文字列」セクションで定義されています。  ICL ファイルは、ブランド.js ファイル内の loc 文字列用に作成されました。

||||
|-|-|-|
|**ブランディング機能**|**関数**|**説明**|
|Var。。。||変数の定義|
|ユーザー コード言語を取得する|設定ユーザー設定ラン|コード言語にインデックス # をマップする|
|クッキー値の設定と取得|クッキーを取得, セットクッキー||
|継承されたメンバー|メンバーラベルを変更します。|継承されたメンバーの展開/折りたたみ|
|自己ブランド=偽の場合|Onload|クエリ文字列を読み、印刷要求かどうかを確認します。  すべてのコード スニペットを設定して、ユーザーが優先するタブにフォーカスを設定します。 印刷要求の場合は、設定してプリンターフレンドリーを true にします。 ハイコントラストモードを確認します。|
|コード スニペット|タグセットを追加します。||
||デヴランからインデックスを取得します。||
||変更タブ||
||コードスニペットランを設定します。||
||現在のラングを設定します。||
||クリップボードにコピー||
|折りたたみエリア|コントロールセットを追加します。|折りたたみ可能なコントロールオブジェクトをすべてリストに書き込みます。|
||CA_Click|折りたたみ可能な領域の状態に基づいて、どの画像とテキストを表示するかを定義します。|
|ロゴのコントラストサポート|はブラックバックグラウンド()|背景が黒かどうかを判断するために呼び出されます。  ハイコントラストモードの場合のみ正確です。|
||はハイコントラスト()|ハイコントラストモードを検出するには、色付きスパンを使用する|
||オンハイコントラスト(ブラック)|ハイ コントラストが検出されたときに呼び出されます。|
|LST 機能|||
||を設定します。||
||アップデートLST(現在のラング)||
||コードスニペット(ラング)||
|マルチメディア機能|キャプション(開始、終了、テキスト、スタイル)||
||すべてのメディア コントロール(正規化された Id) を検索します。||
||をクリックします。||
||キャプションオンオフ(id)||
||トセカンズ(t)||
||すべてのコメントを取得します(ノード)||
||スタイルレクティファイ(スタイル名、スタイル値)||
||ショーCC(id)||
||字幕(id)||

**HTM ファイル**

ブランド化パッケージには、ヘルプ コンテンツ ユーザーに重要な情報を伝達するためのシナリオをサポートする一連の HTM ファイルが含まれています。 これらのHTMファイルは、製品ごとに変更することができます。  ISO Shell ベンダーは、デフォルトのブランド化パッケージを受け取り、これらのページの動作とコンテンツを変更して、必要に応じて使用できます。  これらのファイルは、ブランドタグが対応するコンテンツを branding.xml ファイルから取得するために、それぞれのブランド化パッケージを参照します。

||||
|-|-|-|
|**ファイル**|**用途**|**表示されたコンテンツ ソース**|
|ホームページ.htm|これは、現在インストールされているコンテンツ、およびユーザーに表示するコンテンツに関するその他のメッセージを表示するページです。  このファイルには、追加のメタデータ属性"Microsoft.Help.Id"コンテンツ="-1"があり、このコンテンツはローカルコンテンツTOCの一番上に配置されます。||
||<META_HOME_PAGE_TITLE_ADD />|ブランディング.xml、タグ\<ホームページタイトル>|
||<HOME_PAGE_INTRODUCTION_SECTION_ADD />|ブランディング.xml、タグ\<ホームページ紹介>|
||<HOME_PAGE_CONTENT_INSTALL_SECTION_ADD />|ブランディング.xml、タグ\<ホームページコンテンツインストールテキスト>|
||<HOME_PAGE_BOOKS_INSTALLED_SECTION_ADD />|見出しセクション Branding.xml タグ\<HomePageInstalledBooks>、アプリケーション\<から生成されたデータ、HomePageNoBooksInstalledは、本がインストールされていないときに>。|
||<HOME_PAGE_SETTINGS_SECTION_ADD />|見出しセクション Branding.xml タグ\<ホームページヘルプ設定>、セクション テキスト\<ホームページヘルプ設定テキスト>。|
|トピック破損.htm|ローカル セットにトピックが存在するが、何らかの理由で表示できない (コンテンツが破損している) 場合。||
||<META_TOPIC_CORRUPTED_TITLE_ADD />|ブランディング.xml、タグ\<トピック腐敗したタイトル>|
||<TOPIC_CORRUPTED_SECTION_ADD />|ブランディング.xml、タグ\<トピック腐敗ビューオンラインテキスト>|
|トピックが見つかりません。|トピックがローカル コンテンツ セットに見つからない場合、またはオンラインで利用できない場合||
||<META_TOPIC_NOT_FOUND_TITLE_ADD />|ブランディング.xml、タグ\<トピックNotFoundタイトル>|
||<META_TOPIC_NOT_FOUND_ID_ADD />|ブランディング.xml、タグ\<トピックNotFoundViewオンラインテキスト> \<+ トピックNotFoundDownloadコンテンツテキスト>|
||<TOPIC_NOT_FOUND_SECTION_ADD />|ブランディング.xml、タグ\<トピックNotFoundテキスト>|
|インストールされていません。|製品のローカル コンテンツがインストールされていない場合。||
||<META_CONTENT_NOT_INSTALLED_TITLE_ADD />|ブランディング.xml、タグ\<コンテンツはインストールされていません>|
||<META_CONTENT_NOT_INSTALLED_ID_ADD />|ブランディング.xml、タグ\<はインストールされていませんダウンロードコンテンツテキスト>|
||<CONTENT_NOT_INSTALLED_SECTION_ADD />|ブランディング.xml、タグ\<はインストールされていないテキスト>|

**CSS ファイル**

Visual Studio ヘルプ ビューアーのブランド化パッケージには、一貫性のある Visual Studio ヘルプ コンテンツ プレゼンテーションをサポートする 2 つの css ファイルが含まれています。

- Branding.css - セルフブランド=false の場合にレンダリングするための css 要素が含まれています。

- プリンター.css - セルフブランド=false をレンダリングするためのcss要素が含まれています

Branding.css ファイルには、Visual Studio トピック プレゼンテーションの定義が含まれています (注意点として\<、パッケージ サービスのBranding_ ロケール>.mshc に含まれる branding.css が変更される可能性があります)。

**グラフィックファイル**

Visual Studio コンテンツには、他のグラフィックスだけでなく、Visual Studio のロゴが表示されます。  Visual Studio ヘルプ ビューアー のブランド化パッケージのグラフィック ファイルの完全な一覧を次に示します。

||||
|-|-|-|
|**ファイル**|**用途**|**使用例**|
|クリア.gif|折りたたみ可能領域のレンダリングに使用||
|footer_slice.gif|フッタープレゼンテーション||
|info_icon.gif|情報を表示するときに使用します|免責事項|
|online_icon.gif|このアイコンは、オンラインリンクに関連付けされます||
|タブレフトBD.gif|コード スニペット コンテナーのレンダリングに使用します。||
|タブライトBD.gif|コード スニペット コンテナーのレンダリングに使用します。||
|vs_logo_bk.gif|Branding.xml タグ\<ロゴファイル名>で定義されている標準コントラスト ロゴ参照に使用されます。  Visual Studio 製品の場合、ロゴ名はvs_logo_bk.gif です。||
|vs_logo_wh.gif|Branding.xml タグ\<LogoFileNameHC>で定義されている通常の高いロゴ参照に使用されます。  Visual Studio 製品の場合、ロゴ名はvs_logo_wh.gif です。||
|ccOff.png|キャプショングラフィック||
|ccOn.png|キャプショングラフィック||
|イメージスプライト.png|折りたたみ可能領域のレンダリングに使用|展開されたグラフィックまたは折りたたみグラフィック|

## <a name="deploy-a-set-of-topics"></a>一連のトピックを展開する

これは、MSHA ファイルと、トピックを含む cab または MSH のセットで構成されるヘルプ ビューアー コンテンツ展開セットを作成するための簡単で簡単なチュートリアルです。 MSHA は、一連の cab ファイルまたは MSHC ファイルを記述する XML ファイルです。 ヘルプ ビューアは MSHA を読み取り、コンテンツの一覧を取得できます ( .CAB または .MSHC ファイル) をローカル インストールで使用できます。

これはヘルプ ビューア MSHA の非常に基本的な XML スキーマを記述する入門書にすぎません。  この簡単な概要とサンプルの下に実装例があります。

このプライマーの目的で、MSHA の名前は HelpContentSetup.msha です (ファイルの名前は拡張子を付けて何でもすることができます)。MSHA)。 HelpContentSetup.msha (以下の例) には、利用可能なタクシーまたは MSHCs のリストが含まれている必要があります。  MSHA 内で一貫性のあるファイルの種類を指定する必要があります (MSHA ファイルと CAB ファイルの種類の組み合わせをサポートしていません)。 各 CAB または MSHC に対\<して、div クラス="パッケージ">.\</div> (下記の例を参照)。

注: 以下の実装例では、ブランド化パッケージが含まれています。 これは、必要な Visual Studio コンテンツ レンダリング要素とコンテンツ動作を取得するために含める重要な要素です。

サンプルヘルプコンテンツセットアップ.mshaファイル: ("コンテンツセット名 1" や "コンテンツセット名 2" などをファイル名に置き換えます。

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

1. ローカル フォルダを作成する ("C:\SampleContent" のようなもの)

2. この例では、MSHC ファイルを使用してトピックを含みます。  MSHC は、ファイル拡張子が .zip から に変更された zip です。MSHC.

3. 以下の HelpContentSetup.msha をテキスト ファイルとして作成し (メモ帳を使用してファイルを作成しました)、上記のフォルダに保存します (手順 1 を参照)。

クラス「ブランディング」が存在し、ユニークです。 このプライマーには Branding mshc が含まれており、インストールされたコンテンツにブランドが設定され、MSHCs に含まれるコンテンツ動作にはブランド化パッケージに含まれる適切なサポート要素が含まれます。 これを使用しない場合、システムが、取り込まれた (インストールされた) コンテンツの一部ではないサポート項目を探すと、エラーが発生します。

Visual Studio ブランド パッケージを取得するには、c:\Program ファイル (x86)\Microsoft ヘルプ ビューアー\v2.3\ で Branding_en-US.mshc ファイルを作業フォルダーにコピーします。

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

上記の手順を使用して拡張すると、VSP は Visual Studio ヘルプ ビューアー用にコンテンツ セットをデプロイできるようになります。

### <a name="add-help-to-the-visual-studio-shell-integrated-and-isolated"></a>ヘルプを Visual Studio シェルに追加する (統合および分離)

**はじめに**

このチュートリアルでは、ヘルプ コンテンツを Visual Studio シェル アプリケーションに組み込んで配置する方法について説明します。

**必要条件**

1. [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]

2. [ビジュアル スタジオ 2013 分離シェル リディスト](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

**概要**

シェル[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]は、アプリケーションの[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]ベースとなる IDE のバージョンです。 このようなアプリケーションには、作成した拡張機能と共に分離シェルが含まれます。 拡張機能を構築するには、SDK に含まれている分離[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]シェル プロジェクト テンプレートを使用します。

分離シェル ベースのアプリケーションとそのヘルプを作成するための基本的な手順は次のとおりです。

1. ISO[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]シェル再頒布可能パッケージ (マイクロソフト のダウンロード) を入手します。

2. Visual Studio で、分離シェルに基づくヘルプ拡張機能を作成します。

3. 拡張と ISO シェルの再頒布可能ファイルを展開 MSI (アプリケーションのセットアップ) にラップします。 このチュートリアルには、セットアップ手順は含まれていません。

Visual Studio コンテンツ ストアを作成します。 統合シェル シナリオでは、次のように、Visual Studio12 を製品カタログ名に変更します。

- フォルダー C:\プログラムデータ\マイクロソフト\ヘルプライブラリ2\カタログ\VisualStudio15 を作成します。

- CatalogType.xml という名前のファイルを作成し、フォルダーに追加します。 ファイルには、次のコード行が含まれている必要があります。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <catalogType>UserManaged</catalogType>
    ```

レジストリ内のコンテンツ ストアを定義します。 統合シェルの場合は、VisualStudio15 を製品カタログ名に変更します。

- HKLM\ソフトウェア\Wow6432ノード\マイクロソフト\ヘルプ\v2.3\カタログ\VisualStudio15

   キー: 場所パス文字列値: C:\プログラムデータ\マイクロソフト\ヘルプライブラリ2\カタログ\VisualStudio15\

- HKLM\ソフトウェア\Wow6432ノード\マイクロソフト\ヘルプ\v2.3\カタログ\VisualStudio15\enUS

   キー: カタログ名文字列値[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]: ドキュメント

**プロジェクトの作成**

分離シェル拡張を作成するには、次の手順に従います。

1. Visual Studio の [**ファイル**] で、[**新しいプロジェクト**] を選択し、[**その他のプロジェクトの種類**] の [**機能拡張**] を選択し **、[Visual Studio シェル分離**] を選択します。 Visual Studio`ContosoHelpShell`分離シェル テンプレートに基づいて機能拡張プロジェクトを作成するには、プロジェクトに名前を付けます。

2. ソリューション エクスプローラーの ContosoHelpShellUI プロジェクトの [リソース ファイル] フォルダーで、アプリケーション コマンド.vsct を開きます。 この行がコメント アウトされていることを確認します("No_Help" を検索します)。`<!-- <define name="No_HelpMenuCommands"/> -->`

3. **[デバッグ**] をコンパイルして実行する F5 キーを選択します。 分離シェル IDE の実験用インスタンスで、[**ヘルプ**] メニューを選択します。 [**ヘルプの表示]、[ヘルプ****コンテンツの追加と削除**]、[**ヘルプ設定の設定]** の各コマンドが表示されていることを確認します。

4. ソリューション エクスプローラーの ContosHelpShell プロジェクトのシェル カスタマイズ フォルダーで、ContosoHelpShell.pkgdef を開きます。 Contoso ヘルプ カタログを定義するには、次の行を追加します。

    ```
     [$RootKey$\Help]
    "Product"="Contoso"
    "Catalog"="Contoso"
    "Version"="100"
    "BrandingPackage"="ContosoBrandingPackage.mshc"
    ```

5. ソリューション エクスプローラーの ContosHelpShell プロジェクトのシェル カスタマイズ フォルダーで、ContosoHelpShell.Application.pkgdef を開きます。 F1 ヘルプを有効にするには、次の行を追加します。

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

6. ソリューション エクスプローラーの ContosoHelpShell ソリューションのコンテキスト メニューで、[**プロパティ]** メニュー項目を選択します。 [**構成のプロパティ**] で、[**構成マネージャ ] を**選択します。 [**構成**] 列で、すべての "デバッグ" 値を "リリース" に変更します。

7. ソリューションをビルドします。 これにより、リリース フォルダに一連のファイルが作成され、次のセクションで使用されます。

これを展開された場合と同様にテストするには、次の手順を実行します。

1. Contoso を展開するコンピューターで、ダウンロードした (上から) ISO シェルをインストールします。

2. \\\Program Files (x86)\\にフォルダを作成し、名前を付けます`Contoso`。

3. コンテンツを ContosoHelpShell リリース フォルダーから\\\プログラム ファイル (x86)\Contoso\ フォルダーにコピーします。

4. [**スタート]** メニューの [ファイル名`Regedit`**を指定して実行**] をクリックし、 を入力してレジストリ エディタを起動します。 レジストリ エディタで、[**ファイル**] を選択し、[**インポート**] をクリックします。 プロジェクト フォルダーを参照します。 サブフォルダーで、[ContosoHelpShell.reg] を選択します。

5. コンテンツ ストアを作成します。

    ISO シェルの場合 - Contoso コンテンツ ストア C:\プログラムデータ\マイクロソフト\ヘルプライブラリ2\カタログ\ContosoDev12 を作成します。

    統合[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]シェルの場合は、フォルダー C:\プログラムデータ\マイクロソフト\ヘルプライブラリ2\カタログ\VisualStudio15 を作成します。

6. CatalogType.xml を作成し、次の内容を含むコンテンツ ストア (前の手順) に追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <catalogType>UserManaged</catalogType>
   ```

7. 次のレジストリ キーを追加します。

    HKLM\ソフトウェア\Wow6432ノード\マイクロソフト\ヘルプ\v2.3\カタログ\VisualStudio15Key: ロケーションパス文字列値:

    ISO シェルの場合:

    プログラムプログラムプログラムヘルプライブラリ2カタログ

    [!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]統合シェル:

    C:プログラムデータヘルプライブラリ2カタログ

    キー: カタログ名 文字列[!INCLUDE[vs_dev12](../../extensibility/includes/vs_dev12_md.md)]値: ドキュメント。 ISO シェルの場合、これはカタログの名前です。

8. コンテンツ (cabs または MSHC および MSHA) をローカル フォルダーにコピーします。

9. コンテンツ ストアをテストするための統合シェル コマンド ラインの例。 ISO シェルの場合は、カタログを変更し、製品に合わせて適切な値を起動します。

     "C:\プログラム ファイル (x86)\マイクロソフト ヘルプ ビューアー\v2.3\HlpViewer.exe" /カタログ名 VisualStudio15 /helpQuery メソッド="ページ&id=ContosoTopic0" /起動アプリ マイクロソフト,VisualStudio,12.0

10. Contoso アプリケーションを起動します (Contoso アプリ ルートから)。 ISO シェルで、[**ヘルプ**] メニュー項目を選択し、[**ヘルプの基本設定**] を **[ローカル ヘルプを使用**する] に変更します。

11. シェル内で、[**ヘルプ**] メニュー項目を選択し、[**ヘルプの表示**] をクリックします。 ローカル ヘルプ ビューアーが起動します。 [**コンテンツの管理]** タブを選択します。[**インストール ソース**] で、[**ディスク**] オプション ボタンを選択します。 **[...]** ボタンをクリックし、Contoso のコンテンツを含むローカル フォルダを参照します (上記の手順でローカル フォルダにコピー)。 ヘルプコンテンツセットアップ.msha を選択します。 これで、Contoso は書籍の選択に書籍として表示されます。 [**追加**] をクリックし、[**更新**] ボタン (右下) をクリックします。

12. Contoso IDE 内で F1 キーを選択して F1 機能をテストします。

## <a name="additional-resources"></a>その他のリソース

ランタイム API については[、Windows ヘルプ API](/previous-versions/windows/desktop/helpapi/helpapi-portal)を参照してください。

ヘルプ API を利用する方法の詳細については、[ヘルプ ビューアーのコード例](https://marketplace.visualstudio.com/items?itemName=RobChandlerHelpMVP.HelpViewer20CodeExamples)を参照してください。

[開発者コミュニティ](https://developercommunity.visualstudio.com/content/idea/post.html?space=8)で機能の提案を提出できます。
