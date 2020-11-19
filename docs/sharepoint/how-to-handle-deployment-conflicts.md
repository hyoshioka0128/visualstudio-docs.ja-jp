---
title: '方法: 配置の競合を処理する |Microsoft Docs'
description: SharePoint プロジェクトアイテムの配置の競合を処理する独自のコードを実装する方法の例を参照してください。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 975fa69a503f5e2acd3e90defd9fa9895c70db00
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903508"
---
# <a name="how-to-handle-deployment-conflicts"></a>方法: 配置の競合を処理する
  SharePoint プロジェクト項目の配置の競合を処理する独自のコードを指定できます。 たとえば、現在のプロジェクト項目のファイルが配置場所に既に存在するかどうかを判断し、現在のプロジェクト項目が配置される前に配置済みのファイルを削除することができます。 配置の競合の詳細については、「 [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)」を参照してください。

### <a name="to-handle-a-deployment-conflict"></a>配置の競合を処理するには

1. プロジェクト項目の拡張機能、プロジェクトの拡張機能、または新しいプロジェクト項目の種類の定義を作成します。 詳細については、次のトピックを参照してください。

    - [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. 拡張機能では、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> オブジェクト (プロジェクト項目の拡張機能またはプロジェクトの拡張機能) または <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> オブジェクト (新しいプロジェクト項目の種類の定義内) のイベントを処理します。

3. イベントハンドラーで、配置されているプロジェクト項目と SharePoint サイトに配置されたソリューションとの間に競合があるかどうかを、シナリオに適用される条件に基づいて判断します。 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A>イベント引数パラメーターのプロパティを使用して、配置されているプロジェクト項目を分析できます。また、この目的のために定義した SharePoint コマンドを呼び出すことによって、配置場所でファイルを分析することができます。

     競合の種類によっては、最初に実行している配置手順を判断する必要があります。 これを行うには、 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> イベント引数パラメーターのプロパティを使用します。 通常、組み込みの配置手順で競合を検出するのは理にかなって <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> いますが、配置手順の間に競合を確認することもできます。

4. 競合が存在する場合は、 <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> イベント引数のプロパティのメソッドを使用して、 <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> 新しいオブジェクトを作成し <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> ます。 このオブジェクトは、配置の競合を表します。 メソッドの呼び出しで <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> 、競合を解決するために呼び出されるメソッドも指定します。

## <a name="example"></a>例
 次のコード例は、リスト定義プロジェクト項目のプロジェクト項目の拡張機能で配置の競合を処理するための基本的なプロセスを示しています。 別の種類のプロジェクトアイテムの配置の競合を処理するには、別の文字列をに渡し <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> ます。 詳細については、「 [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。

 わかりやすくするために、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> この例のイベントハンドラーでは、配置の競合が存在することを前提としています (つまり、常に新しいオブジェクトを追加し <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> `Resolve` ます)。メソッドは、競合が解決されたことを示すために **true** を返します。 実際のシナリオでは、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> イベントハンドラーは、現在のプロジェクト項目内のファイルと配置場所のファイルの間に競合があるかどうかを最初に判断し、競合が存在する場合にのみオブジェクトを追加し <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> ます。 たとえば、イベントハンドラーのプロパティを使用して `e.ProjectItem.Files` プロジェクト項目内のファイルを分析し、SharePoint コマンドを呼び出して配置場所でファイルを分析することができます。 同様に、実際のシナリオでは、メソッドは sharepoint `Resolve` コマンドを呼び出して sharepoint サイトの競合を解決することがあります。 SharePoint コマンドの作成の詳細については、「 [方法: sharepoint コマンドを作成](../sharepoint/how-to-create-a-sharepoint-command.md)する」を参照してください。

 [!code-vb[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [方法: 配置手順の実行時にコードを実行する](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [方法: SharePoint コマンドを作成する](../sharepoint/how-to-create-a-sharepoint-command.md)
