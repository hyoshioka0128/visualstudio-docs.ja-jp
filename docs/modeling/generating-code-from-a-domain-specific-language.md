---
title: ドメイン固有言語からのコード生成
ms.date: 11/04/2016
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34b834957dfe18e3fc03a86130a95071dda0badf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75596581"
---
# <a name="generating-code-from-a-domain-specific-language"></a>ドメイン固有言語からのコード生成

Microsoft [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] では、モデルで表されるデータからコード、ドキュメント、構成ファイル、およびその他の成果物を生成するための強力な方法を提供しています。 を使用 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] すると、データを表すクラスのセットを作成できます。また、名前とプロパティにそのデータが反映されたクラスにテキストテンプレートを記述することもできます。

たとえば、Fabrikam には、顧客名と電子メールアドレスの XML ファイルがあります。 開発者は、顧客がクラスであり、プロパティ名と電子メールを含むモデルを作成します。 データを処理するために複数のテキストテンプレートを記述します。このフラグメントを使用すると、すべての顧客のテーブルが HTML ページの一部として生成されます。

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

顧客データベースが処理されると、XML ファイルがモデルストアに読み込まれます。 を使用して作成された *ディレクティブプロセッサ*を使用すると、 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] テキストテンプレート内のコードで Customer クラスを使用できるようになります。 多くのテキストテンプレートは、同じストアに対して実行できます。

テキストテンプレートは、に不可欠です [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 。 これらは、ツールを Visual Studio と統合するために使用される VSPackage およびコントロールに加えて、ドメインモデルの要素のソースコードを生成するために使用されます。

ここでは、で使用されるテキストテンプレートを作成、変更、およびデバッグするためのいくつかの方法について説明し [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] ます。

## <a name="in-this-section"></a>このセクションの内容

[テキストテンプレートからのモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)\
テキストテンプレートでドメイン固有言語を参照する方法についての基本的な情報を提供します。

[チュートリアル: モデルにアクセスするテキストテンプレートのデバッグ](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)\
ドメイン固有言語を参照するテキストテンプレートでトラブルシューティングとデバッグを行う方法について説明します。

[チュートリアル: 生成されたディレクティブプロセッサへのホストの接続](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)\
生成されたディレクティブプロセッサにカスタムホストを接続する方法について説明します。

[DslTextTransform コマンド](../modeling/the-dsltexttransform-command.md)\
ドメイン固有言語を参照するテキストテンプレートのコマンドラインで TextTransform 実行可能ファイルを実行するコマンドファイルについて説明します。

## <a name="reference"></a>リファレンス

[T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)\
テキストテンプレートディレクティブとコントロールブロックの構文を提供します。

## <a name="related-sections"></a>関連項目

[T4 テキストテンプレートを使用したデザイン時のコード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)\
テキストテンプレート変換プロセスについて説明します。

[ビルドプロセスでのコード生成](../modeling/code-generation-in-a-build-process.md)\
ビルドサーバーで DSL からファイルを生成する場合は、このトピックをお読みください。
