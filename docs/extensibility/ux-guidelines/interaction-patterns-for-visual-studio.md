---
title: ビジュアルスタジオのインタラクションパターン |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a3643792-b0df-481c-bc35-576f948e04cf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ac917aeb2530570b755e7f1e6fc6de00714a54b0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698372"
---
# <a name="interaction-patterns-for-visual-studio"></a>Visual Studio のインタラクション パターン
## <a name="overview"></a>概要
 設計パターンは、一般に、特定の状況で適用して、類似した制約のセットを使用して問題を解決できる設計の中核です。 機能設計者とシステム設計者は、これらの設計パターンを出発点として使用し、その設計パターンを特定の状況に適応させることができます。

 Visual Studio には、新しい機能を構築するときに考慮する必要がある一般的な相互作用パターンのライブラリがあります。 デザイン パターンには、Visual Studio クライアント (devenv) と Visual Studio オンラインという 2 つの主要なコンテキストがあります。 設計上の問題の中には、あらゆる状況でうまく機能するユビキタスパターンがあります。 ただし、多くの場合、ソリューションは、ブラウザー内で表示される UI とクライアント アプリケーションでホストされている UI で異なる場合があります。

### <a name="visual-studio-client-pattern-types"></a>ビジュアル スタジオ クライアント パターンの種類

|パターンタイプ|説明|使用例|
|------------------|-----------------|--------------|
|**アプリケーション レベルのパターン**|アプリケーションに共通する高レベルパターン、アプリケーションコンテキストの決定または表示、およびアプリケーション内の複合パターンと制御パターンの含み|- ツールウィンドウ<br />- ドキュメントウィンドウ|
|**複合パターン**|アプリケーション パターン間で使用される共通パターン、または異なる構成の複数のコントロールで構成された認識パターン|- 切り替えを表示<br />- リストビルダー<br />- データの表示<br />- 通知<br />- 検証<br />- 選択モデル|
|**コントロールパターン**|低レベルコントロールの動作に関する詳細|- ツリービュー<br />- グリッド コントロール内での編集|

## <a name="application-patterns"></a>アプリケーション パターン
 大まかに言えば、Visual Studio インターフェイスは、1 つの IDE 内で複数のウィンドウ、ダイアログ、コマンド、およびツール バーで構成されます。 Visual Studio 階層は、コンテキストとドライブのメニューを決定します。 IDE のユーザー インターフェイスの主要な統合ポイントは、ドキュメント ウィンドウ、ツール ウィンドウ、プロジェクト、コマンド構造、テキスト エディター、ツールボックス、プロパティ ウィンドウ、およびツール > オプションです。

 IDE のユーザーインターフェイスの各主要な統合ポイントの基本的な使用パターンがあります。

- [Visual Studio のメニューとコマンド](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)

- [Visual Studio のアプリケーション パターン](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)

  - [ウィンドウの相互作用](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_WindowInteractions)

  - [ツール ウィンドウ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_ToolWindows)

  - [ドキュメント エディタの規則](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_DocumentEditorConventions)

  - [ダイアログ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)

  - [プロジェクト](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Projects)

## <a name="common-control-patterns"></a>共通の制御パターン
 制御パターンは、主に個々のコントロールがどのように動作するかを示します。 これは、一貫性が最も重要な領域の 1 つです。

 Visual Studio の一般的なコントロールの大半は、デスクトップ ウィンドウのガイドラインに従う必要があります。 ガイドラインには、Visual Studio 固有の相互作用で一般的な規則を強化する必要がある領域、または高度なユーザーのニーズに合わせて Visual Studio を調整するためにガイドラインを完全に置き換える領域のみが含まれます。

- [Visual Studio の コモン コントロール パターン](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md)

  - [コモン コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CommonControls)

  - [テキスト コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

  - [ボタンとハイパーリンク](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

## <a name="composite-patterns"></a>複合パターン
 ユーザーがタスクを実行する方法はいくつかあります。 可能な限り、機能は、対話とビジュアル デザインの両方にこれらのパターンを使用するように設計する必要があります。

 Visual Studio には多くの複合パターンがありますが、一貫性に関して最も重要なものは次のとおりです。

- [Visual Studio の複合パターン](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md)

  - [オブジェクト上の UI とピーク](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_OnObjectUI)

  - [選択モデル](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_SelectionModels)

  - [永続性と保存の設定](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_PersistenceAndSavingSettings)

  - [タッチ入力](../../extensibility/ux-guidelines/composite-patterns-for-visual-studio.md#BKMK_TouchInput)
