---
title: サーバーエクスプローラーの組み込みの SharePoint ノードのデータを取得する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5bb69773bf3f031b75d63ebe8cb1f1b4a00286c9
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014894"
---
# <a name="how-to-get-data-for-a-built-in-sharepoint-node-in-server-explorer"></a>方法: サーバーエクスプローラーで組み込みの SharePoint ノードのデータを取得する
  **サーバーエクスプローラー**の組み込みの sharepoint ノードごとに、ノードが表す基になる sharepoint コンポーネントのデータを取得できます。 詳細については、[サーバーエクスプローラーの「SharePoint 接続ノードの拡張](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

## <a name="example"></a>例
 次のコード例では、リストノードが**サーバーエクスプローラー**で表す、基になる SharePoint リストのデータを取得する方法を示します。 既定では、リストノードの [**ブラウザーで表示**] コンテキストメニュー項目をクリックすると、Web ブラウザーでリストを開くことができます。 この例では、visual studio のコンテキストメニュー項目**でビュー**を追加してリストノードを拡張し、visual studio でリストを直接開きます。 このコードは、ノードのリストデータにアクセスして、Visual Studio で開くリストの URL を取得します。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#10](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/serverexplorerextensionnodeinfo.vb#10)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#10](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/serverexplorerextensionnodeinfo.cs#10)]

 この例では、SharePoint プロジェクトサービスを使用して、 <xref:EnvDTE.DTE> Visual Studio でリストを開くために使用されるオブジェクトを取得します。 SharePoint プロジェクトサービスの詳細については、「 [sharepoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

 SharePoint ノードの拡張機能を作成するための基本的なタスクの詳細については、「[方法: サーバーエクスプローラーで sharepoint ノードを拡張](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)する」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- EnvDTE

- Microsoft.VisualStudio.SharePoint

- VisualStudio (拡張子が付いています)

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 **サーバーエクスプローラー**拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [サーバーエクスプローラーで SharePoint 接続ノードを拡張する](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [方法: サーバーエクスプローラーで SharePoint ノードを拡張する](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md)
- [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
