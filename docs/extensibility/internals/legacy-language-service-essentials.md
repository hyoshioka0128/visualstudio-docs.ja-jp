---
title: レガシー言語サービスの基本 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707417"
---
# <a name="legacy-language-service-essentials"></a>従来の言語サービスの基本情報
プログラミング言語を Visual Studio に統合するには、言語サービスを提供する必要があります。 このトピックでは、従来の言語サービスで使用できる機能について説明します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 言語サービスを実装する新しい方法の詳細については、「[エディターと言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

 従来の言語サービスには、次の機能があります。

|機能|説明|
|-------------|-----------------|
|構文の色分け表示|言語の要素ごとに、エディター ビューに異なる色とフォント スタイルを表示させます。 この違いにより、ファイルの読み取りと編集が容易になります。<br /><br /> 一般的な情報については、「[従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)」を参照してください。<br /><br /> 管理パッケージ フレームワーク (MPF) のこの機能については、[レガシー言語サービスでの構文の色分けを](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)参照してください。|
|ステートメント入力候補|ユーザーが入力を開始したステートメントまたはキーワードを完了します。 ステートメント入力候補は、ユーザーが入力が少なく、エラーの可能性が少なく、難しいステートメントをより簡単に入力するのに役立ちます。<br /><br /> 一般的な情報については、「[レガシ言語サービスでのステートメントの補完](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)」を参照してください。<br /><br /> MPF のこの機能の詳細については、「[レガシ言語サービスでの Word の入力候補](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)」を参照してください。|
|かっこの一致|中かっこなどのペア文字を強調表示します。 ユーザーが「}」などの終了文字を入力すると、中かっこの一致は対応する開始文字 ("{" など) を強調表示します。 囲む文字が複数のレベルにある場合、この機能を使用すると、囲む文字が正しくペアになっていることをユーザーが確認できます。<br /><br /> MPF のこの機能の詳細については、「[レガシ言語サービスでのブレースの照合](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)」を参照してください。|
|パラメータ情報ツールチップ|ユーザーが現在入力しているオーバーロードされたメソッドのシグネチャの一覧を表示します。<br /><br /> 一般的な情報については、「[レガシ言語サービスのパラメータ情報](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)」を参照してください。<br /><br /> MPF のこの機能の詳細については、「[レガシ言語サービスのパラメーター情報](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)」を参照してください。|
|エラー マーカー|構文が正しくないテキストの下に、波状の赤い下線 (波線とも呼ばれる) を表示します。 エラー マーカーは、通常、ユーザーに、スペルミスのキーワード、閉じられていないかっこ、無効な文字、および類似のエラーをユーザーに知させるために使用されます。<br /><br /> MPF クラスでは、エラー マーカーはクラスの<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A>メソッドで自動的に<xref:Microsoft.VisualStudio.Package.AuthoringSink>処理されます。|

 これらの機能の多くは、ソース コードを解析するために言語サービスを必要とします。 多くの場合、コンパイラまたはインタプリタのトークン化と解析のコードを再利用できます。

 以下の機能は、プログラミング言語のサポートに関連していますが、言語サービスには含まれません。

| 機能 | 説明 |
|-----------------------| - |
| 式エバリュエーター | ブレークポイントを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]検証し **、Autos**デバッグ ウィンドウに表示される式の一覧を指定することで、デバッガーをサポートします。<br /><br /> 詳細については、「[デバッグ用の言語サービス サポート](../../extensibility/internals/language-service-support-for-debugging.md)」を参照してください。 |
| シンボル参照ツール | **オブジェクト ブラウザ**、**クラス ビュー**、**呼び出しブラウザ**、および**シンボル結果の検索**をサポートしています。 |
