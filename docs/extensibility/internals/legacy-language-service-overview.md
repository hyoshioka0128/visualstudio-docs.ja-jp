---
title: レガシー言語サービスの概要 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707356"
---
# <a name="legacy-language-service-overview"></a>従来の言語サービスの概要
言語サービスは、特定[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の機能を実装できるエディター サポートを提供します。 管理パッケージ フレームワーク (MPF) 言語サービス クラスは、頻繁に使用される機能の完全なサポートと、他の機能の部分的なサポートを提供します。

## <a name="fully-supported-features-in-the-mpf"></a>MPF で完全にサポートされる機能
 MPF 言語サービス・クラスは、以下の機能をサポートします。

- 構文の強調表示

- アウトライン

- コードブロックのコメント

- かっこの一致

- コード スニペット

- カスタム ドキュメント プロパティ

- パラメーター情報

- インテリセンス クイック ヒント

- インテリセンス メンバーの完了

- インテッリセンス語の単語補完

## <a name="partially-supported-features-in-the-mpf"></a>MPF で部分的にサポートされる機能
 MPF は、以下の機能の部分的なサポートのみを提供します。 つまり、MPF によって呼び出されるメソッドを実装する必要があります。

- コードの再フォーマット。 再フォーマットを実装するコードを指定します。

- 有効なコード範囲を識別することによって、ブレークポイントを検証します。 コード範囲を識別するコードを指定します。

- デバッガーの**自動変数を**表示するためのウィンドウをサポートします。 ウィンドウに表示する内容を決定するコードを指定します。

- 型とメンバー間をすばやくナビゲーションするための**ナビゲーション バー**をサポートします。 実装し、**ナビゲーション バー**のコンボ ボックスのリストを設定するヘルパー クラスを返します。

## <a name="implementation"></a>実装
 言語サービス自体と、使用する言語に対応する言語サービス機能を実装するには、いくつかの手順を実行する必要があります。 これらの手順については、次のトピックで説明します。

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
