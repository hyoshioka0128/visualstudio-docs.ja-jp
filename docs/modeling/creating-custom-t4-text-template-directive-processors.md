---
title: カスタム T4 テキスト テンプレート ディレクティブ プロセッサの作成
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, custom directive processors
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c70aa1853701ef671b7057ad698a0fb63334a1ca
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597179"
---
# <a name="create-custom-t4-text-template-directive-processors"></a>カスタム T4 テキスト テンプレート ディレクティブ プロセッサを作成する

*テキストテンプレート変換プロセス*では、*テキストテンプレート*ファイルが入力として取得され、テキストファイルが出力として生成されます。 *テキストテンプレート変換エンジン*はプロセスを制御し、エンジンはテキストテンプレート変換ホストと1つ以上のテキストテンプレート*ディレクティブプロセッサ*を操作してプロセスを完了します。 詳細については、次を参照してください。 [テキスト テンプレート変換プロセス](../modeling/the-text-template-transformation-process.md)

カスタム ディレクティブ プロセッサを作成するには、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> を継承するクラスを作成します。

これらの2つの違いは、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> は、ユーザーからパラメーターを取得し、テンプレートの出力ファイルを生成するコードを生成するために必要な最小限のインターフェイスを実装することです。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> は、要求/提供デザインパターンを実装します。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> は、`requires` と `provides`の2つの特別なパラメーターを処理します。  たとえば、カスタムディレクティブプロセッサは、ユーザーからのファイル名を受け取り、ファイルを開いて読み取り、そのファイルのテキストを `fileText`という名前の変数に格納する場合があります。 <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor> クラスのサブクラスは、`requires` パラメーターの値としてユーザーからファイル名を受け取り、`provides` パラメーターの値としてテキストを格納する変数の名前を受け取る場合があります。 このプロセッサは、ファイルを開いて読み取り、指定した変数にファイルのテキストを格納します。

Visual Studio でテキストテンプレートからカスタムディレクティブプロセッサを呼び出す前に、それを登録する必要があります。

レジストリキーを追加する方法の詳細については、「[カスタムディレクティブプロセッサの配置](../modeling/deploying-a-custom-directive-processor.md)」を参照してください。

## <a name="custom-directives"></a>カスタムディレクティブ

カスタムディレクティブは次のようになります。

`<#@ MyDirective Processor="MyDirectiveProcessor" parameter1="value1" ... #>`

テキストテンプレートから外部データまたはリソースにアクセスする場合は、カスタムディレクティブプロセッサを使用できます。

複数のテキストテンプレートで、1つのディレクティブプロセッサが提供する機能を共有できます。そのため、ディレクティブプロセッサを使用すると、コードを再利用することができます。 組み込みの `include` ディレクティブは似ています。これは、コードを記述して別のテキストテンプレート間で共有するために使用できるためです。 違いは、`include` ディレクティブによって提供される機能が固定されていて、パラメーターを受け入れないことです。 テキストテンプレートに共通の機能を提供し、テンプレートでパラメーターを渡すことができるようにするには、カスタムディレクティブプロセッサを作成する必要があります。

カスタムディレクティブプロセッサの例としては、次のようなものがあります。

- パラメーターとしてユーザー名とパスワードを受け取るデータベースからデータを返すディレクティブプロセッサ。

- ファイルの名前をパラメーターとして受け取るファイルを開いて読み取るためのディレクティブプロセッサ。

### <a name="principal-parts-of-a-custom-directive-processor"></a>カスタムディレクティブプロセッサの主要部分

ディレクティブプロセッサを開発するには、<xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> または <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>のいずれかから継承するクラスを作成する必要があります。

実装する必要がある最も重要な `DirectiveProcessor` メソッドは次のとおりです。

- `bool IsDirectiveSupported(string directiveName)`-ディレクティブプロセッサが名前付きディレクティブを処理できる場合は `true` を返します。

- `void ProcessDirective (string directiveName, IDictionary<string, string> arguments)`-テンプレートエンジンは、テンプレート内でディレクティブが出現するたびにこのメソッドを呼び出します。 プロセッサは結果を保存する必要があります。

ProcessDirective () を呼び出すと、テンプレートエンジンは次のメソッドを呼び出します。

- `string[] GetReferencesForProcessingRun()`-テンプレートコードで必要とされるアセンブリの名前を返します。

- `string[] GetImportsForProcessingRun()`-テンプレートコードで使用できる名前空間を返します。

- `string GetClassCodeForProcessingRun()`-テンプレートコードで使用できるメソッド、プロパティ、およびその他の宣言のコードを返します。 これを行う最も簡単な方法は、 C#または Visual Basic コードを含む文字列を作成することです。 任意の CLR 言語を使用するテンプレートからディレクティブプロセッサを呼び出すことができるようにするには、ステートメントを CodeDom ツリーとして構築し、テンプレートで使用される言語でツリーをシリアル化した結果を返すことができます。

- 詳細については、「[チュートリアル: カスタムディレクティブプロセッサを作成](../modeling/walkthrough-creating-a-custom-directive-processor.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [カスタムディレクティブプロセッサをデプロイ](../modeling/deploying-a-custom-directive-processor.md)するカスタムディレクティブプロセッサを登録する方法について説明します。
- [チュートリアル: カスタム](../modeling/walkthrough-creating-a-custom-directive-processor.md)ディレクティブプロセッサを作成する方法、カスタムディレクティブプロセッサを作成する方法、ディレクティブプロセッサを登録およびテストする方法、および出力ファイルを HTML として書式設定する方法について説明します。
