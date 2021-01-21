---
title: Visual Studio の相互作用パターン |Microsoft Docs
description: Visual Studio の新機能をビルドするときに使用できる、一般的な相互作用パターンのライブラリについて説明します。
ms.custom: SEO-VS-2020
ms.date: 05/13/2020
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1cd618b66eed900c2436704d40de5325c1205e85
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863493"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio のインタラクション パターン
## <a name="overview"></a>概要
 デザインパターンは、一般的には、特定の状況で適用して、同様の制約のセットに関する問題を解決できる設計の中核となります。 フィーチャーデザイナーとシステムデザイナーは、これらのデザインパターンを開始点として使用します。これは、特定の状況に合わせて調整できます。

 Visual Studio には、新しい機能を構築するときに考慮する必要がある一般的な相互作用パターンのライブラリが用意されています。 デザインパターンには、Visual Studio クライアント (devenv) と GitHub Codespaces (以前の Visual Studio Online) という2つのコアコンテキストがあります。 設計上の問題の中には、すべての状況に適したユビキタスパターンがあります。 ただし、多くの場合、このソリューションは、ブラウザー内に表示され、クライアントアプリケーションでホストされている UI では異なる場合があります。

### <a name="visual-studio-client-pattern-types"></a>Visual Studio クライアントのパターンの種類

|パターンの種類|説明|例|
|------------------|-----------------|--------------|
|**アプリケーションレベルのパターン**|アプリケーションに共通する高度なパターン、アプリケーションコンテキストの決定と表示、およびその中の複合およびコントロールパターンの格納|-ツールウィンドウ<br />-ドキュメントウィンドウ|
|**複合パターン**|複数のアプリケーションパターンにわたる一般的なパターン、または個別の構成で複数のコントロールで構成される認識されるパターン|-ビューの切り替え<br />-リストビルダー<br />-データを表示しています<br />-通知<br />-検証<br />-選択モデル|
|**コントロールパターン**|低レベルのコントロールの動作についての詳細|-ツリービュー<br />-Grid コントロール内での編集|

## <a name="application-patterns"></a>アプリケーション パターン
 大まかに言えば、Visual Studio のインターフェイスは、1つの IDE 内の複数のウィンドウ、ダイアログ、コマンド、およびツールバーで構成されています。 Visual Studio 階層によって、コンテキストメニューとドライブメニューが決まります。 IDE のユーザーインターフェイスの重要な統合ポイントは、ドキュメントウィンドウ、ツールウィンドウ、プロジェクト、コマンドの構造、テキストエディター、ツールボックス、プロパティウィンドウ、およびツール > オプションです。

 IDE のユーザーインターフェイスの各主な統合ポイントには基本的な使用パターンがあります。

- [Visual Studio のメニューとコマンド](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio のアプリケーション パターン](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [ウィンドウの相互作用](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [ツールウィンドウ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [ドキュメントエディターの規則](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [ダイアログ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [プロジェクト](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>コモンコントロールパターン
 コントロールパターンは、主に個々のコントロールがどのように動作するかを示します。 これは、一貫性が最も重要な1つの領域です。

 Visual Studio の最も一般的なコントロールは、デスクトップの Windows ガイドラインに従う必要があります。 このガイドラインに含まれるのは、Visual Studio 固有の対話で共通の規則を強化する必要がある場合、または高度なユーザーのニーズに合わせて Visual Studio を調整するためにガイドラインを完全に置き換える場所だけです。

- [Visual Studio の コモン コントロール パターン](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [コモン コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [テキスト コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [ボタンとハイパーリンク](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>複合パターン
 ユーザーは、さまざまな方法でタスクを実行することを想定しています。 可能な限り、これらのパターンを相互作用とビジュアルデザインの両方に使用するように機能を設計する必要があります。

 Visual Studio 内には多くの複合パターンがありますが、一貫性に関して最も重要なものは次のとおりです。

- [Visual Studio の複合パターン](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [オブジェクト内の UI とピーク](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [選択モデル](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [永続化と設定の保存](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [タッチ入力](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
