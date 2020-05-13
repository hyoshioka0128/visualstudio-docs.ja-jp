---
title: カスタム エディターとデザイナーの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK]
- editors [Visual Studio SDK], custom
ms.assetid: b6a5e8b2-0ae1-4fc3-812d-09d40051b435
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b9f56b82225e1e40782b6753bea03d3c1780f596
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739477"
---
# <a name="create-custom-editors-and-designers"></a>カスタム エディターとデザイナーを作成する

Visual Studio 統合開発環境 (IDE) では、さまざまな種類のエディターをホストできます。

- ビジュアル スタジオのコア エディター

- カスタムエディター

- 外部エディタ

- デザイナー

以下の情報は、必要なエディタの種類を選択する際に役立ちます。

## <a name="types-of-editor"></a>エディタの種類

Visual Studio のコア エディターの詳細については、「[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

### <a name="custom-editors"></a>カスタムエディター
 カスタム エディターは、特殊な状況で動作するように設計されたエディターです。 たとえば、Microsoft Exchange サーバーなどの特定のリポジトリに対してデータを読み書きする機能を持つエディターを作成できます。 プロジェクトタイプのみで動作するエディターを使用する場合、または少数の特定のコマンドしか持つエディターが必要な場合は、カスタムエディターを選択します。 ただし、ユーザーはカスタム エディターを使用して標準[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]プロジェクトを編集することはできません。

 カスタム エディターは、エディター ファクトリを使用して、エディターに関する情報をレジストリに追加できます。 ただし、カスタム エディターに関連付けられているプロジェクトの種類は、他の方法でカスタム エディターをインスタンス化できます。

 カスタム エディターでは、埋め込み場所でのアクティブ化または簡易化の埋め込みを使用してビューを実装できます。

### <a name="external-editors"></a>外部エディタ
 外部エディターは、Word、メモ帳、または Microsoft のフロント ページなどの Visual Studio に統合されていないエディターです。 たとえば、VSPackage からテキストを渡す場合などに、このようなエディターを呼び出す場合があります。 外部エディターは自分自身を登録し、Visual Studio の外部で使用できます。 外部エディタを呼び出し、ホストウィンドウに埋め込むこともできる場合、IDE のウィンドウに表示されます。 それでない場合は、IDE は別のウィンドウを作成します。

 この<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>メソッドは、列挙体を使用して<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>ドキュメントの優先順位を設定します。 値を`DP_External`指定すると、外部エディタでファイルを開くことができます。

## <a name="editor-design-decisions"></a>エディターの設計の決定
 次の設計に関する質問は、アプリケーションに最適なエディターの種類を選択するのに役立ちます。

- アプリケーションはデータをファイルに保存するか、保存しないか。 データをファイルに保存する場合、ユーザー設定または標準形式になりますか?

   標準のファイル形式を使用する場合、プロジェクトに加えて他の種類のプロジェクトでデータを開いたり、データを書き込んだりできるようになります。 ただし、カスタム ファイル形式を使用する場合は、プロジェクトの種類だけがデータを開いて書き込みできます。

   プロジェクトでファイルを使用する場合は、標準エディタをカスタマイズする必要があります。 プロジェクトでファイルを使用せず、データベースや他のリポジトリの項目を使用する場合は、カスタムエディターを作成する必要があります。

- エディタで ActiveX コントロールをホストする必要がありますか?

   エディタが ActiveX コントロールをホストしている場合は、「インプレース アクティベーション」で説明されているように、[インプレース アクティベーション](/visualstudio/misc/in-place-activation?view=vs-2015)エディタを実装します。 ActiveX コントロールをホストしていない場合は、簡略化された埋め込みエディターを使用するか、既定の[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]エディターをカスタマイズします。

- エディターは複数のビューをサポートしますか? エディターのビューを既定のエディターと同時に表示する場合は、複数のビューをサポートする必要があります。

   エディターで複数のビューをサポートする必要がある場合は、エディターのドキュメント データオブジェクトとドキュメント ビュー オブジェクトを個別のオブジェクトにする必要があります。 詳細については、「[複数のドキュメント ビューをサポート](../extensibility/supporting-multiple-document-views.md)する 」を参照してください。

   エディターが複数のビューをサポートしている場合、ドキュメント データ[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]オブジェクトにコア エディターのテキスト<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>バッファー実装 (オブジェクト) を使用する予定ですか。 つまり、コア エディターと並べてエディター ビューを[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]サポートしますか? これを行う機能は、フォーム デザイナの基礎となります。

- 外部エディタ をホストする必要がある場合、エディタを 内部[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]に埋め込むことができますか?

   埋め込み可能な場合は、外部エディタのホスト ウィンドウを作成し、メソッド<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.IsDocumentInProject%2A>を呼び出<xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>して列挙値`DP_External`を に設定する必要があります。 エディターを埋め込めない場合、IDE は自動的に別のウィンドウを作成します。

## <a name="in-this-section"></a>このセクションの内容

[チュートリアル: カスタム エディターを作成する](../extensibility/walkthrough-creating-a-custom-editor.md)\
カスタム エディターを作成する方法について説明します。

[チュートリアル: カスタム エディターに機能を追加する](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)\
カスタム エディターに機能を追加する方法について説明します。

[デザイナーの初期化とメタデータの構成](../extensibility/designer-initialization-and-metadata-configuration.md)\
デザイナーを初期化する方法について説明します。

[デザイナに元に戻すサポートを提供する](../extensibility/supplying-undo-support-to-designers.md)\
デザイナーに元に戻すサポートを提供する方法について説明します。

[カスタム エディターでの構文の色分け](../extensibility/syntax-coloring-in-custom-editors.md)\
コア エディターとカスタム エディターでの構文の色の違いについて説明します。

[カスタム エディターでのドキュメント データとドキュメント ビュー](../extensibility/document-data-and-document-view-in-custom-editors.md)\
カスタム エディターでドキュメント データとドキュメント ビューを実装する方法について説明します。

## <a name="related-sections"></a>関連項目

[エディタのレガシーインターフェイス](/visualstudio/extensibility/legacy-interfaces-in-the-editor?view=vs-2015)\
従来の API を使用してコア エディターにアクセスする方法について説明します。

[従来の言語サービスの開発](../extensibility/internals/developing-a-legacy-language-service.md)\
言語サービスを実装する方法について説明します。

[ビジュアル スタジオの他の部分を拡張します。](../extensibility/extending-other-parts-of-visual-studio.md)\
の他の部分と一致する UI[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]要素を作成する方法について説明します。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>
