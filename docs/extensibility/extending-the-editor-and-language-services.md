---
title: エディターと言語サービスの拡張 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80711712"
---
# <a name="extend-the-editor-and-language-services"></a>エディターと言語サービスの拡張
独自のエディターに言語サービス機能 (IntelliSense など) を追加し、Visual Studio コードエディターのほとんどの機能を拡張することができます。  拡張できるものの完全な一覧については、「 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)」を参照してください。

 ほとんどのエディター機能は、Managed Extensibility Framework (MEF) を使用して拡張します。 たとえば、拡張するエディター機能が構文の色分けになっている場合は、異なる色の色分けを必要とする分類とその処理方法を定義する MEF *コンポーネントのパート* を記述できます。 エディターでは、同じ機能の複数の拡張機能もサポートされています。

 エディタープレゼンテーションレイヤーは、Windows Presentation Framework (WPF) に基づいています。 WPF には柔軟なテキスト書式設定用のグラフィックスライブラリが用意されています。また、グラフィックスやアニメーションなどの視覚エフェクトも用意されています。

 Visual Studio SDK には、以前のバージョン用に記述された Vspackage をサポートするための *shim* と呼ばれるアダプターが用意されています。 ただし、既存の VSPackage がある場合は、パフォーマンスと信頼性を向上させるために、新しいテクノロジに更新することをお勧めします。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[言語サービスとエディターの拡張機能を使ってみる](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|エディターの拡張機能を作成する方法について説明します。|
|[エディター内](../extensibility/inside-the-editor.md)|エディターの一般的な構造について説明し、その機能の一部を示します。|
|[エディターでの Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)|エディターで Managed Extensibility Framework (MEF) を使用する方法について説明します。|
|[言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)|エディターの拡張点を一覧表示します。 拡張ポイントは、拡張可能なエディター機能を表します。|
|[チュートリアル: ビューの表示要素、コマンド、および設定の作成 (列ガイド)](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|コードを特定の表示幅に維持できるように、列ガイドの線を描画するビューの表示項目の構築について説明します。  また、設定の読み取りと書き込みに加え、コマンドウィンドウから呼び出すことができるコマンドの宣言と実装についても説明します。|
|[エディターのインポート](../extensibility/editor-imports.md)|拡張機能がインポートできるサービスを一覧表示します。|
|[従来のコードをエディターに適応させる](/visualstudio/extensibility/adapting-legacy-code-to-the-editor?view=vs-2015)|従来のコードを調整するためのさまざまな方法について説明します (Visual Studio 2010 より前)。|
|[従来の言語サービスを移行する](../extensibility/internals/migrating-a-legacy-language-service.md)|VSPackage ベースの言語サービスを移行する方法について説明します。|
|[チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|コンテンツタイプをファイル名拡張子にリンクする方法について説明します。|
|[チュートリアル: 余白のグリフの作成](../extensibility/walkthrough-creating-a-margin-glyph.md)|余白にアイコンを追加する方法について説明します。|
|[チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)|*タグ*を使用してテキストを強調表示する方法について説明します。|
|[チュートリアル: アウトラインの追加](../extensibility/walkthrough-outlining.md)|特定の種類の中かっこのアウトラインを追加する方法について説明します。|
|[チュートリアル: 一致する中かっこの表示](../extensibility/walkthrough-displaying-matching-braces.md)|一致する中かっこを強調表示する方法について説明します。|
|[チュートリアル: QuickInfo ツールヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|プロパティ、メソッド、イベントなどのコードの要素を記述する QuickInfo ポップアップを表示する方法について説明します。|
|[チュートリアル: 署名のヘルプを表示する](../extensibility/walkthrough-displaying-signature-help.md)|署名のパラメーターの数と型に関する情報を提供するポップアップを表示する方法について説明します。|
|[チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)|ステートメント入力候補を実装する方法について説明します。|
|[チュートリアル: コードスニペットの実装](../extensibility/walkthrough-implementing-code-snippets.md)|コードスニペットの拡張を実装する方法について説明します。|
|[チュートリアル: 電球の提案を表示する](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|コード候補の電球を表示する方法について説明します。|
|[チュートリアル: エディター拡張機能でシェルコマンドを使用する](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|VSPackage のメニューコマンドを MEF コンポーネントに関連付ける方法について説明します。|
|[チュートリアル: エディター拡張機能でのショートカットキーの使用](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|VSPackage のメニューショートカットを MEF コンポーネントに関連付ける方法について説明します。|
|[MEF (Managed Extensibility Framework)](/dotnet/framework/mef/index)|Managed Extensibility Framework (MEF) に関する情報を提供します。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|Windows Presentation Foundation (WPF) に関する情報を提供します。|

## <a name="reference"></a>関連項目
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
