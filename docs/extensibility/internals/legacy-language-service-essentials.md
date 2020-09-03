---
title: レガシ言語サービスの要点 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 501bccf755293e86e8a9dc23fce125a10c882376
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707417"
---
# <a name="legacy-language-service-essentials"></a>従来の言語サービスの基本情報
プログラミング言語を Visual Studio に統合するには、言語サービスを提供する必要があります。 このトピックでは、従来の言語サービスで使用できる機能について説明します。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 言語サービスを実装する新しい方法の詳細については、「 [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

 従来の言語サービスでは、次の機能が提供されます。

|機能|説明|
|-------------|-----------------|
|構文の色分け表示|エディタービューで、言語のさまざまな要素に対して異なる色とフォントスタイルを表示します。 このような違いにより、ファイルの読み取りと編集が容易になります。<br /><br /> 一般的な情報については、「 [従来の言語サービスの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)表示」を参照してください。<br /><br /> Managed package framework (MPF) のこの機能の詳細については、「 [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)」を参照してください。|
|ステートメント入力候補|ユーザーが入力を開始したステートメントまたはキーワードを完了します。 ステートメント入力候補を使用すると、入力が少なく、エラーが発生する可能性が少なくなるため、ユーザーは複雑なステートメントを簡単に入力できます。<br /><br /> 一般的な情報については、「 [従来の言語サービスでのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)」を参照してください。<br /><br /> MPF のこの機能の詳細については、「 [従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)」を参照してください。|
|かっこの一致|中かっこなどのペアの文字を強調表示します。 ユーザーが "}" などの終了文字を入力すると、かっこの照合では、対応する開始文字 ("{" など) が強調表示されます。 囲み文字が複数ある場合、この機能を使用すると、ユーザーは、囲んでいる文字が正しくペアになっていることを確認できます。<br /><br /> MPF のこの機能の詳細については、「 [従来の言語サービスでの中かっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)」を参照してください。|
|パラメーター情報のヒント|ユーザーが現在入力しているオーバーロードされたメソッドに使用できるシグネチャの一覧を表示します。<br /><br /> 一般的な情報については、「 [従来の言語サービスのパラメーターヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)」を参照してください。<br /><br /> MPF のこの機能の詳細については、「 [従来の言語サービスのパラメーターヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)」を参照してください。|
|エラーマーカー|構文が間違っているテキストの下に赤い波線 (波線) を表示します。 通常、エラーマーカーは、スペルが間違っているキーワード、閉じていないかっこ、無効な文字、および類似したエラーをユーザーに認識させるために使用されます。<br /><br /> MPF クラスでは、エラーマーカーはクラスのメソッドで自動的に処理され <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink> ます。|

 これらの機能の多くでは、言語サービスでソースコードを解析する必要があります。 多くの場合、コンパイラまたはインタープリターのトークン化と解析コードを再利用できます。

 次の機能は、プログラミング言語のサポートに関連していますが、言語サービスには含まれていません。

| 機能 | 説明 |
|-----------------------| - |
| 式エバリュエーター | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ブレークポイントを検証し、[**自動変数**デバッグ] ウィンドウに表示される式の一覧を指定することにより、デバッガーをサポートします。<br /><br /> 詳細については、「 [デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)」を参照してください。 |
| シンボル参照ツール | **シンボル結果**の**オブジェクトブラウザー**、**クラスビュー**、**呼び出しブラウザー**、および検索をサポートします。 |
