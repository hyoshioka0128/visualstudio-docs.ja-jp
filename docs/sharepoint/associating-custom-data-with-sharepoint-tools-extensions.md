---
title: SharePoint ツールの拡張機能にカスタムデータを関連付ける |Microsoft Docs
description: カスタムデータを SharePoint ツールの拡張機能に関連付けます。 カスタムデータを含めることができるオブジェクトの一覧を表示します。 カスタムデータを追加および取得します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], associating custom data
- project items [SharePoint development in Visual Studio], associating custom data
- SharePoint project items, associating custom data
- SharePoint projects, associating custom data
- SharePoint development in Visual Studio, extensibility features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: db32c05b4a1f4536e71b4ef233758f747a958327
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850404"
---
# <a name="associate-custom-data-with-sharepoint-tools-extensions"></a>カスタムデータと SharePoint ツールの拡張機能の関連付け
  SharePoint ツールの拡張機能では、特定のオブジェクトにカスタムデータを追加できます。 これは、拡張機能の一部に、後で拡張機能の他のコードからアクセスするデータがある場合に便利です。 データを格納してアクセスするための独自の方法を実装する代わりに、拡張機能のオブジェクトにデータを関連付け、後で同じオブジェクトからデータを取得することができます。

 カスタムデータをオブジェクトに追加することは、Visual Studio の特定の項目に関連するデータを保持する場合にも便利です。 SharePoint ツールの拡張機能は Visual Studio に一度だけ読み込まれるため、拡張機能では、プロジェクト、プロジェクト項目、 **サーバーエクスプローラー** ノードなどのさまざまな項目をいつでも使用できます。 特定のアイテムにのみ関連するカスタムデータがある場合は、そのアイテムを表すオブジェクトにデータを追加できます。

 SharePoint ツールの拡張機能のオブジェクトにカスタムデータを追加しても、データは保持されません。 データは、オブジェクトの有効期間中にのみ使用できます。 オブジェクトがガベージコレクションによって回収されると、データは失われます。

 SharePoint プロジェクトシステムの拡張機能では、拡張機能がアンロードされた後に保持される文字列データを保存することもできます。 詳細については、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

## <a name="objects-that-can-contain-custom-data"></a>カスタムデータを含むことができるオブジェクト
 インターフェイスを実装する SharePoint ツールオブジェクトモデル内の任意のオブジェクトに、カスタムデータを追加でき <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> ます。 このインターフェイス <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> は、カスタムデータオブジェクトのコレクションであるプロパティを1つだけ定義します。 次の型はを実装し <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> ます。

- <xref:Microsoft.VisualStudio.SharePoint.IMappedFolder>

- <xref:Microsoft.VisualStudio.SharePoint.IMenuItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectMember>

- <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>

- <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentContext>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeType>

- <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeDefinition>

## <a name="add-and-retrieve-custom-data"></a>カスタムデータの追加と取得
 SharePoint ツールの拡張機能でオブジェクトにカスタムデータを追加するには、 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> データを追加するオブジェクトのプロパティを取得し、メソッドを使用してデータを <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.Add%2A> オブジェクトに追加します。

 SharePoint ツールの拡張機能でオブジェクトからカスタムデータを取得するには、 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> オブジェクトのプロパティを取得して、次のいずれかの方法を使用します。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.TryGetValue%2A>. このメソッドは、データオブジェクトが存在する場合は **true** 、存在しない場合は **false** を返します。 このメソッドを使用すると、値型または参照型のインスタンスを取得できます。

- <xref:Microsoft.VisualStudio.SharePoint.IAnnotationDictionary.GetValue%2A>. このメソッドは、終了した場合はデータオブジェクトを返し、存在しない場合は **null** を返します。 このメソッドは、参照型のインスタンスを取得するためにのみ使用できます。

  次のコード例では、特定のデータオブジェクトが既にプロジェクト項目に関連付けられているかどうかを判断します。 データオブジェクトがまだプロジェクト項目に関連付けられていない場合、コードはプロジェクト項目のプロパティにオブジェクトを追加し <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> ます。 大きな例のコンテキストでこの例を確認するには、「 [方法: カスタム SharePoint プロジェクト項目の種類にプロパティを追加](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)する」を参照してください。

  [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#13)]
  [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#13](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#13)]

## <a name="see-also"></a>関連項目
- [SharePoint ツール拡張機能におけるプログラミングに関する概念および特徴](../sharepoint/programming-concepts-and-features-for-sharepoint-tools-extensions.md)
- [チュートリアル: 項目テンプレートを使用したカスタムアクションプロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: web パーツを表示するためのサーバーエクスプローラーの拡張](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [方法: プロパティをカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
