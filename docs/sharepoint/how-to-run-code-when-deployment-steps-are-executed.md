---
title: '方法: 配置手順の実行時にコードを実行する |Microsoft Docs'
description: Visual Studio が配置手順を実行する前と後に、SharePoint プロジェクト項目によって発生するイベントを処理するコードを実行します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 00b921d8500c95ebbb771b5c0b5817db87b7c6ca
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304458"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>方法: 配置手順の実行時にコードを実行する
  SharePoint プロジェクトの配置手順に対して追加のタスクを実行する場合は、Visual Studio が各配置手順を実行する前と後に、SharePoint プロジェクト項目によって発生するイベントを処理できます。 詳細については、「 [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。

### <a name="to-run-code-when-deployment-steps-are-executed"></a>配置手順の実行時にコードを実行するには

1. プロジェクト項目の拡張機能、プロジェクトの拡張機能、または新しいプロジェクト項目の種類の定義を作成します。 詳細については、次のトピックを参照してください。

    - [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 拡張機能では、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> オブジェクト (プロジェクト項目の拡張機能またはプロジェクトの拡張機能) または <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> オブジェクト (新しいプロジェクト項目の種類の定義内) のイベントおよびイベントを処理します。

3. イベントハンドラーでは、パラメーターとパラメーターを使用して <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs> <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs> 、配置手順に関する情報を取得します。 たとえば、実行中の配置手順と、ソリューションが配置または取り消しされているかどうかを確認できます。

## <a name="example"></a>例
 次のコード例は、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> リストインスタンスプロジェクト項目の拡張でイベントとイベントを処理する方法を示しています。 この拡張機能は、Visual Studio がソリューションの配置と取り消しの際にアプリケーションプールをリサイクルするときに、追加のメッセージを [ **出力** ] ウィンドウに書き込みます。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb#4)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs#4)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [方法: SharePoint プロジェクトの配置時または取り消し時にコードを実行する](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)
