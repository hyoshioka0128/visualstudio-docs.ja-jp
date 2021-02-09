---
title: サーバーエクスプローラー | の [SharePoint 接続] ノードの拡張Microsoft Docs
titleSuffix: ''
description: Visual Studio の [サーバーエクスプローラー] ウィンドウで [SharePoint 接続] ノードを拡張します。 ノードにカスタムプロパティを追加します。 組み込みノードのデータを取得します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9c10c2bc69086e3c98633ba746c1e6fc8d7f2a20
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889695"
---
# <a name="extend-the-sharepoint-connections-node-in-server-explorer"></a>サーバー エクスプローラーで [SharePoint 接続] ノードを拡張する
  Visual Studio では、[**サーバーエクスプローラー** ] ウィンドウの [ **sharepoint 接続**] ノードを使用して、開発用コンピューターのローカル sharepoint サイトに接続できます。 このノードには、ローカル SharePoint サイトの多くのコンポーネントが階層ツリービューで表示されます。 たとえば、ローカルサイトのリスト、ドキュメントライブラリ、コンテンツの種類を表示できます。 **サーバーエクスプローラー** を使用してローカルの SharePoint サイトに接続する方法の詳細については、「[サーバーエクスプローラーを使用した Sharepoint 接続の参照](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)」を参照してください。

 既存のノードの拡張機能を作成するか、カスタムノードの種類を作成してノードの階層に追加することによって、[ **SharePoint 接続** ] ノードを拡張できます。

## <a name="tasks-for-extending-the-sharepoint-connections-node"></a>SharePoint 接続ノードを拡張するためのタスク
 既存のノードを拡張するには、インターフェイスを実装する Visual Studio 拡張機能を作成し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> ます。 ノードを拡張すると、独自のショートカットメニュー項目やカスタムプロパティなど、ノードに機能を追加できます。 詳細については、「 [方法: サーバーエクスプローラーで SharePoint ノードを拡張](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)する」を参照してください。

 カスタムノード型を作成するには、インターフェイスを実装する Visual Studio 拡張機能を作成し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> ます。 既定で **サーバーエクスプローラー** に表示されていない SharePoint サイトのコンポーネントを表示する場合は、カスタムノードを作成します。 たとえば、 **サーバーエクスプローラー** では既定で SharePoint サイトの Web パーツギャラリーは表示されませんが、これを実行するカスタムノードを追加することはできます。 詳細については、「 [方法: サーバーエクスプローラーにカスタム SharePoint ノードを追加](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md) する」および「 [チュートリアル: サーバーエクスプローラーを拡張して Web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

## <a name="add-custom-properties-to-nodes"></a>ノードへのカスタムプロパティの追加
 ノードを拡張する場合、またはカスタムノード型を作成する場合は、ノードにカスタムプロパティを追加できます。 ノードが選択されると、プロパティが [ **プロパティ** ] ウィンドウに表示されます。

 ノードに追加できるカスタムプロパティには、次の2種類があります。

- SharePoint サイトからの一連の読み取り専用データを表示するプロパティです。 データには、ノードが表す SharePoint コンポーネントが記述されています。 これを行う方法を示すチュートリアルについては、「 [チュートリアル: web パーツを表示するためのサーバーエクスプローラーの拡張](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)」を参照してください。

- カスタムの読み取り/書き込みデータを表示するプロパティ。 これを行う方法を示すコード例については、「 [方法: サーバーエクスプローラーで SharePoint ノードを拡張](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)する」を参照してください。

## <a name="get-data-for-built-in-nodes"></a>組み込みノードのデータを取得する
 Visual Studio に用意されているすべての組み込みノードには、それが表す SharePoint コンポーネントに関するデータが含まれています。 たとえば、SharePoint サイトのリストを表すノードは、リストの既定のビューのタイトルや URL など、リストに関するデータを提供します。

 このデータにアクセスするには、目的のノードを表すオブジェクトのプロパティからデータオブジェクトを取得 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> します。 データオブジェクトの型は、ノードの型によって異なります。

 次のコード例は、リストノードのデータオブジェクトを取得する方法を示しています。 大きな例のコンテキストでこの例を確認するには、「 [方法: サーバーエクスプローラーの組み込み SharePoint ノードのデータを取得](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)する」を参照してください。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#11)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#11](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#11)]

 次の表は、各組み込みノード型のデータオブジェクトの種類を示しています。

|ノードの種類|データオブジェクトの種類|
|---------------|----------------------|
|SharePoint サイトノード|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerSiteNodeInfo>|
|Content type|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IContentTypeNodeInfo>|
|機能|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFeatureNodeInfo>|
|フィールド|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IFieldNodeInfo>|
|List|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListNodeInfo>|
|リストテンプレート|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListTemplateNodeInfo>|
|リストビュー (Microsoft. SharePoint. SPView)|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IListViewNodeInfo>|
|ワークフローの関連付け|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowAssociationNodeInfo>|
|ワークフローテンプレート|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions.IWorkflowTemplateNodeInfo>|

 プロパティの使用方法の詳細については <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 、「 [SharePoint ツールの拡張機能とカスタムデータの関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [方法: サーバーエクスプローラーで SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [方法: サーバーエクスプローラーにカスタム SharePoint ノードを追加する](../sharepoint/how-to-add-a-custom-sharepoint-node-to-server-explorer.md)
- [方法: サーバーエクスプローラーで組み込みの SharePoint ノードのデータを取得する](../sharepoint/how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer.md)
- [カスタムデータと SharePoint ツールの拡張機能の関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [サーバー エクスプローラーを使用して SharePoint 接続を参照する](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
