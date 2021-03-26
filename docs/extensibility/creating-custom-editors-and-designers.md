---
title: カスタムエディターとデザイナーの作成 |Microsoft Docs
description: Visual Studio IDE でホストできるさまざまな種類のエディター (コアエディター、カスタムエディター、外部エディター、およびデザイナー) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c2882cfa103627672e5c96a0e3d4b2a23b4b4ba9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055779"
---
# <a name="create-custom-editors-and-designers"></a>カスタムエディターとデザイナーを作成する

Visual Studio 統合開発環境 (IDE) では、さまざまな種類のエディターをホストできます。

- Visual Studio のコアエディター

- カスタムエディター

- 外部エディター

- デザイナー

次の情報は、必要なエディターの種類を選択するのに役立ちます。

## <a name="types-of-editor"></a>エディターの種類

Visual Studio のコアエディターの詳細については、「 [エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

### <a name="custom-editors"></a>カスタムエディター
 カスタムエディターは、特殊な状況で動作するように設計されています。 たとえば、Microsoft Exchange server などの特定のリポジトリに対してデータの読み取りと書き込みを行う機能を持つエディターを作成できます。 プロジェクトの種類に対してのみ機能するエディターを使用する場合、または特定のコマンドのみを含むエディターが必要な場合は、カスタムエディターを選択します。 ただし、ユーザーはカスタムエディターを使用して標準プロジェクトを編集できないことに注意して [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ください。

 カスタムエディターでは、エディターファクトリを使用して、エディターに関する情報をレジストリに追加できます。 ただし、カスタムエディターに関連付けられているプロジェクトの種類では、他の方法でカスタムエディターをインスタンス化できます。

 カスタムエディターでは、埋め込み先アクティブ化または簡略化された埋め込みを使用して、ビューを実装できます。

### <a name="external-editors"></a>外部エディター
 外部エディターは、Microsoft Word、メモ帳、Microsoft FrontPage など、Visual Studio に統合されていないエディターです。 たとえば、VSPackage からテキストを渡す場合は、このようなエディターを呼び出すことができます。 外部エディターは自身を登録し、Visual Studio の外部で使用できます。 外部エディターを呼び出し、ホストウィンドウに埋め込むことができる場合は、IDE のウィンドウに表示されます。 そうでない場合は、IDE によって別のウィンドウが作成されます。

 メソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> 列挙体を使用してドキュメントの優先順位を設定し <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> ます。 値を指定した場合は、 `DP_External` 外部エディターでファイルを開くことができます。

## <a name="editor-design-decisions"></a>エディターの設計上の決定
 次の設計に関する質問は、アプリケーションに最適なエディターの種類を選択するのに役立ちます。

- アプリケーションのデータはファイルに保存されますか。 データがファイルに保存される場合、そのデータはカスタム形式または標準形式になりますか。

   標準のファイル形式を使用する場合は、プロジェクトに加えて他のプロジェクトの種類を使用して、プロジェクトに対するデータの読み取り/書き込みを行うことができます。 ただし、カスタムファイル形式を使用する場合は、プロジェクトの種類に対してのみ、データを開いて読み取り/書き込みを行うことができます。

   プロジェクトでファイルを使用する場合は、標準エディターをカスタマイズする必要があります。 プロジェクトでファイルを使用せず、データベースまたは他のリポジトリ内の項目を使用する場合は、カスタムエディターを作成する必要があります。

- エディターで ActiveX コントロールをホストする必要がありますか。

   エディターが ActiveX コントロールをホストしている場合は、「インプレース [アクティブ化](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015)」で説明されているように、インプレースアクティブ化エディターを実装します。 ActiveX コントロールをホストしていない場合は、簡略化された埋め込みエディターを使用するか、既定のエディターをカスタマイズし [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。

- エディターは複数のビューをサポートしますか。 エディターのビューを既定のエディターと同時に表示する場合は、複数のビューをサポートする必要があります。

   エディターが複数のビューをサポートする必要がある場合、エディターのドキュメントデータオブジェクトとドキュメントビューオブジェクトは別々のオブジェクトである必要があります。 詳細については、「 [複数のドキュメントビューのサポート](../extensibility/supporting-multiple-document-views.md)」を参照してください。

   エディターが複数のビューをサポートしている場合は、 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ドキュメントデータオブジェクトのコアエディターのテキストバッファーの実装 (オブジェクト) を使用する予定 <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ですか。 つまり、エディタービューをコアエディターとサイドバイサイドでサポートし [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ますか。 これを行う機能は、フォームデザイナーの基礎です。「」を参考にしてください。

- 外部エディターをホストする必要がある場合は、エディターを内部に埋め込むことができ [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ますか。

   これを埋め込むことができる場合は、外部エディター用のホストウィンドウを作成し、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A> メソッドを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> 列挙値をに設定する必要があり `DP_External` ます。 エディターを埋め込むことができない場合は、IDE によって自動的に別のウィンドウが作成されます。

## <a name="in-this-section"></a>このセクションの内容

[チュートリアル: カスタムエディターを作成する](../extensibility/walkthrough-creating-a-custom-editor.md)\
カスタムエディターを作成する方法について説明します。

[チュートリアル: カスタムエディターへの機能の追加](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
カスタムエディターに機能を追加する方法について説明します。

[デザイナーの初期化とメタデータの構成](../extensibility/designer-initialization-and-metadata-configuration.md)\
デザイナーを初期化する方法について説明します。

[デザイナーに取り消しサポートを提供する](../extensibility/supplying-undo-support-to-designers.md)\
デザイナーの取り消しサポートを提供する方法について説明します。

[カスタムエディターでの構文の色分け](../extensibility/syntax-coloring-in-custom-editors.md)\
コアエディターとカスタムエディターの構文の色分けの違いについて説明します。

[カスタムエディターでのドキュメントデータとドキュメントビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)\
カスタムエディターでドキュメントデータとドキュメントビューを実装する方法について説明します。

## <a name="related-sections"></a>関連項目

[エディター内のレガシインターフェイス](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)\
レガシ API を使用してコアエディターにアクセスする方法について説明します。

[従来の言語サービスを開発する](../extensibility/internals/developing-a-legacy-language-service.md)\
言語サービスを実装する方法について説明します。

[Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)\
の残りの部分に一致する UI 要素を作成する方法について説明 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
