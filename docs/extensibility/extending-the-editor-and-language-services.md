---
title: エディタと言語サービスの拡張 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 239c638ec32cc0dc2b2e275a5dbe0c4213a3423e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711712"
---
# <a name="extend-the-editor-and-language-services"></a>エディタと言語サービスを拡張する
言語サービス機能 (IntelliSense など) を独自のエディターに追加し、Visual Studio コード エディターのほとんどの機能を拡張できます。  拡張できる内容の完全なリストについては、[言語サービスとエディター拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)を参照してください。

 マネージ機能拡張フレームワーク (MEF) を使用して、ほとんどのエディター機能を拡張します。 たとえば、拡張するエディター機能が構文の色分けである場合、異なる色分けの分類とそれらを処理する方法を定義する MEF*コンポーネント部分*を記述できます。 エディタは、同じ機能の複数の拡張機能もサポートしています。

 エディター プレゼンテーション層は、Windows プレゼンテーション フレームワーク (WPF) に基づいています。 WPFWPF は、柔軟なテキスト書式設定用のグラフィックス ライブラリを提供し、グラフィックスやアニメーションなどの視覚エフェクトも提供します。

 Visual Studio SDK には、以前のバージョン用に作成された VSPackage をサポートする*shim*と呼ばれるアダプターが用意されています。 VSPackage が既に存在する場合は、パフォーマンスと信頼性を向上させるために新しいテクノロジに更新することをお勧めします。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[言語サービスとエディター拡張機能の概要](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|エディターの拡張機能を作成する方法について説明します。|
|[エディタ内](../extensibility/inside-the-editor.md)|エディタの一般的な構造を説明し、その機能の一部を一覧表示します。|
|[エディターでのマネージ機能拡張フレームワーク](../extensibility/managed-extensibility-framework-in-the-editor.md)|エディターでマネージ機能拡張フレームワーク (MEF) を使用する方法について説明します。|
|[言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)|エディタの拡張ポイントを一覧表示します。 拡張ポイントは、拡張可能なエディター機能を表します。|
|[チュートリアル: ビューの表示要素、コマンド、および設定を作成する (列ガイド)](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|コードを特定の表示幅に保つために、列のガイドラインを描画するビュー表示要素の構築について説明します。  また、読み取りと書き込みの設定、コマンド ウィンドウから呼び出すことができるコマンドの宣言と実装も示します。|
|[エディターのインポート](../extensibility/editor-imports.md)|拡張機能がインポートできるサービスの一覧が表示されます。|
|[レガシ コードをエディターに適用する](/visualstudio/extensibility/adapting-legacy-code-to-the-editor?view=vs-2015)|従来のコード (Visual Studio 2010 より前) を変更してエディターを拡張するさまざまな方法について説明します。|
|[従来の言語サービスを移行する](../extensibility/internals/migrating-a-legacy-language-service.md)|VSPackage ベースの言語サービスを移行する方法について説明します。|
|[チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|コンテンツ タイプをファイル名拡張子にリンクする方法について説明します。|
|[チュートリアル: 余白グリフを作成する](../extensibility/walkthrough-creating-a-margin-glyph.md)|余白にアイコンを追加する方法を示します。|
|[チュートリアル: テキストを強調表示する](../extensibility/walkthrough-highlighting-text.md)|*タグ*を使用してテキストを強調表示する方法について説明します。|
|[チュートリアル: アウトラインの追加](../extensibility/walkthrough-outlining.md)|特定の種類の中かっこのアウトラインを追加する方法について説明します。|
|[チュートリアル: 一致する中かっこを表示する](../extensibility/walkthrough-displaying-matching-braces.md)|一致する中かっこを強調表示する方法を示します。|
|[チュートリアル: クイック ヒントヒントを表示する](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|プロパティ、メソッド、イベントなどのコード要素を記述する QuickInfo ポップアップを表示する方法について説明します。|
|[チュートリアル: 署名ヘルプを表示する](../extensibility/walkthrough-displaying-signature-help.md)|署名のパラメーターの数と種類に関する情報を提供するポップアップを表示する方法について説明します。|
|[チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)|ステートメント入力候補を実装する方法を示します。|
|[チュートリアル: コード スニペットを実装する](../extensibility/walkthrough-implementing-code-snippets.md)|コード スニペットの展開を実装する方法を示します。|
|[チュートリアル: 電球候補を表示する](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|コード候補の電球を表示する方法を示します。|
|[チュートリアル: エディター拡張機能でシェル コマンドを使用する](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|VSPackage のメニュー コマンドを MEF コンポーネントに関連付ける方法について説明します。|
|[チュートリアル: エディター拡張機能でショートカット キーを使用する](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|VSPackage のメニュー ショートカットを MEF コンポーネントに関連付ける方法について説明します。|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|マネージ機能拡張フレームワーク (MEF) に関する情報を提供します。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Windows プレゼンテーション ファウンデーション (WPF) に関する情報を提供します。|

## <a name="reference"></a>リファレンス
 Visual Studio エディターには、次の名前空間が含まれています。

 <xref:Microsoft.VisualStudio.Language.Intellisense>

 <xref:Microsoft.VisualStudio.Language.StandardClassification>

 <xref:Microsoft.VisualStudio.Editor>

 <xref:Microsoft.VisualStudio.Text>

 <xref:Microsoft.VisualStudio.Text.Adornments>

 <xref:Microsoft.VisualStudio.Text.Classification>

 <xref:Microsoft.VisualStudio.Text.Differencing>

 <xref:Microsoft.VisualStudio.Text.Document>

 <xref:Microsoft.VisualStudio.Text.Editor>

 <xref:Microsoft.VisualStudio.Text.Editor.OptionsExtensionMethods>

 <xref:Microsoft.VisualStudio.Text.Formatting>

 <xref:Microsoft.VisualStudio.Text.IncrementalSearch>

 <xref:Microsoft.VisualStudio.Text.Operations>

 <xref:Microsoft.VisualStudio.Text.Outlining>

 <xref:Microsoft.VisualStudio.Text.Projection>

 <xref:Microsoft.VisualStudio.Text.Tagging>

 <xref:Microsoft.VisualStudio.Utilities>
