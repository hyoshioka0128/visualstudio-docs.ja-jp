---
title: '方法: SharePoint プロジェクトサービスを取得する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f49883337c5748c0f8bcab5d0a88e02612e51b4c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015555"
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>方法: SharePoint プロジェクトサービスを取得する
  SharePoint プロジェクトサービスには、次の種類のソリューションでアクセスできます。

- SharePoint プロジェクトシステムの拡張機能 (プロジェクトの拡張機能、プロジェクト項目の拡張機能、プロジェクト項目の種類の定義など)。 これらの種類の拡張機能の詳細については、「 [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

- **サーバーエクスプローラー**の**SharePoint 接続**ノードの拡張機能。 これらの種類の拡張機能の詳細については、 [サーバーエクスプローラーの「SharePoint 接続ノードの拡張](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

- 別の種類の Visual Studio 拡張機能 (VSPackage など)。

## <a name="retrieve-the-service-in-project-system-extensions"></a>プロジェクトシステムの拡張機能でサービスを取得する
 SharePoint プロジェクトシステムの拡張機能では、オブジェクトのプロパティを使用してプロジェクトサービスにアクセスでき <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> ます。

 次の手順を使用して、プロジェクトサービスを取得することもできます。

#### <a name="to-retrieve-the-service-in-a-project-extension"></a>プロジェクト拡張機能でサービスを取得するには

1. インターフェイスの実装で、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> メソッドを見つけ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> ます。

2. サービスにアクセスするには、 *projectservice* パラメーターを使用します。

     次のコード例では、プロジェクトサービスを使用して、単純なプロジェクト拡張機能で [ **出力** ] ウィンドウおよび **エラー一覧** ウィンドウにメッセージを書き込む方法を示します。

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#1)]

     プロジェクト拡張機能の作成の詳細については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。

#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>プロジェクト項目の拡張機能でサービスを取得するには

1. インターフェイスの実装で、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> メソッドを見つけ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> ます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> *ProjectItemType*パラメーターのプロパティを使用して、サービスを取得します。

     次のコード例では、project service を使用して、[**出力**] ウィンドウにメッセージを書き込み、**リスト定義**プロジェクト項目の単純な拡張機能に**エラー一覧**ウィンドウにメッセージを書き込む方法を示します。

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#2)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#2)]

     プロジェクト項目の拡張機能の作成の詳細については、「 [方法: SharePoint プロジェクト項目の拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)する」を参照してください。

#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>プロジェクト項目の種類の定義でサービスを取得するには

1. インターフェイスの実装で、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> メソッドを見つけ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> ます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> *Typedefinition*パラメーターのプロパティを使用して、サービスを取得します。

     次のコード例では、プロジェクトサービスを使用して、単純なプロジェクト項目の種類の定義で [ **出力** ] ウィンドウと [ **エラー一覧** ] ウィンドウにメッセージを書き込む方法を示します。

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#3)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#3)]

     プロジェクト項目の種類の定義の詳細については、「 [方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。

## <a name="retrieve-the-service-in-server-explorer-extensions"></a>サーバーエクスプローラー拡張機能でサービスを取得する
 **サーバーエクスプローラー**の [ **SharePoint 接続**] ノードの拡張機能では、オブジェクトのプロパティを使用してプロジェクトサービスにアクセスでき <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> ます。

#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>サーバーエクスプローラー拡張機能でサービスを取得するには

1. <xref:System.IServiceProvider> <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> 拡張機能内のオブジェクトのプロパティからオブジェクトを取得 <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> します。

2. <xref:System.IServiceProvider.GetService%2A>オブジェクトを要求するには、メソッドを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> ます。

     次のコード例では、プロジェクトサービスを使用して、[**出力**] ウィンドウにメッセージを書き込む方法と、拡張機能によって**サーバーエクスプローラー**の一覧ノードに追加されるショートカットメニューから [**エラー一覧**] ウィンドウにメッセージを書き込む方法を示します。

     [!code-vb[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs#1)]

     **サーバーエクスプローラー**の [ **sharepoint 接続**] ノードの拡張の詳細については、「[方法: サーバーエクスプローラーで sharepoint ノードを拡張](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)する」を参照してください。

## <a name="retrieve-the-service-in-other-visual-studio-extensions"></a>他の Visual Studio 拡張機能でサービスを取得する
 プロジェクトサービスは、VSPackage、または <xref:EnvDTE80.DTE2> インターフェイスを実装するプロジェクトテンプレートウィザードなど、オートメーションオブジェクトモデルのオブジェクトにアクセスできる任意の Visual Studio 拡張機能で取得でき <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> ます。

 VSPackage では、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 次のいずれかの方法を使用してオブジェクトを要求できます。

- <xref:System.IServiceProvider.GetService%2A>クラスから派生したマネージ VSPackage のメソッド <xref:Microsoft.VisualStudio.Shell.Package> 。 詳細については、「 [方法: サービスを取得](../extensibility/how-to-get-a-service.md)する」を参照してください。

- 静的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッド。 詳細については、「 [GetGlobalService の使用](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice)」を参照してください。

  オブジェクトへのアクセス権を持つ Visual Studio 拡張機能では、オブジェクト <xref:EnvDTE80.DTE2> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> のメソッドを使用してオブジェクトを要求でき <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> <xref:Microsoft.VisualStudio.Shell.ServiceProvider> ます。 詳細については、「 [DTE オブジェクトからのサービスの取得](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
- [方法: サービスを取得する](../extensibility/how-to-get-a-service.md)
- [方法: プロジェクトテンプレートでウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)
