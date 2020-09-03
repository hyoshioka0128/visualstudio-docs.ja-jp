---
title: T4 テキスト変換のカスタマイズ
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8e35c279f397f1228c17fb6a41a18a2fe583ab88
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75589735"
---
# <a name="customize-t4-text-transformation"></a>T4 テキスト変換をカスタマイズする

テキストテンプレートは、変換プロセスを使用してプログラムコードやその他のテキストファイルを生成できるようにする Visual Studio の機能です。 を使用 [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] すると、テキストテンプレートディレクティブプロセッサまたはテキストテンプレートホストをカスタマイズすることで、既定のテンプレート変換プロセスを拡張できます。

## <a name="in-this-section"></a>このセクションの内容

 [テキストテンプレート変換プロセス](../modeling/the-text-template-transformation-process.md) テキスト変換のしくみについて説明し、テンプレートホストとディレクティブプロセッサの役割について説明します。

 [カスタム T4 テキストテンプレートディレクティブプロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md) ディレクティブプロセッサは、テンプレートのコンパイル中に実行されるなど、テンプレート内のディレクティブを `<#@template#>.` 処理し、アセンブリやその他のリソースを読み込むことができます。 また、実行時にリソースを読み込むコードを挿入することもできます。 独自のディレクティブプロセッサを定義することで、テンプレートの複雑さを軽減できます。

 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md) メニューコマンドやイベントハンドラーなどの Visual Studio 拡張機能を作成する場合、拡張機能ではテキストテンプレートサービスを使用してテキストテンプレートを変換できます。 パラメーターデータは、セッションオブジェクトを使用してテンプレートに渡すことができます。また、ディレクティブを使用して、テンプレート内から値を取得することもでき `<#@parameter#>` ます。

 [カスタムホストを使用したテキストテンプレートの処理](../modeling/processing-text-templates-by-using-a-custom-host.md) テキストテンプレートのコードが実行されると、ホストは外部ファイルおよびアプリケーションの状態へのアクセスを提供します。 たとえば、Visual Studio でテキスト変換を実行するホストは、 **ソリューションエクスプローラー**へのアクセスを提供できます。 また、エラーメッセージウィンドウにエラーが表示されます。 テキスト変換を別のコンテキストで実行する場合は、そのコンテキストで利用可能なサービスへのアクセスを提供する独自のホストを定義できます。

 Visual Studio 拡張機能を作成する場合は、独自のホストを作成するのではなく、既存のテキスト変換サービスを使用することを検討してください。 詳細については、「 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

## <a name="reference"></a>関連項目

- [T4 テキストテンプレートの記述](../modeling/writing-a-t4-text-template.md) テキストテンプレートのディレクティブとコントロールブロックの構文を提供します。
