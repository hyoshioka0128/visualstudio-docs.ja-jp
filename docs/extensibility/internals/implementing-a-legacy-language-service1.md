---
title: レガシ言語サービスの実装1 |マイクロソフトドキュメント
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
ms.openlocfilehash: c3805e49ffa83f7dea2ee58ef36e1bc8e48b1eaa
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707695"
---
# <a name="implementing-a-legacy-language-service"></a>従来の言語サービスの実装
マネージ パッケージ フレームワーク (MPF) のクラスを使用して、構文の強調表示、かっこの一致、IntelliSense の補完など、さまざまな機能をサポートする従来の言語サービスを実装できます。

 レガシ言語サービスは VSPackage の一部として実装されますが、言語サービス機能を実装する新しい方法は、MEF 拡張機能を使用することです。 言語サービスを実装する新しい方法の詳細については、「[エディターと言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

> [!NOTE]
> できるだけ早く新しいエディター API の使用を開始することをお勧めします。 これにより、言語サービスのパフォーマンスが向上し、新しいエディター機能を利用できるようになります。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスの概要](../../extensibility/internals/legacy-language-service-overview.md)

 MPF でサポートされている言語サービス機能の概要。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 MPF を使用して言語サービスを実装するために必要な内容について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

 に MPF ベースの言語サービスを登録するために必要な手順について説明[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 MPF を使用して言語サービスのすべての機能を実装するために必要な 2 つのパーサーについて説明します。

- [チュートリアル: 従来の言語サービスの作成](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 VSPackage で MPF 言語サービスを実装するために必要な基本的な手順を説明します。

- [チュートリアル: インストールされているコード スニペットの一覧の取得 (従来の実装)](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 インストールされているコード スニペットの一覧を取得する方法を示します。

- [従来の言語サービスの特徴](../../extensibility/internals/legacy-language-service-features1.md)

 MPF を使用して言語サービスのすべての機能を実装するために実行する必要がある内容について詳しく説明するトピックへのリンクを示します。
