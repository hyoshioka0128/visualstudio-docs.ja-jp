---
title: '変換: SharePoint プロジェクトシステムの種類と他の型との間'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 44b3e32114b10eae776f39e4c3d7337bba636f3f
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584647"
---
# <a name="convert-between-sharepoint-project-system-types-and-other-visual-studio-project-types"></a>SharePoint プロジェクトシステムの種類とその他の Visual Studio プロジェクトの種類の変換
  場合によっては、SharePoint プロジェクトシステムにオブジェクトがあり、Visual Studio オートメーションオブジェクトモデルまたは統合オブジェクトモデルで対応するオブジェクトの機能を使用する必要がある場合があります。 このような場合は、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> SharePoint プロジェクトサービスのメソッドを使用して、オブジェクトを別のオブジェクトモデルに変換できます。

 たとえば、オブジェクトがある場合に、オブジェクト <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> またはオブジェクトでのみ使用できるメソッドを使用し <xref:EnvDTE.Project> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> ます。 この場合は、メソッドを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> て、を <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> またはに変換でき <xref:EnvDTE.Project> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> ます。

 Visual Studio オートメーションオブジェクトモデルと Visual Studio 統合オブジェクトモデルの詳細については、「 [SharePoint ツールの拡張機能のプログラミングモデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)」を参照してください。

## <a name="types-of-conversions"></a>変換の種類
 次の表に、このメソッドが SharePoint プロジェクトシステムと他の Visual Studio オブジェクトモデルとの間で変換できる型を示します。

|SharePoint プロジェクトシステムの種類|オートメーションおよび統合オブジェクトモデルの対応する型|
|------------------------------------|-------------------------------------------------------------------------|
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>|<xref:EnvDTE.Project><br /><br /> または<br /><br /> プロジェクトの基になる COM オブジェクトによって実装される、Visual Studio 統合オブジェクトモデル内の任意のインターフェイス。 これらのインターフェイスには <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 、、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> (または派生インターフェイス)、およびが含ま <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> れます。 プロジェクトによって実装される主要なインターフェイスの一覧については、「 [プロジェクトモデルのコアコンポーネント](../extensibility/internals/project-model-core-components.md)」を参照してください。|
|<xref:Microsoft.VisualStudio.SharePoint.IMappedFolder><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeature><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectFeatureResourceFile><br /><br /> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectPackage>|<xref:EnvDTE.ProjectItem><br /><br /> または<br /><br /> <xref:System.UInt32>それを含む内のプロジェクトメンバーを識別する値 (VSITEMID とも呼ばれ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます)。 この値は、一部のメソッドの *itemid* パラメーターに渡すことができ <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ます。|

## <a name="example"></a>例
 メソッドを使用してオブジェクトをに変換する方法を次のコード例に示し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.Convert%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> <xref:EnvDTE.Project> ます。

 [!code-csharp[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/CSharp/spprojectserviceaddin/connect.cs#2)]
 [!code-vb[SPExtensibility.ProjectService.FromDTE#2](../sharepoint/codesnippet/VisualBasic/spprojectserviceaddin/connect.vb#2)]

 この例で必要な要素は次のとおりです。

- *EnvDTE.dll*アセンブリへの参照を持つ SharePoint プロジェクトシステムの拡張機能。 詳細については、「[SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

- `projectService_ProjectAdded`オブジェクトのイベントを処理するメソッドを登録するコード <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectAdded> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> 。 例については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
- [方法: SharePoint プロジェクトサービスを取得する](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)
- [SharePoint ツール拡張機能のプログラミング モデルの概要](../sharepoint/overview-of-the-programming-model-of-sharepoint-tools-extensions.md)
