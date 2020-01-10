---
title: '方法: テキスト テンプレートを使用する'
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a7ecabc00f37cb199f203bcd71a1b72bdbfbe1a4
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594657"
---
# <a name="how-to--with-text-templates"></a>方法: テキスト テンプレートを使用する
Visual Studio のテキストテンプレートは、任意の種類のテキストを生成する便利な方法を提供します。 テキストテンプレートを使用して、アプリケーションの一部として実行時にテキストを生成したり、デザイン時にプロジェクトコードを生成したりすることができます。 このトピックでは、最もよく寄せられる "操作方法...?" 点.

 このトピックでは、ビュレットが付いている複数の回答は代替案です。

 テキスト テンプレートの一般的な概要については、[コードの生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)をお読みください。

## <a name="how-to-"></a>どうやって ... をする

### <a name="generate-part-of-my-application-code"></a>アプリケーション コードの一部を生成
 ファイルまたはデータベースにコンフィグレーションまたは*モデル*があります。 コードの 1 つ以上の部分が、そのモデルに依存しています。

- テキストテンプレートからいくつかのコードファイルを生成します。 詳細については、「 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」と、[テンプレートの作成を開始するための最適な方法](#starting)に関する説明を参照してください。

### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>テンプレートにデータを渡して、実行時にファイルを生成する
 アプリケーションでは、実行時に、標準のテキストとデータを組み合わせたレポートなどのテキストファイルが生成されます。 何百もの `write` ステートメントを書くことを回避したいです。

- ランタイムテキストテンプレートをプロジェクトに追加します。 このテンプレートは、あなたのコードでインスタンス化しテキストを生成することができるクラスを作成します。 データは、コンストラクターのパラメーターから渡すことができます。 詳細については、次を参照してください。 [T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)

- 実行時にのみ使用できるテンプレートから生成する場合は、標準のテキストテンプレートを使用できます。 Visual Studio 拡張機能を作成する場合は、テキストテンプレートサービスを呼び出すことができます。 詳細については、「[VS 拡張機能でテキスト変換を呼び出す](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください 他のコンテキストでは、テキストテンプレートエンジンを使用できます。 詳細については、「 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>」を参照してください。

     \<#@parameter# > ディレクティブを使用して、これらのテンプレートにパラメーターを渡します。 詳細については、「 [T4 Parameter ディレクティブ](../modeling/t4-parameter-directive.md)」を参照してください。

### <a name="read-another-project-file-from-a-template"></a>別のプロジェクトファイルをテンプレートから読み取る
 テンプレートと同じ Visual Studio プロジェクトからのファイルを読み取るには次のようにします。

- `hostSpecific="true"` ディレクティブに `<#@template#>` を挿入します。

     コードでは、`this.Host.ResolvePath(filename)` を使用してファイルの完全なパスを取得します。

### <a name="invoke-methods-from-a-template"></a>テンプレートからメソッドを呼び出す

メソッドが既に存在している場合 (たとえば、.NET クラス)、次のようになります。

- \<#@assembly# > ディレクティブを使用してアセンブリを読み込み、\<#@import# > を使用して名前空間のコンテキストを設定します。 詳細については、次を参照してください。 [T4 インポート ディレクティブ](../modeling/t4-import-directive.md)

   頻繁に同じアセンブリのセットを使用し、ディレクティブをインポートする場合には、ディレクティブ プロセッサの作成を検討してください。 各テンプレートでは、アセンブリとモデル ファイルを読み込み、名前空間のコンテキストを設定できるディレクティブ プロセッサを呼び出すことができます。 詳細については、次を参照してください。[カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)

自分で作成したメソッドの場合:

- ランタイムテキストテンプレートを作成する場合は、ランタイムテキストテンプレートと同じ名前を持つ部分クラス定義を記述します。 このクラスに、追加するメソッドを追加します。

- メソッド、プロパティ、およびプライベートクラスを宣言できるクラス機能コントロールブロック `<#+ ... #>` を記述します。 テキストテンプレートがコンパイルされると、クラスに変換されます。 標準コントロールブロック `<#...#>` とテキストは1つのメソッドに変換され、クラス機能ブロックは個別のメンバーとして挿入されます。 詳細については、「[テキストテンプレートコントロールブロック](../modeling/text-template-control-blocks.md)」を参照してください。

   クラスの機能として定義されたメソッドは、埋め込みのテキスト ブロックとして含めることもできます。

   クラスの機能を別のファイルに配置することを検討してください。1つまたは複数のテンプレートファイルに `<#@include#>` できます。

- メソッドを別のアセンブリ (クラスライブラリ) に記述し、テンプレートから呼び出します。 `<#@assembly#>` ディレクティブを使用してアセンブリを読み込み、`<#@import#>` して名前空間のコンテキストを設定します。 デバッグ中にアセンブリを再構築するには、Visual Studio を停止して再起動する必要があることに注意してください。 詳細については、次を参照してください。 [T4 テキスト テンプレート ディレクティブ](../modeling/t4-text-template-directives.md)します。

### <a name="generate-many-files-from-one-model-schema"></a>1 つのモデル スキーマからの多数のファイル生成
 同じXMLまたはデータベース スキーマを持つモデルからファイルをしばしば生成する場合:

- ディレクティブ プロセッサを記述することを検討します。 これにより、アセンブリの複数のステートメントを置換して、単一のカスタム ディレクティブを持つ各テンプレート内でステートメントをインポートすることができます。 ディレクティブ プロセッサはモデル ファイルを読み込み、解析できます。 詳細については、次を参照してください。[カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)

### <a name="generate-files-from-a-complex-model"></a>複雑なモデルからファイルを生成する

- モデルを表すために、ドメイン固有言語 (DSL) を作成することを検討してください。 これによって、モデル内の要素の名前を反映した型とプロパティを使用するため、テンプレートの記述が簡単になります。 ファイルを解析したり、XML ノードを巡回したりする必要はありません。 例:

     `foreach (Book book in this.Library) { ... }`

     詳細については、「[ドメイン固有言語を使用したはじめに](../modeling/getting-started-with-domain-specific-languages.md)」および「[ドメイン固有言語からのコードの生成](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

### <a name="get-data-from-visual-studio"></a>Visual Studio からのデータの取得
 Visual Studio で提供されるサービスを使用するには、`hostSpecific` 属性を設定し、`EnvDTE` アセンブリをロードします。 例:

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#
  IServiceProvider serviceProvider = (IServiceProvider)this.Host;
  EnvDTE.DTE dte = (EnvDTE.DTE) serviceProvider.GetService(typeof(EnvDTE.DTE));
#>

Number of projects in this VS solution:  <#= dte.Solution.Projects.Count #>
```

### <a name="execute-text-templates-in-the-build-process"></a>ビルド プロセスでのテキスト テンプレートの実行

- 詳細については、「[ビルド プロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)」を参照してください。

## <a name="more-general-questions"></a>その他の一般的な質問

### <a name="starting"></a>テキストテンプレートの作成を開始する最適な方法は何ですか。

1. 生成されたファイルの特定の例を記述します。

2. `<#@template #>` ディレクティブ、および入力ファイルまたはモデルの読み込みに必要なディレクティブとコードを挿入して、テキストテンプレートに変換します。

3. 段階的に、ファイルの一部を式とコード ブロックに置き換えます。

### <a name="what-is-a-model"></a>「モデル」とは何ですか?

- テンプレートによって読み取られる入力です。 ファイルまたはデータベースに存在する可能性があります。 XML、Visio 図面、ドメイン固有言語 (DSL)、UML モデルのいずれか、またはプレーン テキストである可能性があります。 これは、いくつかのファイルにまたがることがあります。 通常は、複数のテンプレートが、1 つのモデルを読み取ります。

     「モデル」という用語の意味は、プログラム コードやその他のファイルの生成というよりも、ビジネスの側面をより直接的に表現しています。 たとえば、生成されたソフトウェアが監督する通信ネットワークの計画を表しているかもしれません。

### <a name="what-is-the-benefit-of-using-text-templates"></a>テキスト テンプレートを使用する利点は何ですか?
 通常は、1つのモデルから複数のコードまたは他のファイルを生成します。 モデルは、生成されるコードよりも直接的に要件を表しています。 実装の詳細を省略し、コードではなく、要件の観点から記述されます。 （あなたにもよくある）要件変更のとき、モデルの更新は、プログラム コードのさまざまな部分の更新よりも、より簡単かつより確実にできます。

 すなわち、コード生成は、アジャイル開発手法の観点から貴重なツールです。

### <a name="what-best-practices-are-there-for-text-templates"></a>テキスト テンプレートには、どのような「ベスト プラクティス」がありますか?

- 詳細については、「 [T4 テキストテンプレートの作成に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)」を参照してください。

### <a name="what-is-t4"></a>"T4"とは何ですか?

- ここで説明されている Visual Studio のテキスト テンプレート機能の別の名前です。 公開されていない以前のバージョンでは、「Text Template Transformation」の省略形でした。
