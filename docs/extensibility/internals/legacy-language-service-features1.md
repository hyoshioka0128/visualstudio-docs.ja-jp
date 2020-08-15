---
title: 従来の言語サービス Features1 |Microsoft Docs
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
ms.openlocfilehash: c1f2a4010529d3d9727ceb76d6a34f2cbc41b959
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238492"
---
# <a name="legacy-language-service-features-1"></a>従来の言語サービス機能1
Managed package framework (MPF) 言語サービスでは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 構文の強調表示、IntelliSense、ブレークポイントの検証など、1つまたは複数の機能をサポートできます。 各機能を他の機能とは別に実装することもできますが、構文の強調表示を除き、スキャナーだけを必要とするパーサーとスキャナーが必要です。

## <a name="in-this-section"></a>このセクションの内容
- [従来の言語サービスでのかっこの一致](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 言語ペアの一致をサポートするために必要なものについて説明します。これは、かっこの照合とも呼ばれます。

- [従来の言語サービスのコメント コード](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 選択したコードのコメントとコメント解除をサポートするために必要なものについて説明します。

- [従来の言語サービスのカスタム ドキュメント プロパティ](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 ソースファイルに埋め込まれているドキュメントプロパティをサポートするために必要なものについて説明します。

- [従来の言語サービスのアウトライン](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 非表示領域の実装によってアウトラインをサポートするために必要なものについて説明します。

- [従来の言語サービスの再フォーマット コード](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 コードの再フォーマットをサポートするために必要なものについて説明します。

- [従来の言語サービスでのコード スニペットのサポート](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 コードスニペットをサポートするために必要なものについて説明します。コードスニペットは、挿入されて編集できるコードのセグメントです。

- [従来の言語サービスのパラメーター ヒント](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 メソッドが型指定されたときに、メソッドシグネチャを表示するための IntelliSense パラメーターヒント操作をサポートするために必要な事項について説明します。

- [従来の言語サービスのクイック ヒント](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 IntelliSense のクイックヒント操作をサポートして、識別子に関する情報を表示するために必要なものについて説明します。

- [従来の言語サービスでのメンバー補完](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 リストから名前空間のメンバーを選択するために IntelliSense メンバーの完了操作をサポートするために必要な事項について説明します。

- [従来の言語サービスでの単語補完](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 部分的に入力された単語を完了するために IntelliSense の入力候補操作をサポートするために必要なものについて説明します。

- [従来の言語サービスでの自動変数ウィンドウのサポート](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 デバッグ中に言語サービスが [ **自動変数** ] ウィンドウをサポートするために実行できる操作について説明します。

- [従来の言語サービスでのナビゲーション バーのサポート](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 エディタービューの上部にある **ナビゲーションバー** を使用して、そのビューに表示されるファイル内の任意の型またはメンバーにすばやく移動できるようにする方法について説明します。「」を参照してください。

- [従来の言語サービスでの構文の配色変更](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 ソースコードの構文の強調表示をサポートするために必要な事項について説明します。

- [従来の言語サービスでのブレークポイントの検証](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 デバッガーの外部でのブレークポイントの検証をサポートするために言語サービスが実行できることについて説明します。

## <a name="related-sections"></a>関連項目
- [従来の言語サービスのパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 マネージパッケージフレームワークを使用する言語サービスのすべての機能を実装するために必要なパーサーとスキャナーについて説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 MPF を使用して言語サービスを実装するために必要な事項について説明します。

- [従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)

 MPF ベースの言語サービスをに登録するために必要な手順について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [IntelliSense の使用](../../ide/using-intellisense.md)

 IntelliSense によって言語参照が簡単にアクセスできるようにする方法について説明します。

- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 Managed package framework (MPF) を使用して、完全な機能を備えた言語サービスをマネージコードで実装する方法について説明します。
