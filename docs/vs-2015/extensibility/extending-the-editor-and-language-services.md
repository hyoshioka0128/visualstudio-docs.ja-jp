---
title: エディターと言語サービスの拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new -
ms.assetid: 8d04f8db-eda7-4b3e-b6eb-c06df104502a
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 085e1b5c1fbfbbaf5649966738f2864e0b72ed35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65674782"
---
# <a name="extending-the-editor-and-language-services"></a>エディターと言語サービスの拡張
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

独自のエディターに言語サービス機能 (IntelliSense など) を追加し、Visual Studio コードエディターのほとんどの機能を拡張することができます。  拡張できるものの完全な一覧については、「 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)」を参照してください。  
  
 ほとんどのエディター機能は、Managed Extensibility Framework (MEF) を使用して拡張します。 たとえば、拡張するエディター機能が構文の色分けになっている場合は、異なる色の色分けを必要とする分類とその処理方法を定義する MEF *コンポーネントのパート* を記述できます。 エディターでは、同じ機能の複数の拡張機能もサポートされています。  
  
 エディタープレゼンテーションレイヤーは、Windows Presentation Framework (WPF) に基づいています。 WPF には柔軟なテキスト書式設定用のグラフィックスライブラリが用意されています。また、グラフィックスやアニメーションなどの視覚エフェクトも用意されています。  
  
 Visual Studio SDK には、以前のバージョン用に記述された Vspackage をサポートするための *shim* と呼ばれるアダプターが用意されています。 ただし、既存の VSPackage がある場合は、パフォーマンスと信頼性を向上させるために、新しいテクノロジに更新することをお勧めします。  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[言語サービスとエディターの拡張機能の概要](../extensibility/getting-started-with-language-service-and-editor-extensions.md)|エディターの拡張機能を作成する方法について説明します。|  
|[エディターの内部](../extensibility/inside-the-editor.md)|エディターの一般的な構造について説明し、その機能の一部を示します。|  
|[エディター内の Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)|エディターで Managed Extensibility Framework (MEF) を使用する方法について説明します。|  
|[言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)|エディターの拡張点を一覧表示します。 拡張ポイントは、拡張可能なエディター機能を表します。|  
|[チュートリアル: ビューの表示要素、コマンド、設定 (垂直グリッド ガイド) の作成](../extensibility/walkthrough-creating-a-view-adornment-commands-and-settings-column-guides.md)|コードを特定の表示幅に維持できるように、列 gudie 描画するビューの表示要素を構築する方法と説明を示します。  また、設定の読み取りと書き込みに加え、コマンドウィンドウから呼び出すことができるコマンドの宣言と実装についても説明します。|  
|[エディターのインポート](../extensibility/editor-imports.md)|拡張機能がインポートできるサービスを一覧表示します。|  
|[レガシ コードをエディターに適合させる](../extensibility/adapting-legacy-code-to-the-editor.md)|従来のコードを調整するためのさまざまな方法について説明します (Visual Studio 2010 より前)。|  
|[従来の言語サービスの移行](../extensibility/internals/migrating-a-legacy-language-service.md)|VSPackage ベースの言語サービスを移行する方法について説明します。|  
|[チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)|コンテンツタイプをファイル名拡張子にリンクする方法について説明します。|  
|[チュートリアル: 余白のグリフの作成](../extensibility/walkthrough-creating-a-margin-glyph.md)|余白にアイコンを追加する方法について説明します。|  
|[チュートリアル: テキストの強調表示](../extensibility/walkthrough-highlighting-text.md)|*タグ*を使用してテキストを強調表示する方法について説明します。|  
|[チュートリアル: アウトライン](../extensibility/walkthrough-outlining.md)|特定の種類の中かっこのアウトラインを追加する方法について説明します。|  
|[チュートリアル: 対応するかっこの表示](../extensibility/walkthrough-displaying-matching-braces.md)|一致する中かっこを強調表示する方法について説明します。|  
|[チュートリアル: クイック ヒントの表示](../extensibility/walkthrough-displaying-quickinfo-tooltips.md)|プロパティ、メソッド、イベントなどのコードの要素を記述する QuickInfo ポップアップを表示する方法について説明します。|  
|[チュートリアル: シグネチャ ヘルプの表示](../extensibility/walkthrough-displaying-signature-help.md)|署名のパラメーターの数と型に関する情報を提供するポップアップを表示する方法について説明します。|  
|[チュートリアル: 入力候補の表示](../extensibility/walkthrough-displaying-statement-completion.md)|ステートメント入力候補を実装する方法について説明します。|  
|[チュートリアル: コード スニペットの実装](../extensibility/walkthrough-implementing-code-snippets.md)|コードスニペットの拡張を実装する方法について説明します。|  
|[チュートリアル: 電球アイコンによる提案の表示](../extensibility/walkthrough-displaying-light-bulb-suggestions.md)|コード候補の電球を表示する方法について説明します。|  
|[チュートリアル: エディター拡張機能でシェル コマンドを使用する](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)|VSPackage のメニューコマンドを MEF コンポーネントに関連付ける方法について説明します。|  
|[チュートリアル: エディター拡張機能でショートカット キーを使用する](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)|VSPackage のメニューショートカットを MEF コンポーネントに関連付ける方法について説明します。|  
|[MEF (Managed Extensibility Framework)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)|Managed Extensibility Framework (MEF) に関する情報を提供します。|  
|[Windows Presentation Foundation](https://msdn.microsoft.com/library/f667bd15-2134-41e9-b4af-5ced6fafab5d)|Windows Presentation Foundation (WPF) に関する情報を提供します。|  
  
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
