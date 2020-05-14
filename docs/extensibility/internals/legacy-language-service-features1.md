---
title: レガシー言語サービスの特徴1 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f0be7cb4401792b30eac595faf64162dc375dbb2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707396"
---
# <a name="legacy-language-service-features"></a>従来の言語サービスの特徴
マネージ パッケージ フレームワーク (MPF) 言語サービスは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]構文の強調表示、IntelliSense、ブレークポイントの検証など、1 つ以上の機能をサポートできます。 各機能は他の機能とは独立して実装できますが、構文の強調表示を除いて、すべてパーサーとスキャナが必要です。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 言語ペアの一致 (中かっこの一致とも呼ばれます) をサポートするために必要な内容について説明します。

- [従来の言語サービスのコメント コード](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 選択したコードのコメントとコメント解除をサポートするために必要な内容について説明します。

- [従来の言語サービスのカスタム ドキュメント プロパティ](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 ソース ファイルに埋め込まれているドキュメント プロパティをサポートするために必要な情報について説明します。

- [従来の言語サービスのアウトライン](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 非表示領域の実装を通じてアウトラインをサポートするために必要な内容について説明します。

- [従来の言語サービスの再フォーマット コード](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 コードの再フォーマットをサポートするために必要な内容について説明します。

- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 コード スニペットをサポートするために必要な内容について説明します。

- [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 メソッドの型指定時にメソッド シグネチャを表示するために IntelliSense パラメーター ヒント操作をサポートするために必要な内容について説明します。

- [従来の言語サービスのクイック ヒント](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 識別子に関する情報を表示するために IntelliSense クイック ヒント操作をサポートするために必要な事項について説明します。

- [従来の言語サービスでのメンバー補完](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 一覧から名前空間のメンバーを選択するために IntelliSense メンバーの完了操作をサポートするために必要な内容について説明します。

- [従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 部分的に入力された単語を完了するために IntelliSense 完全な単語操作をサポートするために必要な内容について説明します。

- [従来の言語サービスでの自動変数ウィンドウのサポート](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 デバッグ中に言語サービスが **[自動**変数] ウィンドウをサポートするためにできることについて説明します。

- [従来の言語サービスでのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 エディター ビューの上部にある**ナビゲーション バー**を使用して、そのビューに表示されるファイル内の任意の型またはメンバーにすばやく移動する方法について説明します。

- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 ソース コードの構文の強調表示をサポートするために必要な内容について説明します。

- [従来の言語サービスでのブレークポイントの検証](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 デバッガーの外部でブレークポイントを検証する場合に、言語サービスが実行できる操作について説明します。

## <a name="related-sections"></a>関連項目
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 マネージ パッケージ フレームワークを使用する言語サービスのすべての機能を実装するために必要なパーサーとスキャナーについて説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 MPF を使用して言語サービスを実装するために必要な内容について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

 に MPF ベースの言語サービスを登録するために必要な手順について説明[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。

- [IntelliSense の使用](../../ide/using-intellisense.md)

 IntelliSense が言語参照に簡単にアクセスできるしくみについて説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 マネージ パッケージ フレームワーク (MPF) を使用して、マネージ コードでフル機能の言語サービスを実装する方法について説明します。
