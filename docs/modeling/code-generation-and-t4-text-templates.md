---
title: コード生成と T4 テキスト テンプレート
ms.date: 11/04/2016
ms.topic: overview
f1_keywords:
- VS.ToolsOptionsPages.TextTemplating.TextTemplating
helpviewer_keywords:
- generating text
- .tt files
- code generation
- text templates
- generating code
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fbcd41461ab57e3bbb5fb48849ddde8593c587fb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548240"
---
# <a name="code-generation-and-t4-text-templates"></a>コード生成と T4 テキスト テンプレート

Visual Studio では、 *T4 テキストテンプレート*はテキストブロックとコントロールロジックを組み合わせたもので、テキストファイルを生成できます。 制御ロジックは、 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] または [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]のプログラム コードのフラグメントとして記述します。 Visual Studio 2015 Update 2 以降では、T4 テンプレート ディレクティブで C# バージョン 6.0 の機能を使用できます。 生成されるファイルは、web ページ、リソースファイル、任意の言語のプログラムソースコードなど、あらゆる種類のテキストにすることができます。

T4 テキストテンプレートには、実行時とデザイン時の2種類があります。

## <a name="run-time-t4-text-templates"></a>実行時 T4 テキストテンプレート

"前処理された" テンプレートとも呼ばれる実行時テンプレートは、通常、出力の一部としてテキスト文字列を生成するためにアプリケーションで実行されます。 たとえば、次のように HTML ページを定義するテンプレートを作成できます。

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

アプリケーションは、Visual Studio がインストールされていないコンピューターで実行できます。

実行時テンプレートを作成するには、 **前処理されたテキスト テンプレート** ファイルをプロジェクトに追加します。 または、プレーンテキスト ファイルを追加し、 **[カスタム ツール]** プロパティを **TextTemplatingFilePreprocessor**に設定することもできます。

詳細については、「 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。 テンプレートの構文の詳細については、「 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

## <a name="design-time-t4-text-templates"></a>デザイン時 T4 テキストテンプレート

デザイン時テンプレートは、アプリケーションのソースコードとその他のリソースの一部を定義します。 通常は、1つの入力ファイルまたはデータベースのデータを読み取り、 *.cs*、 *.vb*、またはその他のソースファイルの一部を生成する複数のテンプレートを使用します。 テンプレートごとに 1 つのファイルが生成されます。 これらは、Visual Studio または MSBuild 内で実行されます。

たとえば、入力データが構成データの XML ファイルであるとします。 開発中に XML ファイルを編集するたびに、テキストテンプレートによってアプリケーションコードの一部が再生成されます。 テンプレートの例を次に示します。

```
<#@ output extension=".cs" #>
<#@ assembly name="System.Xml" #>
<#
 System.Xml.XmlDocument configurationData = ...; // Read a data file here.
#>
namespace Fabrikam.<#= configurationData.SelectSingleNode("jobName").Value #>
{
  ... // More code here.
}
```

XML ファイルの値によっては、生成された *.cs*ファイルは次のようになります。

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

## <a name="see-also"></a>関連項目

- [ドメイン固有言語からコードを生成する](../modeling/generating-code-from-a-domain-specific-language.md)
