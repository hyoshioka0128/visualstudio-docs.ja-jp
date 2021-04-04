---
title: SharePoint プロジェクトの配置時または取り消し時にコードを実行する
titleSuffix: ''
description: SharePoint プロジェクトの配置時または取り消し時にコードを実行して、Visual Studio によって発生するイベントを処理できるようにする方法について説明します。
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4645d0b2cf1670a3834c4ac09cd66d56b48fbf27
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106214474"
---
# <a name="how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>方法: SharePoint プロジェクトの配置時または取り消し時にコードを実行する
  SharePoint プロジェクトの配置時または取り消し時に追加のタスクを実行する場合は、Visual Studio によって発生するイベントを処理できます。 詳細については、「 [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。

### <a name="to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>SharePoint プロジェクトの配置時または取り消し時にコードを実行するには

1. プロジェクト項目の拡張機能、プロジェクトの拡張機能、または新しいプロジェクト項目の種類の定義を作成します。 詳細については、次のトピックを参照してください。

   - [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

   - [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

   - [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 拡張機能で、オブジェクトにアクセスし <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> ます。 詳細については、「 [方法: SharePoint プロジェクトサービスを取得する](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md)」を参照してください。

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted> プロジェクトサービスのイベントとイベントを処理します。

4. イベントハンドラーでは、パラメーターを使用し <xref:Microsoft.VisualStudio.SharePoint.DeploymentEventArgs> て、現在の配置セッションに関する情報を取得します。 たとえば、現在の配置セッションに含まれているプロジェクトと、そのプロジェクトが配置または取り消しされているかどうかを確認できます。

   次のコード例は、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted> プロジェクトの拡張機能でイベントとイベントを処理する方法を示して <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted> います。 この拡張機能は、SharePoint プロジェクトの配置の開始時と完了時に、追加のメッセージを [ **出力** ] ウィンドウに書き込みます。

   :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handleprojectdeploymentevents.cs" id="Snippet12":::
   :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handleprojectdeploymentevents.vb" id="Snippet12":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [方法: 配置手順の実行時にコードを実行する](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
