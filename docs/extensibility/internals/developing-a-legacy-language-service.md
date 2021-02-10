---
title: 従来の言語サービスの開発 |Microsoft Docs
description: VSPackage の一部として、または Managed Extensibility Framework (MEF) 拡張機能を使用して、従来の言語サービスを実装する方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5f61337b6dbdef158c7fb7ebe42d0af9f79822fc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99959533"
---
# <a name="develop-a-legacy-language-service"></a>従来の言語サービスを開発する
このセクションでは、従来の言語サービスの作成に役立つトピックにリンクします。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 言語サービスを実装する新しい方法の詳細については、「 [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスのモデル](../../extensibility/internals/model-of-a-legacy-language-service.md)

 コアエディターの最小言語サービスのモデルを提供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 このモデルは、独自の言語サービスを作成するためのガイドとして使用できます。

- [従来の言語サービスインターフェイス](../../extensibility/internals/legacy-language-service-interfaces.md)

 言語サービスを実装するために必要なオブジェクトについて説明し、構文の強調表示、メソッドデータ、およびその他の機能を提供するために使用できる追加のオブジェクトの一覧を示します。

- [レガシ言語サービスコマンドのインターセプト](../../extensibility/internals/intercepting-legacy-language-service-commands.md)

 言語サービスにコマンドフィルターを挿入して、テキストビューで処理されるコマンドをインターセプトする方法について説明します。

- [従来の言語サービスを登録する](../../extensibility/internals/registering-a-legacy-language-service2.md)

 を使用して言語サービスを登録する方法について説明 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

- [デバッグのための言語サービスのサポート](../../extensibility/internals/language-service-support-for-debugging.md)

 言語サービスがデバッガーをサポートする機能を提供する方法について説明します。

- [チェックリスト: 従来の言語サービスを作成する](../../extensibility/internals/checklist-creating-a-legacy-language-service.md)

 コアエディターの言語サービスを作成および統合するための詳細な手順について説明します。

## <a name="related-sections"></a>関連項目
- [従来の言語サービスでの構文の色分け](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 言語サービスで構文の強調表示を実装する方法について説明します。

- [従来の言語サービスでのステートメント入力候補](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)

 ステートメント入力候補について説明します。このプロセスでは、言語サービスは、ユーザーが入力を開始した言語キーワードまたは要素を完了するのに役立ちます。

- [従来の言語サービスのパラメーターヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)

 オーバーロードされた関数およびメソッドに対してメソッドのヒントを提供する方法について説明します。

- [方法: 従来の言語サービスで非表示テキストのサポートを提供する](../../extensibility/internals/how-to-provide-hidden-text-support-in-a-legacy-language-service.md)

 非表示テキスト領域の目的について説明し、非表示のテキスト領域を実装する方法について説明します。

- [方法: 従来の言語サービスで拡張されたアウトラインサポートを提供する](../../extensibility/internals/how-to-provide-expanded-outlining-support-in-a-legacy-language-service.md)

 [ *定義に折りたたむ* ] コマンドをサポートすること以外に、言語のアウトラインサポートを拡張する2つのオプションについて説明します。
