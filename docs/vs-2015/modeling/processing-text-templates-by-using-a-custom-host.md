---
title: カスタムホストを使用したテキストテンプレートの処理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, in application or VS extension
- text templates, custom directive hosts
ms.assetid: affa3296-854d-47d6-9685-285f6d9ba5dc
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 71f18fbbf9f2d5c587c2cd0961c6625467f4f298
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72652450"
---
# <a name="processing-text-templates-by-using-a-custom-host"></a>カスタム ホストを使用したテキスト テンプレートの処理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*テキストテンプレート変換*プロセスでは、*テキストテンプレート*ファイルが入力として取得され、テキストファイルが出力として生成されます。 テキスト変換エンジンは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能か、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされているコンピューターで実行中のスタンドアロン アプリケーションから呼び出すことができます。 ただし、 *テキストテンプレートホスト*を指定する必要があります。 このクラスは、テンプレートを環境に接続し、アセンブリやインクルード ファイルなどのリソースの検索と、出力およびエラー メッセージの処理を行います。

> [!TIP]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内で実行されるパッケージまたは拡張機能を作成する場合は、独自のホストを作成するのではなく、テキスト テンプレート サービスを使用することを検討します。 詳細については、「 [VS 拡張機能でのテキスト変換の呼び出し](../modeling/invoking-text-transformation-in-a-vs-extension.md)」を参照してください。

> [!NOTE]
> サーバー アプリケーションでテキスト テンプレート変換を使用することはお勧めしません。 また、シングル スレッド以外でテキスト テンプレート変換を使用することはお勧めしません。 テキスト テンプレート エンジンでは、単一の AppDomain を再利用して、テンプレートを変換、コンパイル、および実行するためです。 変換されたコードは、スレッド セーフになるように設計されているわけではありません。 デザイン時にはファイルは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトに含まれているので、このエンジンはファイルを連続的に処理するように設計されています。
>
> ランタイムアプリケーションの場合は、前処理されたテキストテンプレートの使用を検討してください。 [T4 テキストテンプレートを使用した実行時のテキスト生成に](../modeling/run-time-text-generation-with-t4-text-templates.md)関する説明を参照してください。

 コンパイル時に決定されるテンプレートのセットをアプリケーションで使用する場合は、前処理されたテキスト テンプレートを使用する方が簡単です。 この方法は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされていないコンピューターでアプリケーションを実行する場合にも使用できます。 詳細については、「 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

## <a name="executing-a-text-template-in-your-application"></a>アプリケーションでのテキスト テンプレートの実行
 テキスト テンプレートを実行するには、<xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> の ProcessTemplate メソッドを呼び出します。

```
using Microsoft.VisualStudio.TextTemplating;
...
Engine engine = new Engine();
string output = engine.ProcessTemplate(templateString, host);
```

 アプリケーションでは、テンプレートを見つけて提供すると共に、出力を処理する必要があります。

 パラメーターでは `host` 、 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))を実装するクラスを指定する必要があります。 これはエンジンによってコールバックされます。

 ホストは、エラーのログ記録、アセンブリとインクルード ファイルへの参照の解決、テンプレートを実行できるアプリケーション ドメインの指定、各ディレクティブの適切なプロセッサの呼び出しを実行できる必要があります。

 <xref:Microsoft.VisualStudio.TextTemplating.Engine?displayProperty=fullName> は ** \*.0.dllVisualStudio **で定義されており、 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) は VisualStudio で定義されています。また、 ** \*.0.dll**で定義されています。

## <a name="in-this-section"></a>このセクションの内容
 [チュートリアル: カスタムテキストテンプレートホストの作成](../modeling/walkthrough-creating-a-custom-text-template-host.md) テキストテンプレート機能を外部で使用できるようにするカスタムテキストテンプレートホストを作成する方法について説明し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

## <a name="reference"></a>リファレンス
 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))

## <a name="related-sections"></a>関連項目
 [テキストテンプレート変換プロセス](../modeling/the-text-template-transformation-process.md) テキスト変換のしくみと、カスタマイズできる部分について説明します。

 [カスタム T4 テキストテンプレートディレクティブプロセッサの作成](../modeling/creating-custom-t4-text-template-directive-processors.md) テキストテンプレートディレクティブプロセッサの概要について説明します。
