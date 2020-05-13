---
title: レガシー言語サービスの開発 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.vsip.LangServWiz.langtoks
- vs.vsip.LangServWiz.welcome
- vs.vsip.LangServWiz.langSpec
- vs.vsip.LangServWiz.langInfo
- vs.vsip.LangServWiz.langServOpts
helpviewer_keywords:
- language services, developing
ms.assetid: 6151ba88-c1c3-41de-a1cc-668f494d48d1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0c7f930d5087b6a822156fd44024def0d5b42b49
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708668"
---
# <a name="develop-a-legacy-language-service"></a>従来の言語サービスの開発
このセクションでは、従来の言語サービスの作成に役立つトピックへのリンクを示します。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 言語サービスを実装する新しい方法の詳細については、「[エディターと言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)

 コア エディターの最小限の言語サービスのモデル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を提供します。 このモデルは、独自の言語サービスを作成するためのガイドとして使用できます。

- [レガシー言語サービスインタフェース](../../extensibility/internals/legacy-language-service-interfaces.md)

 言語サービスの実装に必要なオブジェクトについて説明し、構文の強調表示、メソッド データ、およびその他の機能を提供するために使用できる追加のオブジェクトの一覧を示します。

- [従来の言語サービス コマンドをインターセプトする](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 言語サービスにコマンド フィルタを挿入して、テキスト ビューが処理するコマンドをインターセプトする方法について説明します。

- [従来の言語サービスを登録する](../../extensibility/internals/registering-a-legacy-language-service2.md)

 を使用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]して言語サービスを登録する方法について説明します。

- [デバッグのための言語サービスサポート](../../extensibility/internals/language-service-support-for-debugging.md)

 言語サービスがデバッガーをサポートする機能を提供する方法について説明します。

- [チェックリスト: 従来の言語サービスを作成する](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 コア エディターの言語サービスを作成および統合する手順について説明します。

## <a name="related-sections"></a>関連項目
- [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 言語サービスで構文の強調表示を実装する方法について説明します。

- [従来の言語サービスでのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 言語サービスが、入力を開始した言語キーワードまたは要素をユーザーが終了するプロセスについて説明します。

- [従来の言語サービスのパラメーター情報](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 オーバーロードされた関数およびメソッドのメソッドヒントを提供する方法について説明します。

- [方法: 従来の言語サービスで隠しテキストのサポートを提供する](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 隠しテキスト領域の目的について説明し、非表示のテキスト領域を実装する方法について説明します。

- [方法: 従来の言語サービスで拡張アウトライン サポートを提供する](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 [*定義に折りたたむ*] コマンドをサポートする以外に、言語のサポートを拡張する 2 つのオプションについて説明します。
