---
title: JavaScript IntelliSense | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [JavaScript]
- <reference> JavaScript XML tag
- JavaScript Code Editor
- XML code comments, JavaScript IntelliSense
- reference JavaScript XML tag
- JavaScript, IntelliSense
- code comments, JavaScript IntelliSense
- JavaScript, reference groups
- JavaScript Editor
- reference directives [JavaScript]
- JavaScript, XML documentation comments
- reference groups [JavaScript]
- JavaScript, reference directives
- IntelliSense [JavaScript], about
- IntelliSense extensibility [JavaScript]
- XML documentation comments [JavaScript]
ms.assetid: af1a3171-c9d8-45a3-9c96-a763e3b163ef
caps.latest.revision: 67
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e367ff6d6abbf40cdf7efebed04aee6fc74a384c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300742"
---
# <a name="javascript-intellisense"></a>JavaScript IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IntelliSense ではコード入力中に情報が表示されるため、コードの記述が速くなり、エラーも減少します。 JavaScript エディターでクライアント スクリプトを操作するときは、現在のコンテキストに基づいて使用できるオブジェクト、関数、プロパティ、およびパラメーターが IntelliSense で一覧表示されます。 IntelliSense で表示されるポップアップ リストから入力するコードを選択し、コードを完成することができます。

 IntelliSense を使用して、次のタスクを簡単に実行できます。

- メンバー情報を検索する。

- 言語要素をコードに直接挿入する。

- コード エディターを離れることなくコンテキストを維持する。

- XML ドキュメントのコメントおよび JavaScript IntelliSense の機能拡張を持つカスタム IntelliSense をサポートする。

  このトピックは、次のセクションで構成されています。

