---
title: カスタム ホストを使用したテキスト テンプレートの処理
description: テキストテンプレート変換プロセスで入力としてテキストテンプレートファイルを取得し、出力としてテキストファイルを生成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b1a4e4c2177e388db1de0b42fe10d92daa1a3e67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99934911"
---
# <a name="process-text-templates-by-using-a-custom-host"></a>カスタム ホストを使用してテキスト テンプレートを処理する

*テキストテンプレート変換* プロセスでは、*テキストテンプレート* ファイルが入力として取得され、テキストファイルが出力として生成されます。 テキスト変換エンジンは、Visual Studio 拡張機能から、または Visual Studio がインストールされているコンピューターで実行されているスタンドアロンアプリケーションから呼び出すことができます。 ただし、 *テキストテンプレートホスト* を指定する必要があります。 このクラスは、テンプレートを環境に接続し、アセンブリやインクルード ファイルなどのリソースの検索と、出力およびエラー メッセージの処理を行います。

> [!TIP]
> Visual Studio 内で実行されるパッケージまたは拡張機能を作成する場合は、独自のホストを作成するのではなく、テキストテンプレートサービスを使用することを検討してください。 詳細については、「 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

> [!NOTE]
> サーバー アプリケーションでテキスト テンプレート変換を使用することはお勧めしません。 また、シングル スレッド以外でテキスト テンプレート変換を使用することはお勧めしません。 テキスト テンプレート エンジンでは、単一の AppDomain を再利用して、テンプレートを変換、コンパイル、および実行するためです。 変換されたコードは、スレッド セーフになるように設計されているわけではありません。 エンジンは、デザイン時に Visual Studio プロジェクト内にあるため、ファイルを順番に処理するように設計されています。
>
> ランタイムアプリケーションの場合は、前処理されたテキストテンプレートの使用を検討してください。 [T4 テキストテンプレートを使用した実行時のテキスト生成に](../modeling/run-time-text-generation-with-t4-text-templates.md)関する説明を参照してください。

コンパイル時に決定されるテンプレートのセットをアプリケーションで使用する場合は、前処理されたテキスト テンプレートを使用する方が簡単です。 また、Visual Studio がインストールされていないコンピューターでアプリケーションを実行する場合にも、この方法を使用できます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

## <a name="execute-a-text-template-in-your-application"></a>アプリケーションでテキストテンプレートを実行する

テキスト テンプレートを実行するには、<xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> の ProcessTemplate メソッドを呼び出します。

```csharp
using Microsoft.VisualStudio.TextTemplating;
...
Engine engine = new Engine();
string output = engine.ProcessTemplate(templateString, host);
```

 アプリケーションでは、テンプレートを見つけて提供すると共に、出力を処理する必要があります。

 パラメーターでは `host` 、 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))を実装するクラスを指定する必要があります。 これはエンジンによってコールバックされます。

 ホストは、エラーのログ記録、アセンブリとインクルード ファイルへの参照の解決、テンプレートを実行できるアプリケーション ドメインの指定、各ディレクティブの適切なプロセッサの呼び出しを実行できる必要があります。

 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> は **\*.0.dllVisualStudio** で定義されており、 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) は VisualStudio で定義されています。また、 **\*.0.dll** で定義されています。

## <a name="in-this-section"></a>このセクションの内容
 [チュートリアル: カスタムテキストテンプレートホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md) Visual Studio の外部でテキストテンプレート機能を使用できるようにするカスタムテキストテンプレートホストを作成する方法について説明します。

## <a name="reference"></a>リファレンス
 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))

## <a name="related-sections"></a>関連項目

- [テキストテンプレート変換プロセスでは](../modeling/the-text-template-transformation-process.md) 、テキスト変換のしくみと、カスタマイズできるパーツについて説明します。
- [カスタム T4 テキストテンプレートディレクティブプロセッサを作成する](../modeling/creating-custom-t4-text-template-directive-processors.md) と、テキストテンプレートディレクティブプロセッサの概要が示されます。
