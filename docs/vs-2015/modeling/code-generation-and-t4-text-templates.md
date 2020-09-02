---
title: コード生成と T4 テキストテンプレート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
ms.assetid: 74a0a748-5b11-4999-8bea-49572967827d
caps.latest.revision: 84
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1f34422dfd47efdce9bf837f923da0e139a13398
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667918"
---
# <a name="code-generation-and-t4-text-templates"></a>コード生成と T4 テキスト テンプレート
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]では、 *T4 テキスト テンプレート* は、テキスト ファイルを生成できる、テキスト ブロックと制御ロジックが混在するファイルです。 制御ロジックは、 [!INCLUDE[csprcs](../includes/csprcs-md.md)] または [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]のプログラム コードのフラグメントとして記述します。 Visual Studio 2015 Update 2 以降では、T4 テンプレート ディレクティブで C# バージョン 6.0 の機能を使用できます。 Web ページ、リソース ファイル、任意の言語のプログラム ソース コードなど、あらゆる種類のテキスト ファイルを生成できます。

 T4 テキスト テンプレートには、次の 2 種類があります。

 **実行時 T4 テキスト テンプレート** ('前処理された' テンプレート) は、通常、出力の一部として文字列を生成するために、アプリケーションで実行されます。
たとえば、次のように HTML ページを定義するテンプレートを作成できます。

```
<html><body>
 The date and time now is: <#= DateTime.Now #>
</body></html>
```

 このテンプレートは、生成される出力に似ている点にご注目ください。 このように、テンプレートは結果の出力に似ているため、テンプレートを変更する場合に誤りを防ぐことができます。

 また、テンプレートにはプログラム コードのフラグメントも含まれます。 これらのフラグメントを使用して、テキストのセクションの繰り返し、条件付きセクションの作成、アプリケーションのデータの表示を行うことができます。

 出力を生成するには、テンプレートによって生成される関数をアプリケーションで呼び出します。 次に例を示します。

```csharp
string webResponseText = new MyTemplate().TransformText();

```

 アプリケーションは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされていないコンピューターでも実行できます。

 実行時テンプレートを作成するには、 **前処理されたテキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFilePreprocessor**に設定することもできます。

 詳細については、「 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。 テンプレートの構文の詳細については、「 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

 **デザイン時 T4 テキスト テンプレート** は、アプリケーションのソース コードや他のリソースの一部を定義するために、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で実行されます。
通常は、複数のテンプレートを使用して 1 つの入力ファイルまたはデータベースのデータを読み込み、一部の `.cs`ファイル、 `.vb`ファイル、または他のソース ファイルを生成します。 テンプレートごとに 1 つのファイルが生成されます。 テンプレートは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] または [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]内で実行されます。

 たとえば、入力データが構成データの XML ファイルであるとします。 開発中に XML ファイルを編集するたびに、テキスト テンプレートによって、アプリケーション コードの一部が再生成されます。 テンプレートの例を次に示します。

```
<#@ output extension=".txt" #>
<#@ assembly name="System.Xml" #>
<#
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.
#>
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>
{
  ... // More code here.
}

```

 XML ファイルの値に応じて、次のような `.cs` ファイルが生成されます。

```
namespace Fabrikam.FirstJob
{
  ... // More code here.
}
```

 別の例として、入力がビジネス アクティビティのワークフローの図であるとします。 ユーザーがビジネス ワークフローを変更した場合や、別のワークフローを使用する新しいユーザーとの作業を開始する場合は、新しいモデルに合わせてコードを簡単に再生成できます。

 デザイン時テンプレートを使用すると、要件が変わったときに構成をすばやく変更できるようになり、変更の信頼性も高まります。 ワークフローの例のように、ビジネス要件の観点で入力を定義するのが一般的です。 このように定義すると、変更点についてユーザーと共に検討しやすくなります。 そのため、デザイン時テンプレートは、アジャイル開発プロセスにおける有用なツールとなります。

 デザイン時テンプレートを作成するには、 **テキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFileGenerator**に設定することもできます。

 詳細については、「 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。 テンプレートの構文の詳細については、「 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

> [!NOTE]
> 1 つ以上のテンプレートで読み込まれるデータを示す際に、 *モデル* という用語を使用する場合があります。 モデルはどのような形式でもかまいません。あらゆる種類のファイルまたはデータベースを使用できます。 必ずしも UML モデルやドメイン固有言語モデルである必要はありません。 'モデル' は、コードのようなものではなく、ビジネス概念の観点でデータを定義できることを示します。

 テキスト テンプレート変換機能は、 *T4*と名付けられています。

## <a name="in-this-section"></a>このセクションの内容
 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md) テキストファイルを生成するアプリケーションでは、プリコンパイルされたテキストテンプレートは、テキストを定義するための簡単で信頼性の高い方法です。 ただし、この方法では、実行時にテキスト テンプレートを変更することができません。

 [T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md) モデルからコードやその他のリソースを生成すると、モデルを更新することによってアプリケーションを更新できます。

 [ビルドプロセスでのコード生成](../modeling/code-generation-in-a-build-process.md) 視覚化およびモデリング SDK がインストールされている場合は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 生成されたソフトウェアをモデルの変更に合わせて最新の状態に保つことができます。

 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md) テキストテンプレートファイルの構文。

 [チュートリアル: テキストテンプレートを使用したコードの生成](../modeling/walkthrough-generating-code-by-using-text-templates.md) コード生成を使用する1つの方法のデモ。

 [T4 テキストテンプレートのデバッグ](../modeling/debugging-a-t4-text-template.md) テキストテンプレートのデバッグ方法および一般的なテキストテンプレートエラー。

 [TextTransform ユーティリティを使用したファイルの生成](../modeling/generating-files-with-the-texttransform-utility.md) テキストテンプレート変換を実行するために使用できるコマンドラインツール。

 [T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md) 独自のデータソースのディレクティブプロセッサとカスタムテンプレートホストを作成する方法。

## <a name="see-also"></a>参照
 [ドメイン固有言語からコードを生成](../modeling/generating-code-from-a-domain-specific-language.md)[する UML モデルからファイルを生成する](../modeling/generate-files-from-a-uml-model.md)
