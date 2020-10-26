---
title: '方法: SharePoint コマンドを実行する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], executing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 789b77f3161b5fe566ea033060e8cab16cbaecc7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016987"
---
# <a name="how-to-execute-a-sharepoint-command"></a>方法: SharePoint コマンドを実行する
  SharePoint ツールの拡張機能でサーバーオブジェクトモデルを使用する場合は、API を呼び出すカスタム *SharePoint コマンド* を作成する必要があります。 コマンドを定義し、SharePoint ツールの拡張機能を使用して配置した後、コマンドを実行して、SharePoint サーバーオブジェクトモデルを呼び出すことができます。 コマンドを実行するには、オブジェクトの ExecuteCommand メソッドのいずれかを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> ます。

 SharePoint コマンドの目的の詳細については、「 [sharepoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

### <a name="to-execute-a-sharepoint-command"></a>SharePoint コマンドを実行するには

1. SharePoint ツールの拡張機能で、オブジェクトを取得 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> します。 オブジェクトを取得する方法は、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> 作成する拡張機能の種類によって異なります。

    - SharePoint プロジェクトシステムの拡張機能で、プロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> ます。

         プロジェクトシステムの拡張機能の詳細については、「 [SharePoint プロジェクトシステムの拡張](../sharepoint/extending-the-sharepoint-project-system.md)」を参照してください。

    - **サーバーエクスプローラー**の [ **SharePoint 接続**] ノードの拡張機能で、プロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> ます。 オブジェクトを取得するには <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> 、プロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> ます。

         **サーバーエクスプローラー**拡張機能の詳細については、[サーバーエクスプローラーの「SharePoint 接続ノードの拡張](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)」を参照してください。

    - プロジェクトテンプレートウィザードなど、SharePoint ツールの拡張機能の一部ではないコードでは、プロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> ます。

         プロジェクトサービスの取得の詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

2. オブジェクトの ExecuteCommand メソッドのいずれかを呼び出し <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> ます。 実行するコマンドの名前を、ExecuteCommand メソッドの最初の引数に渡します。 コマンドにカスタムパラメーターがある場合は、そのパラメーターを ExecuteCommand メソッドの2番目の引数に渡します。

     サポートされているコマンド署名ごとに異なる ExecuteCommand オーバーロードがあります。 次の表に、サポートされている署名と、各署名に使用するオーバーロードを示します。

    |コマンド署名|使用する ExecuteCommand のオーバーロード|
    |-----------------------|------------------------------------|
    |コマンドは、既定のパラメーターのみを持ち、 <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> 戻り値はありません。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |コマンドには、既定のパラメーターと戻り値のみが含まれてい <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> ます。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |このコマンドには2つのパラメーター (既定の <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターとカスタムパラメーター) があり、戻り値はありません。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |このコマンドには、2つのパラメーターと戻り値があります。|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>例
 次のコード例は、「 <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> `Contoso.Commands.UpgradeSolution` [方法: SharePoint コマンドを作成](../sharepoint/how-to-create-a-sharepoint-command.md)する」で説明されているコマンドをオーバーロードを使用して呼び出す方法を示しています。

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#6)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#6)]

 `Execute`この例に示すメソッドは、 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> カスタム配置手順でインターフェイスのメソッドを実装したものです。 このコードをより大きな例のコンテキストで表示するには、「 [チュートリアル: SharePoint プロジェクトのカスタム配置手順を作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)する」を参照してください。

 メソッドの呼び出しの詳細については、次の点に注意して <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> ください。

- 最初のパラメーターは、呼び出すコマンドを識別します。 この文字列は、コマンド定義のに渡す値と一致し <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> ます。

- 2番目のパラメーターは、コマンドのカスタム2番目のパラメーターに渡す値です。 この場合、SharePoint サイトにアップグレードされる *.wsp* ファイルの完全なパスになります。

- このコードは、暗黙的な <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> パラメーターをコマンドに渡しません。 このパラメーターは、SharePoint プロジェクトシステムの拡張機能からコマンドを呼び出したとき、または**サーバーエクスプローラー**の [ **sharepoint 接続**] ノードの拡張機能からコマンドを呼び出すと、コマンドに自動的に渡されます。 インターフェイスを実装するプロジェクトテンプレートウィザードなど、他の種類のソリューションで <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> は、このパラメーターは **null**になります。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、VisualStudio アセンブリへの参照が必要です。

## <a name="see-also"></a>関連項目
- [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)
- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