- [IntelliSense のコンテキストの確認](#DeterminingIntelliSenseContext)

- [IntelliSense の情報の処理](#ProcessingIntelliSenseInformation)

- [JavaScript IntelliSense の機能](#Features)

- [JavaScript IntelliSense の機能拡張](#Extensibility)

- [JavaScript の検証](#Validation)

  [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] の IntelliSense の機能の詳細については、「[IntelliSense の使用方法](../ide/using-intellisense.md)」を参照してください。

## <a name="DeterminingIntelliSenseContext"></a> IntelliSense のコンテキストの確認
 JavaScript IntelliSense では、現在のスクリプト コンテキストに関連するすべてのスクリプトに基づいて、入力するコードを選択できます。 これには、現在のファイル内のスクリプト要素が含まれます。 また、スクリプト ファイル参照、アセンブリ スクリプト参照、サービス参照、ページに関連付けられた参照など、作業中のスクリプトから直接的または間接的に参照されるコードもすべて含まれます。

 現在のスクリプト コンテキストは、次の項目に基づいて作成されます。

- アクティブ ドキュメント内のすべてのスクリプト ブロックで定義された関数。 ファイル名拡張子が .aspx、.ascx、.master、.html、および .htm のファイルでは、インライン スクリプト ブロックがサポートされています。

- 別のスクリプト ファイルを指す `src` 属性を持つ `script` 要素。 参照先スクリプト ファイルのファイル名拡張子は .js であることが必要です。

- `reference` ディレクティブを使用して別の JavaScript ファイルを参照している JavaScript ファイル。

- グローバル オブジェクト、IntelliSense の機能拡張、または遅延読み込みスクリプト ファイルの参照グループ。

- XML Web サービスへの参照。

- Web アプリケーションが AJAX 対応の ASP.NET アプリケーションの場合は、<xref:System.Web.UI.ScriptManager> コントロールおよび <xref:System.Web.UI.ScriptManagerProxy> コントロール。

- AJAX 対応の ASP.NET Web アプリケーションの作業をしている場合は、[!INCLUDE[atlaslib_current_ext](../includes/atlaslib-current-ext-md.md)]。

    > [!NOTE]
    > IntelliSense は、HTML 要素のイベント ハンドラー属性内のスクリプトや `href` 属性に定義されたスクリプトではサポートされません。

## <a name="ProcessingIntelliSenseInformation"></a> IntelliSense の情報の処理
 JavaScript IntelliSense を使用できるようにするため、言語サービスでは次の操作が実行されます。

- アクティブ ドキュメント内の参照と、参照されるファイル内のスクリプト参照を再帰的にチェックする処理に基づいて JavaScript 依存ファイルのリストを作成します。

- リストを走査し、各ファイルから型情報やその他の関連データを収集します。

- データを集計して JavaScript 言語サービスに渡します。これにより、型情報やデータが IntelliSense で使用できるようになります。

- ファイルで IntelliSense のリストに影響する可能性がある変更を監視し、必要に応じてリストを更新します。 リモート ストアのスクリプト (HTTP を使用して参照するものなど) は監視されません。

## <a name="Features"></a> JavaScript IntelliSense の機能
 JavaScript IntelliSense は、次のオブジェクトをサポートします。

- [ドキュメント オブジェクト モデル (DOM: Document Object Model) 要素](#HTMLDom)

- [組み込みオブジェクト](#IntrinsicObjects)

- [ユーザー定義の変数、関数、およびオブジェクト](#UserDefined)

- [スクリプト参照](#Script)、[参照ディレクティブ](#ReferenceDirectives)、[参照グループ](#ReferenceGroups)などの参照を使用して外部ファイルで定義されるオブジェクト。

- Visual Studio がダウンロードするリモート ファイルによって定義されたオブジェクト。

- パラメーターやフィールドなど [XML ドキュメントのコメント](#XMLDocComments)で指定されるオブジェクト。

- 標準の JavaScript コメント タグ (//) を使用して記述されるオブジェクト。 詳細については、「[JavaScript IntelliSense の拡張](../ide/extending-javascript-intellisense.md)」を参照してください。

- [JavaScript IntelliSense 機能拡張](#Extensibility)のメカニズムを使ってサポートされるオブジェクト。 詳細については、「[JavaScript IntelliSense の拡張](../ide/extending-javascript-intellisense.md)」を参照してください。

- [ASP.NET AJAX オブジェクト](#ASPNet)

  IntelliSense は、オブジェクトの型を特定できない場合、アクティブ ドキュメントの識別子を使用して入力候補のオプションを提供します。 詳細については、「[Statement Completion for Identifiers (識別子の入力候補)](../ide/statement-completion-for-identifiers.md)」をご覧ください。

### <a name="HTMLDom"></a> HTML DOM 要素
 JavaScript IntelliSense では、`body`、`form`、`div` などのダイナミック HTML (DHTML: Dynamic HTML) DOM 要素のプログラミングで参照できる一覧が表示されます。 現在のドキュメントとマスター ページに含まれる要素だけが IntelliSense によって表示されます。 `window` オブジェクトと `document` オブジェクト、およびそれらのメンバーも JavaScript IntelliSense でサポートされます。

### <a name="IntrinsicObjects"></a> 組み込みオブジェクト
 JavaScript IntelliSense では、組み込みオブジェクトのプログラミングで参照できる一覧が表示されます。これには、`Array`、`String`、`Math`、`Date`、`Number` などがあります。 組み込みオブジェクトの詳細については、「[標準ビルトインオブジェクト](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)」を参照してください。

### <a name="UserDefined"></a> ユーザー定義の変数、関数、およびオブジェクト
 JavaScript ファイルを変更すると、開かれているドキュメントと参照されているドキュメントが [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] でスキャンされ、利用できるすべてのコード リソースが確認されます。 これには、ご自分で作成した変数、関数、およびオブジェクトが含まれます。 その後、これらのリソースが JavaScript IntelliSense で利用できるようになります。

 ユーザー定義の変数、関数、およびオブジェクトの詳細については、MSDN Web サイト上の[独自のオブジェクトの作成](https://go.microsoft.com/fwlink/?LinkId=108671)に関するページを参照してください。

### <a name="External"></a> 外部ファイル参照
 コードの IntelliSense サポートを実現するために、さまざまな種類の外部ファイル参照を含めることができます。 外部ファイル参照は、スクリプト参照または参照ディレクティブの場合があり、参照グループを使って指定することもできます。

#### <a name="Script"></a> スクリプト参照
 ページ内にすべてのクライアント スクリプトを記述する代わりに、スクリプト コードを格納した外部ファイルを参照できます。 これによって、ページ間でのコードの再利用が容易になり、ブラウザーでクライアント スクリプトをキャッシュできるようになります。

 ASP.NET AJAX 対応の Web ページで作業していない場合は、`src` 要素の開始タグにある `script` 属性を使用して外部スクリプト ファイルを参照できます。 `src` 属性には、ソース コードまたはデータを格納した外部ファイルへの URL が指定されます。

 <`script`> タグの `src` 属性を使用してスクリプト ファイルを参照するマークアップの例を次に示します。

```html
<script type="text/javascript" src="~/Scripts/JavaScript.js">

</script>
```

 ASP.NET AJAX 対応の Web ページで作業している場合は、<xref:System.Web.UI.ScriptReference> コントロールの <xref:System.Web.UI.ScriptManager> オブジェクトを使用してスクリプト ファイルを参照できます。

 <xref:System.Web.UI.ScriptReference> コントロールの <xref:System.Web.UI.ScriptManager> オブジェクトを使用してスクリプト ファイルを参照するマークアップの例を次に示します。

```html
<asp:ScriptManager ID="ScriptManager1" runat="server">
  <Scripts>
    <asp:ScriptReference Path="~/Scripts/JavaScript.js" />
  </Scripts>
</asp:ScriptManager>
```

 IntelliSense では、ASP.NET AJAX Web アプリケーションのアセンブリ内にリソースとして埋め込まれるスクリプト ファイルもサポートされます。 埋め込みスクリプト リソースの詳細については、「[Walkthrough: Embedding a JavaScript File as a Resource in an Assembly (チュートリアル: アセンブリ内のリソースとしての JavaScript ファイルの埋め込み)](https://msdn.microsoft.com/library/d8cb78cd-95a9-4dc6-92df-391866817e89)」を参照してください。

#### <a name="ReferenceDirectives"></a> 参照ディレクティブ
 `reference` ディレクティブを使用すると、現在編集中のスクリプトとその他のスクリプトとの間の関係を [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] で確立できます。 `reference` ディレクティブにより、現在のスクリプト ファイル内のスクリプトのコンテキストにスクリプト ファイルを含めることができます。 これにより、コードの入力時に、外部で定義されている関数、型、およびフィールドを IntelliSense で参照できます。

 `reference` ディレクティブは、XML コメントの形式で作成します。 このディレクティブは、ファイル内で他のいずれのスクリプトよりも前に定義する必要があります。 `reference` ディレクティブには、ディスク ベースのスクリプト参照、アセンブリ ベースのスクリプト参照、サービス ベースのスクリプト参照、またはページ ベースのスクリプト参照を含めることができます。

 ディスク ベースの参照ディレクティブを使用する例を次に示します。 最初の例では、言語サービスは、プロジェクト ファイル (たとえば、.jsproj) が含まれるのと同じフォルダー内のファイルを検索します。

 `/// <reference path="ScriptFile1.js" />`

 `/// <reference path="Scripts/ScriptFile2.js" />`

 `/// <reference path="../ScriptFile3.js" />`

 `/// <reference path="~/Scripts/ScriptFile4.js" />`

 アセンブリ ベースのスクリプトへの参照を作成する方法の例を次に示します。

 `/// <reference name "Ajax.js" assembly="System.Web.Extensions, ..." />`

 サービス ベースのスクリプトへの参照方法の例を次に示します。

 `/// <reference path="MyService.asmx" />`

 `/// <reference path="Services/MyService.asmx" />`

 `/// <reference path="../MyService.asmx" />`

 `/// <reference path="~/Services/MyService.asmx" />`

> [!NOTE]
> JavaScript IntelliSense は、Web アプリケーション プロジェクト (WAP: Web Application Project) の Web サービス ファイル (.asmx) 内に格納されたスクリプトではサポートされません。

 ページ ベースのスクリプトへの参照方法の例を次に示します。

 `/// <reference path="Default.aspx" />`

 `/// <reference path="Admin/Default.aspx" />`

 `/// <reference path="../Default.aspx" />`

 `/// <reference path="~/Admin/Default.aspx" />`

 `reference` ディレクティブには、次の規則が適用されます。

- `reference` XML コメントは、他のいずれのスクリプトよりも前に定義する必要があります。

- XML コメントの構文を 3 つのスラッシュと共に使用する必要があります。 標準のコメントの構文 (2 つのスラッシュ) を使用して作成された参照は無視されます。

- ディレクティブごとに、1 つのファイルまたは 1 つのリソースだけを指定できます。

- ページ ベースのスクリプトへの複数の参照は指定できません。

- ページ参照を指定する場合、これ以外の種類の参照ディレクティブは指定できません。

- ファイル名には相対パスを使用します。 ティルダ演算子 (`~`) を使用すると、アプリケーション ルートに対する相対パスを指定できます。

- 絶対パスは無視されます。

- 参照されるページにある参照ディレクティブは処理されません。つまり、参照ディレクティブは、ページに対して再帰的には解決されません。 ページによって直接参照されるスクリプトだけが含まれます。

#### <a name="ReferenceGroups"></a>参照グループ
 定義済みの参照グループを使用して、特定の IntelliSense (.js) ファイルがさまざまな JavaScript プロジェクトのスコープ内にあることを指定できます。 使用できる参照グループの種類は次のとおりです。

- 暗黙 (Windows)、JavaScript を使用する [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーション用。 このグループに含まれるファイルは、指定された種類のプロジェクトのコード エディターで開かれる、すべての .js ファイルのスコープ内にあります。

- 暗黙 (Web)、HTML5 プロジェクト用。 このグループに含まれるファイルは、これらのプロジェクト タイプのコード エディターで開かれる、すべての .js ファイルのスコープ内にあります。

- 専用のワーカーの参照グループ、HTML5 Web ワーカー用。 このグループで指定されたファイルは、専用のワーカーの参照グループへの明示的な参照がある .js ファイルのスコープ内にあります。

- ジェネリック、他の JavaScript プロジェクト タイプ用。

  ほとんどのシナリオでは、参照グループを変更する必要はありません。 しかし変更する場合は、参照グループに含まれるファイルを指定するために JavaScript コード エディターの構成オプションを使用できます。 この機能を使用する方法の詳細については、「[[オプション]、[テキスト エディター]、[JavaScript]、[IntelliSense]](../ide/reference/options-text-editor-javascript-intellisense.md)」を参照してください。

> [!TIP]
> 通常、IntelliSense 参照は、グローバル オブジェクトに IntelliSense サポートを提供するため、および IntelliSense [機能拡張](#Extensibility)のために使用されます。 また、スクリプト ローダーを使用して実行時に読み込む必要があるスクリプトでこの機能を使用できます。

### <a name="remote-file-references"></a>リモート ファイル参照
 リモート ファイルまたはライブラリで IntelliSense サポートを提供するために、JavaScript ファイルで参照されるリモート JavaScript ファイルをダウンロードするよう Visual Studio に指示できます。 この機能を使用する場合、JavaScript ファイルに参照として含まれるファイルがダウンロードされます。

> [!NOTE]
> Web プロジェクトを除き、この機能はプロジェクトのコンテキスト外で開いた JavaScript ファイルでのみ実行されます。 Web プロジェクトでは、プロジェクトで参照されるリモート ファイルは既定でダウンロードされます。

 この機能を使用する方法の詳細については、「[[オプション]、[テキスト エディター]、[JavaScript]、[IntelliSense]](../ide/reference/options-text-editor-javascript-intellisense.md)」を参照してください。

> [!WARNING]
> この機能を有効にするとコード エディターのパフォーマンスが低下することが観察された場合、機能を無効にすることをお勧めします。

### <a name="XMLDocComments"></a> XML ドキュメント コメント
 XML ドキュメントのコメントは、スクリプトに追加されるコード要素の説明テキストです。 これらの説明テキストは、コメントされたスクリプトを参照したときに IntelliSense で表示されます。 たとえば、関数のパラメーターと戻り値に関する情報を含められます。 XML ドキュメントのコメントは、参照されるファイル、アセンブリ、およびサービスでのみ使用できます。 詳細については、[XML ドキュメントのコメント](../ide/xml-documentation-comments-javascript.md)と [XML ドキュメントのコメントの作成](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)に関するページをご覧ください。

 IntelliSense は、次のシナリオで XML ドキュメントのコメントを表示できます。

- 別の .js ファイルを参照する .js ファイル。

- .aspx ファイルを参照する .js ファイル。

- .js ファイルを参照する .aspx ファイル。

  いずれかの .aspx ファイルで別の .aspx ファイルを参照している場合、IntelliSense は使用できません。

### <a name="ASPNet"></a> ASP.NET AJAX オブジェクト
 ASP.NET AJAX も JavaScript IntelliSense をサポートしています。 ASP.NET AJAX には、ECMAScript (JavaScript) で使用できる標準の型を拡張するクライアント フレームワークが含まれています。 JavaScript IntelliSense を有効にして ASP.NET AJAX オブジェクトに関する詳細を利用できるようにするために、XML ドキュメントのコメントが [!INCLUDE[atlaslib_current_ext](../includes/atlaslib-current-ext-md.md)] 全体に追加されました。 これらの XML ドキュメントのコメントは、ASP.NET AJAX ライブラリに格納された型およびメンバーを使用したときに表示されます。

> [!NOTE]
> プライベート メンバーは JavaScript IntelliSense では表示されません。 プライベート メンバーは、ASP.NET AJAX ではアンダースコア (_) で始まるメンバーとして表されます。

## <a name="Extensibility"></a> JavaScript IntelliSense の機能拡張
 JavaScript Language Service はオブジェクトや機能を提供して、サードパーティのライブラリを使用する開発者が IntelliSense の操作性を変更できるようにします。 これらの機能は、既定の言語サービスではすべての情報を顧客に提供できない場合に特に役立ちます。 詳細については、「[JavaScript IntelliSense の拡張](../ide/extending-javascript-intellisense.md)」を参照してください。

## <a name="Validation"></a> JavaScript の検証
 JavaScript のスクリプティングの検証は、背景で常に行われています。 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] が JavaScript コードで構文エラーを検出すると、フィードバックが次の方法で提供されます。

- エディター内の下線付き要素。 赤い波型の下線はエラーを示します。 マウス ポインターをエラーの上に置くと、ツールヒントにエラーの説明が表示されます。

- **[エラー一覧]** ウィンドウ。 **[エラー一覧]** ウィンドウに、エラーの説明、エラーが発生したファイル、行番号と列番号、およびプロジェクトが表示されます。 **[エラー一覧]** ウィンドウを表示するには、 **[表示]** メニューの **[エラー一覧]** をクリックします。

- 読み込まれなかった参照が [出力] ウィンドウに表示されます。

## <a name="see-also"></a>関連項目
- [IntelliSense の使用](../ide/using-intellisense.md)
- [XML ドキュメントのコメントを作成する](../ide/create-xml-documentation-comments-for-javascript-intellisense.md)
- [JavaScript IntelliSense の拡張](../ide/extending-javascript-intellisense.md)
- [識別子の入力候補](../ide/statement-completion-for-identifiers.md)
- [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)
- [DHTML オブジェクト モデルについて](https://go.microsoft.com/fwlink/?LinkID=92344)
- [リスト メンバー](https://msdn.microsoft.com/1b9cc469-9cd4-4d42-9999-1f9479635ff8)
- [SRC 属性 &#124; src プロパティ](https://go.microsoft.com/fwlink/?LinkId=92345)
