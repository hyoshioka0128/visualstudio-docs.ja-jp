---
title: '方法: テキスト テンプレートを使用する'
description: テキストテンプレートを使用してテキストを生成する際によく寄せられる質問への回答について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c5b5e1f4e7488253112eb33905fe534be3591782
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934898"
---
# <a name="how-to--with-text-templates"></a>方法: テキスト テンプレートを使用する
Visual Studio のテキストテンプレートは、任意の種類のテキストを生成する便利な方法を提供します。 テキストテンプレートを使用して、アプリケーションの一部として実行時にテキストを生成したり、デザイン時にプロジェクトコードを生成したりすることができます。 このトピックでは、最もよく寄せられる "操作方法...?" 点.

 このトピックでは、箇条書きの前にある複数の解答が代替候補です。

 テキストテンプレートの概要については、「 [コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)」を参照してください。

## <a name="how-to-"></a>操作方法。。。

### <a name="generate-part-of-my-application-code"></a>アプリケーションコードの一部を生成する
 ファイルまたはデータベースに構成または *モデル* がある。 コードの1つ以上の部分が、そのモデルに依存しています。

- テキストテンプレートからいくつかのコードファイルを生成します。 詳細については、「 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md) 」と、 [テンプレートの作成を開始するための最適な方法](#starting)に関する説明を参照してください。

### <a name="generate-files-at-run-time-passing-data-into-the-template"></a>実行時にファイルを生成し、テンプレートにデータを渡す
 アプリケーションでは、実行時に、標準のテキストとデータを組み合わせたレポートなどのテキストファイルが生成されます。 何百ものステートメントの記述を避ける必要があり `write` ます。

- ランタイムテキストテンプレートをプロジェクトに追加します。 このテンプレートは、コード内にクラスを作成します。このクラスをインスタンス化して、テキストを生成するために使用できます。 コンストラクターパラメーターでデータを渡すことができます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

- 実行時にのみ使用できるテンプレートから生成する場合は、標準のテキストテンプレートを使用できます。 Visual Studio 拡張機能を作成する場合は、テキストテンプレートサービスを呼び出すことができます。 詳細については、「 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。 他のコンテキストでは、テキストテンプレートエンジンを使用できます。 詳細については、「<xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName>」を参照してください。

     これらの \<#@parameter#> テンプレートにパラメーターを渡すには、ディレクティブを使用します。 詳細については、「 [T4 Parameter ディレクティブ](../modeling/t4-parameter-directive.md)」を参照してください。

### <a name="read-another-project-file-from-a-template"></a>別のプロジェクトファイルをテンプレートから読み取る
 同じ Visual Studio プロジェクトからテンプレートとしてファイルを読み取るには、次のようにします。

- `hostSpecific="true"` ディレクティブに `<#@template#>` を挿入します。

     コードで、を使用して `this.Host.ResolvePath(filename)` ファイルの完全なパスを取得します。

### <a name="invoke-methods-from-a-template"></a>テンプレートからメソッドを呼び出す

メソッドが既に存在している場合 (たとえば、.NET クラス)、次のようになります。

- ディレクティブを使用して \<#@assembly#> アセンブリを読み込み、を使用して \<#@import#> 名前空間コンテキストを設定します。 詳細については、「 [T4 Import ディレクティブ](../modeling/t4-import-directive.md)」を参照してください。

   同じアセンブリとインポートディレクティブのセットを頻繁に使用する場合は、ディレクティブプロセッサの記述を検討してください。 各テンプレートでは、ディレクティブプロセッサを呼び出すことができます。このプロセッサは、アセンブリとモデルファイルを読み込み、名前空間コンテキストを設定できます。 詳細については、「 [カスタム T4 テキストテンプレートディレクティブプロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)」を参照してください。

メソッドを自分で作成する場合は、次の手順を実行します。

- ランタイムテキストテンプレートを作成する場合は、ランタイムテキストテンプレートと同じ名前を持つ部分クラス定義を記述します。 このクラスに追加のメソッドを追加します。

- `<#+ ... #>`メソッド、プロパティ、およびプライベートクラスを宣言できるクラス機能コントロールブロックを記述します。 テキストテンプレートがコンパイルされると、クラスに変換されます。 標準のコントロールブロック `<#...#>` とテキストは1つのメソッドに変換され、クラス機能ブロックは個別のメンバーとして挿入されます。 詳細については、「 [テキストテンプレートコントロールブロック](../modeling/text-template-control-blocks.md)」を参照してください。

   クラス機能として定義されたメソッドには、埋め込みテキストブロックを含めることもできます。

   クラスの機能を別のファイルに配置することを検討してください。このファイルは、 `<#@include#>` 1 つまたは複数のテンプレートファイルに含めることができます。

- メソッドを別のアセンブリ (クラスライブラリ) に記述し、テンプレートから呼び出します。 ディレクティブを使用して、 `<#@assembly#>` アセンブリを読み込み、 `<#@import#>` 名前空間のコンテキストを設定します。 デバッグ中にアセンブリを再構築するには、Visual Studio を停止して再起動する必要があることに注意してください。 詳細については、「 [T4 テキストテンプレートのディレクティブ](../modeling/t4-text-template-directives.md)」を参照してください。

### <a name="generate-many-files-from-one-model-schema"></a>1つのモデルスキーマから多数のファイルを生成する
 同じ XML スキーマまたはデータベーススキーマを持つモデルからファイルを生成することが多い場合は、次のようにします。

- ディレクティブプロセッサを記述することを検討してください。 これにより、各テンプレートの複数の assembly ステートメントと import ステートメントを1つのカスタムディレクティブで置き換えることができます。 ディレクティブプロセッサは、モデルファイルを読み込んで解析することもできます。 詳細については、「 [カスタム T4 テキストテンプレートディレクティブプロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md)」を参照してください。

### <a name="generate-files-from-a-complex-model"></a>複雑なモデルからのファイルの生成

- モデルを表すために、ドメイン固有言語 (DSL) を作成することを検討してください。 これにより、モデル内の要素の名前を反映する型とプロパティを使用するため、テンプレートの記述が非常に簡単になります。 ファイルを解析したり、XML ノードを移動したりする必要はありません。 次に例を示します。

     `foreach (Book book in this.Library) { ... }`

     詳細については、「 [Domain-Specific 言語を使用したはじめに](../modeling/getting-started-with-domain-specific-languages.md) 」および「 [Domain-Specific 言語からのコードの生成](../modeling/generating-code-from-a-domain-specific-language.md)」を参照してください。

### <a name="get-data-from-visual-studio"></a>Visual Studio からデータを取得する
 Visual Studio で提供されるサービスを使用するには、属性を設定 `hostSpecific` し、アセンブリを読み込み `EnvDTE` ます。 次に例を示します。

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

### <a name="execute-text-templates-in-the-build-process"></a>ビルドプロセスでテキストテンプレートを実行する

- 詳細については、「 [ビルドプロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)」を参照してください。

## <a name="more-general-questions"></a>その他の一般的な質問

### <a name="what-is-the-best-way-to-start-writing-a-text-template"></a><a name="starting"></a> テキストテンプレートの作成を開始する最適な方法は何ですか。

1. 生成されたファイルの特定の例を記述します。

2. `<#@template #>`ディレクティブ、および入力ファイルまたはモデルを読み込むために必要なディレクティブとコードを挿入して、テキストテンプレートに変換します。

3. ファイルの一部を式およびコードブロックにプログレッシブ置換します。

### <a name="what-is-a-model"></a>"モデル" とは何ですか?

- テンプレートによって読み取られた入力。 ファイルまたはデータベースに存在する可能性があります。 XML、Visio 図面、ドメイン固有言語 (DSL)、または UML モデルの場合もあれば、プレーンテキストである場合もあります。 複数のファイルにわたって分散させることができます。 通常、複数のテンプレートは1つのモデルを読み取ります。

     "モデル" という用語の意味は、生成されたプログラムコードや他のファイルよりもビジネスの一部をより直接的に表すことです。 たとえば、生成されたソフトウェアが監視する通信ネットワークの計画を表す場合があります。

### <a name="what-is-the-benefit-of-using-text-templates"></a>テキストテンプレートを使用する利点は何ですか。
 通常は、1つのモデルから複数のコードまたは他のファイルを生成します。 モデルは、生成されたコードよりも要件を直接表します。 実装の詳細を省略し、コードではなく、要件の観点で記述します。 要件が変更された場合、通常どおりに、プログラムコードのさまざまな部分よりも簡単かつ確実にモデルを更新できます。

 このため、コード生成はアジャイル開発手法の観点から重要なツールです。

### <a name="what-best-practices-are-there-for-text-templates"></a>テキストテンプレートには、どのような "ベストプラクティス" がありますか。

- 詳細については、「 [T4 テキストテンプレートの作成に関するガイドライン](../modeling/guidelines-for-writing-t4-text-templates.md)」を参照してください。

### <a name="what-is-t4"></a>"T4" とは何ですか。

- ここで説明されている Visual Studio テキストテンプレート機能のもう1つの名前。 以前のバージョンは発行されていませんでしたが、"テキストテンプレート変換" の省略形でした。
