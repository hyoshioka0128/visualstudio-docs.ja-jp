---
title: カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成
description: テキストテンプレート変換プロセスと、カスタム T4 テキストテンプレートディレクティブプロセッサを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 283f2122c05a91a5e677293f59e3f6e02d43f63a
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97363428"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>カスタム T4 テキスト テンプレート ディレクティブ プロセッサを作成する

*テキストテンプレート変換プロセス* では、*テキストテンプレート* ファイルが入力として取得され、テキストファイルが出力として生成されます。 *テキストテンプレート変換エンジン* はプロセスを制御し、エンジンはテキストテンプレート変換ホストと1つ以上のテキストテンプレート *ディレクティブプロセッサ* を操作してプロセスを完了します。 詳細については、「 [テキストテンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)」を参照してください。

カスタム ディレクティブ プロセッサを作成するには、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> を継承するクラスを作成します。

これら2つの違いは、は、 <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ユーザーからパラメーターを取得し、テンプレート出力ファイルを生成するコードを生成するために必要な最小インターフェイスを実装するという点です。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> 要求/提供デザインパターンを実装します。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> は、との2つの特殊なパラメーターを処理し `requires` `provides` ます。  たとえば、カスタムディレクティブプロセッサは、ユーザーからのファイル名を受け取り、ファイルを開いて読み取り、ファイルのテキストをという名前の変数に格納する場合があり `fileText` ます。 クラスのサブクラスは、パラメーターの値とし <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> てユーザーからファイル名を取得し、 `requires` パラメーターの値としてテキストを格納する変数の名前を受け取る場合があり `provides` ます。 このプロセッサは、ファイルを開いて読み取り、指定した変数にファイルのテキストを格納します。

Visual Studio でテキストテンプレートからカスタムディレクティブプロセッサを呼び出す前に、それを登録する必要があります。

レジストリキーを追加する方法の詳細については、「 [カスタムディレクティブプロセッサの配置](../modeling/deploying-a-custom-directive-processor.md)」を参照してください。

## <a name="custom-directives"></a>カスタムディレクティブ

カスタムディレクティブは次のようになります。

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

テキストテンプレートから外部データまたはリソースにアクセスする場合は、カスタムディレクティブプロセッサを使用できます。

複数のテキストテンプレートで、1つのディレクティブプロセッサが提供する機能を共有できます。そのため、ディレクティブプロセッサを使用すると、コードを再利用することができます。 組み込み `include` ディレクティブは似ています。これは、コードを記述したり、異なるテキストテンプレート間で共有したりするために使用できるためです。 違いは、ディレクティブが提供するすべての機能が固定されていて、 `include` パラメーターを受け入れないことです。 テキストテンプレートに共通の機能を提供し、テンプレートでパラメーターを渡すことができるようにするには、カスタムディレクティブプロセッサを作成する必要があります。

カスタムディレクティブプロセッサの例としては、次のようなものがあります。

- パラメーターとしてユーザー名とパスワードを受け取るデータベースからデータを返すディレクティブプロセッサ。

- ファイルの名前をパラメーターとして受け取るファイルを開いて読み取るためのディレクティブプロセッサ。

### <a name="principal-parts-of-a-custom-directive-processor"></a>カスタムディレクティブプロセッサの主要部分

ディレクティブプロセッサを開発するには、またはのいずれかから継承するクラスを作成する必要があり <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> ます。

実装する必要がある最も重要な `DirectiveProcessor` 方法は次のとおりです。

- `bool IsDirectiveSupported(string directiveName)` - `true` ディレクティブプロセッサが名前付きディレクティブを処理できる場合は、を返します。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)` -テンプレートエンジンは、テンプレート内でディレクティブが出現するたびに、このメソッドを呼び出します。 プロセッサは結果を保存する必要があります。

ProcessDirective () を呼び出すと、テンプレートエンジンは次のメソッドを呼び出します。

- `string[] GetReferencesForProcessingRun()` -テンプレートコードで必要とされるアセンブリの名前を返します。

- `string[] GetImportsForProcessingRun()` -テンプレートコードで使用できる名前空間を返します。

- `string GetClassCodeForProcessingRun()` -テンプレートコードで使用できるメソッド、プロパティ、およびその他の宣言のコードを返します。 これを行う最も簡単な方法は、C# または Visual Basic コードを含む文字列を作成することです。 任意の CLR 言語を使用するテンプレートからディレクティブプロセッサを呼び出すことができるようにするには、ステートメントを CodeDom ツリーとして構築し、テンプレートで使用される言語でツリーをシリアル化した結果を返すことができます。

- 詳細については、「 [チュートリアル: カスタムディレクティブプロセッサを作成](../modeling/walkthrough-creating-a-custom-directive-processor.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [カスタムディレクティブプロセッサをデプロイ](../modeling/deploying-a-custom-directive-processor.md) するカスタムディレクティブプロセッサを登録する方法について説明します。
- [チュートリアル: カスタム](../modeling/walkthrough-creating-a-custom-directive-processor.md) ディレクティブプロセッサを作成する方法、カスタムディレクティブプロセッサを作成する方法、ディレクティブプロセッサを登録およびテストする方法、および出力ファイルを HTML として書式設定する方法について説明します。
