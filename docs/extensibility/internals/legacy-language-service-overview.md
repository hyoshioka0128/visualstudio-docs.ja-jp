---
title: 従来の言語サービスの概要 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], about language services
ms.assetid: bb44e27b-d228-463c-b2cf-cd5c24c7c1b5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aed653ec200063e72434fc758c7920e6caabafe1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707356"
---
# <a name="legacy-language-service-overview"></a>従来の言語サービスの概要
言語サービスでは、特定の機能を実装できるエディターのサポートが提供され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 Managed Package Framework (MPF) 言語サービスクラスは、頻繁に使用される機能とその他の機能の部分的なサポートを完全にサポートしています。

## <a name="fully-supported-features-in-the-mpf"></a>MPF で完全にサポートされている機能
 MPF 言語サービスクラスは、次の機能をサポートしています。

- 構文の強調表示

- アウトライン

- コードブロックのコメント化

- かっこの一致

- コード スニペット

- カスタムドキュメントのプロパティ

- IntelliSense のパラメーター情報

- IntelliSense のクイックヒント

- IntelliSense メンバーの完了

- IntelliSense の単語入力候補

## <a name="partially-supported-features-in-the-mpf"></a>MPF で部分的にサポートされている機能
 MPF では、次の機能の一部のみがサポートされています。 これは、MPF によって呼び出されるメソッドを実装する必要があることを意味します。

- コードを再フォーマットします。 再フォーマットを実装するコードを指定します。

- 有効なコード範囲を識別してブレークポイントを検証します。 コードの範囲を識別するコードを指定します。

- 変数を表示するためのデバッガーの [ **自動** 変数] ウィンドウのサポート。 ウィンドウに表示する内容を決定するコードを指定します。

- 型とメンバーの間をすばやく移動するための **ナビゲーションバー** のサポート。 を実装し、 **ナビゲーションバー** のコンボボックスにリストを設定するヘルパークラスを返します。

## <a name="implementation"></a>実装
 言語サービス自体と言語をサポートする言語サービス機能を実装するには、いくつかの手順を実行する必要があります。 これらの手順については、次のトピックで説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

- [従来の言語サービスのアウトライン](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

- [従来の言語サービスのコメント コード](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

- [従来の言語サービスの再フォーマット コード](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

- [従来の言語サービスのカスタム ドキュメント プロパティ](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

- [従来の言語サービスでのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

- [従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

- [従来の言語サービスでのメンバー補完](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

- [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

- [従来の言語サービスのクイック ヒント](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

- [従来の言語サービスでの自動変数ウィンドウのサポート](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

- [従来の言語サービスでのブレークポイントの検証](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)
