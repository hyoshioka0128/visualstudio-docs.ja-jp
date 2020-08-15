---
title: レガシ言語の実装 Service1 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2535c527fc3d2d94609246959c5293e455b9808d
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238752"
---
# <a name="implementing-a-legacy-language-service-1"></a>従来の言語サービスの実装1
Managed package framework (MPF) のクラスを使用して、構文の強調表示、かっこの一致、IntelliSense の入力候補など、さまざまな機能をサポートする従来の言語サービスを実装できます。

 従来の言語サービスは VSPackage の一部として実装されていますが、言語サービス機能を実装するための新しい方法として、MEF 拡張機能を使用することをお勧めします。 言語サービスを実装する新しい方法の詳細については、「 [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、エディターの新機能を利用できるようになります。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)

 MPF でサポートされている言語サービス機能の概要について説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 MPF を使用して言語サービスを実装するために必要な事項について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

 MPF ベースの言語サービスをに登録するために必要な手順について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 MPF を使用して言語サービスのすべての機能を実装するために必要な2つのパーサーについて説明します。

- [チュートリアル: 従来の言語サービスの作成](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 VSPackage で MPF 言語サービスを実装するために必要な基本的な手順について説明します。

- [チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 インストールされているコードスニペットの一覧を取得する方法を示します。

- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)

 MPF を使用して言語サービスのすべての機能を実装するために必要な作業について詳しく説明したトピックへのリンクを示します。
